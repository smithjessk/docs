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

```scala
import scala.collection._

def map[@specialized Y, R](c: Coroutine.Instance[Y, R]) = {
    var resultList = immutable.Seq[Y]
    c.foreach { element => 
      resultList = resultList :+ element
    }
    resultList.toList
}
```
