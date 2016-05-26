# Daily Progress

## Warm-Up Tasks 
- **23 May 2016**: Got set up with Coroutines. Hooked up both IntelliJ and SBT on multiple machines. Learned a lot about Java Bytecode and the JRE trying to figure out why [this version of boxing-tests.scala](https://github.com/storm-enroute/coroutines/blob/487e58d0cc2b85e0b4253d1b7baf70bb01c11241/src/test/scala/org/coroutines/boxing-tests.scala) still has a value boxed. I think I may be onto the solution, and will pursue it tomorrow. 

- **24 May 2016**: Looked through the Java bytecode more. Had to learn to read through bytecode and mentally translate that to a place in the codebase. Was super hard, but it was also super rewarding to see some of the Scala / Java internals. Got a lot more adept at using `javap` to understand the structure of a Java program. Couldn't figure out the boxing issue, but looked through the [fixing commit](https://github.com/storm-enroute/coroutines/commit/008db410f07d28b4e0d05e9169be7e5289468793) and understood it.

- **25 May 2016**: Dove deeper into Coroutines by looking through and understanding its tests. I got a much better feel for the specialization (and lack thereof) of different parts of the project. Documented some methods inside the Frame class both for my own understanding and for the ScalaDoc API. Learned more about how Coroutines are actually implemented by looking through Synthesizer.scala and Stack.scala. Added some tests that I felt were missing, and documented others. Tomorrow I will continue to do more or less the same things I did today, except with a focus on writing new tests.
