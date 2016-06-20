# Async/Await Implementation

## Motivation

[Scala Async](https://github.com/scala/async) is a library-level extension for 
Scala. It allows users to easily write complex asynchronous code that is 
translated into calls to 
[`scala.concurrent`](http://www.scala-lang.org/files/archive/nightly/docs/library/#scala.concurrent.package).
We want to design an alternative that can be used with the coroutines library 
without having to include Scala Async. 

## Goals

We want to design an Async/Await implementation that is both powerful and simple.

- Fast, with minimal overhead over regular futures
- Graceful handling of errors regardless of their origin

## High-Level Overview

The inspiration for this implementation comes from the Async/Await implementation in the [examples section](https://git.io/volQ8). However, to complete the design, we need to add error handling. Currently, errors are not bubbled up to the `async` level. 

These errors can occur either when trying to get the result of either the coroutine or the future returned from an `await` call.

## Detailed Design

Consider the following implementation [defined in Coroutines](https://github.com/storm-enroute/coroutines/blob/47cffcfe565db4f20192afec4d35682aecb57812/src/test/scala/org/examples/AsyncAwait.scala#L13). 

```scala
class Cell[+T] {
  var x: T @uncheckedVariance = _
}

def await[R]: Future[R] ~~> ((Future[R], Cell[R]), R) =
  coroutine { (f: Future[R]) =>
    val cell = new Cell[R]
    yieldval((f, cell))
    cell.x
  }

def async[Y, R](body: ~~~>[(Future[Y], Cell[Y]), R]): Future[R] = {
  val c = call(body())
  val p = Promise[R]
  def loop() {
    if (!c.resume) p.success(c.result)
    else {
      val (future, cell) = c.value
      for (x <- future) {
        cell.x = x
        loop()
      }
    }
  }
  Future { loop() }
  p.future
}
```

Note that there are no checks to see if `c.hasException` or to see if `future` failed.

We propose the following alternative:

```scala
class Cell[+T] {
  var x: T @uncheckedVariance = _
}

def await[R]: Future[R] ~~> ((Future[R], Cell[R]), R) =
  coroutine { (f: Future[R]) =>
    val cell = new Cell[R]
    yieldval((f, cell))
    cell.x
  }

def async[Y, R](body: ~~~>[(Future[Y], Cell[Y]), R]): Future[R] = {
  val c = call(body())
  val p = Promise[R]
  def loop() {
    if (!c.resume) {
      c.tryResult match {
        case Success(result) => p.success(result)
        case Failure(exception) => p.failure(exception)
      }
    } else {
      val (future, cell) = c.value
      future onComplete {
        case Success(x) =>
          cell.x = x
          loop()
        case Failure(exception) =>
          p.failure(exception)
      }
    }
  }
  Future { loop() }
  p.future
}
```
