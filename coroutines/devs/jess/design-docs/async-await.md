# Async/Await Implementation

## Motivation

[Scala Async](https://github.com/scala/async) is a library-level extension for Scala. It allows users to easily write complex asynchronous code that is translated into calls to [`scala.concurrent`](http://www.scala-lang.org/files/archive/nightly/docs/library/#scala.concurrent.package).

## Goals

## High-Level Overview

The inspiration for this implementation comes from the Async/Await implementation in the [examples section](https://git.io/volQ8). However, to complete the design, we need to add error handling. Currently, errors are not bubbled up to the `async` level. 

## Detailed Design

## Alternatives Considered
