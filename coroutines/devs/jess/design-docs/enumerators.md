# Enumerators Implementation

## Motivation

## Goals

- `foreach` method
- `map` to return a container

## High-Level Overview

- `foreach`

  Implemented as a method on `Coroutine.Instance[Y, R]`. Called at all yield points. Not called at the `result` point because this might incur boxing if, for instance, the coroutine returns `Unit`. 
  
- `map`

  Implemented using `foreach`. Returns an `immutable.List[Y]` that is specialized on `Y`. 

## Detailed Design

These functions are both defined on a `Coroutine.Instance[Y, R]`. Boxing should be avoided since this class is specialized on `Y`.

```scala
import scala.collection._
import scala.util.{ Success, Failure }

def foreach(f: (Y) => Unit) {
  while (resume) {
    tryValue match {
      case Success(value) => f(value)
      case Failure(exception) => throw exception
    }
  }
}

def map(f: (Y) => Y) = {
  var resultList = immutable.Seq.empty[Y]
  foreach { element => 
    resultList = resultList :+ f(element)
  }
  resultList.toList
}
```
