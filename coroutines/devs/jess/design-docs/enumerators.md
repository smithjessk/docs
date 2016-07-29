# Enumerators Implementation

## Motivation

## Goals

- Function that converts from a coroutine instance to an enumerator
- Specialized `Enumerator` class
- Collection options on the `Enumerator` class, e.g. `foreach`, `map`
- Unit tests
- Benchmarks

## High-Level Overview

- Conversion function

  The enumerator pauses at all `yield` points. It should not pause at the `result` point because this might incur boxing if, for instance, the coroutine returns `Unit`. 

- Specialized `Enumerator` class

  Should be specialized on all primitive types, just like the `Coroutine` trait. 

- Collection methods

  Should implement, at least, `foreach`, `map`, `flatMap`, `++`, and `fold`. 

- Unit tests

  Written before the API is implemented. Should test all collection methods and the conversion from coroutine instance to `Enumerator`. 

- Benchmarks
 
  Implemented with Scalameter. Test both speed and amount of boxing.
