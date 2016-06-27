# Milestones

This GSoC project has five stages. Below, each stage is listed along with its sub-goals and expected time to completion.

## Warm-up Tasks
#### Allotted Time: 3 Weeks
- Setup Coroutines fork and solve the specialization puzzle in the intro doc (2 days)
- Understand and document all test cases inside Coroutines repo (1 day)
- Add missing test cases (1 day)
- Investigate Async/Await tests mentioned in [this issue](https://github.com/storm-enroute/coroutines/issues/15), and port an Async/Await test into Coroutines (1 day)
- Port 1/4 tests from Async/Await into Coroutines (1 day)
- Port 1/4 tests from Async/Await into Coroutines (1 day)
- Port 1/4 tests from Async/Await into Coroutines (1 day)
- Port 1/4 tests from Async/Await into Coroutines (1 day)
- Fix issues discovered while porting the tests over (1-5 days)

## Async/Await
#### Allotted Time: 2 Weeks
- Write a design doc that contains a plan for the implementation of Async/Await. Make sure it pays special attention to failure handling (2 days)
- Add and document motivating examples that will serve as unit tests (1 day)
- Implement Async/Await. (5 days) 
- Port remaining example and test code from Scala Async into Coroutines (2 days)

## Enumerators
#### Allotted Time: 3 Weeks
- Write a design doc, including descriptions of any basic data structures to implement (2 days)
- Create and document motivating examples for when enumerators are better than iterators. These examples will also serve as unit tests (2 days)
- Add boxing and specialization tests in the style of Scalameter (2 days)
- Implement basic enumerators using coroutines (3 days) (**Note**: More details will be added here when they are planned out via the design doc)
- Specialize enumerators (2 days)
- Implement data structures described in the design doc (2 days)
- Add performance benchmarks (2 days)

## Continuations
#### Allotted Time: 3 Weeks
- Write a design doc (2 days)
- Read this [Wiki Page](https://en.wikipedia.org/wiki/Delimited_continuation) and [this article](http://users.eecs.northwestern.edu/~clk800/rand-test-study/_ifpdcbatsc/ifpdcbatsc-2009-10-8-12-02-00.pdf) (1 day)
- Create and document motivating examples for continuations. Explain why, in some situations, continuations are better than coroutines. These examples will also serve as unit tests (2 days)
- Implement continuations as described in the design doc (4 days) (**Note**: More details will be added here when they are planned out via the design doc)
- Add and document exhaustive tests (3 days)
- Add boxing tests (1 day)
- Add performance benchmarks (2 days)

## Event-Driven Coroutines
#### Allotted Time: 2 Weeks
- Write a design doc (2 days)
- Add motivating examples from [this document](https://infoscience.epfl.ch/record/176887/files/DeprecatingObservers2012.pdf), explaining why event-driven coroutines lead to cleaner code than the observer pattern does (2 days)
- Implement a tool that converts procedural code to a callback-based equivalent (3 days) (**Note**: More details will be added here when they are planned out via the design doc)
- Add correctness tests (2 days)
- Add performance tests (1 day)
