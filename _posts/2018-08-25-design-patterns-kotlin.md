---
layout: post 
title: "Design Patterns and Aspects of Kotlin"
date: 2018-08-25
date_updated: 2018-09-30
abst: "Some design patterns are easier to implement in Kotlin than in other languages."
categories: design-patterns computer-science kotlin

---

# The Kotlin programming language

The [Kotlin programming language](http://kotlinlang.org) is a statically typed language with a functional programming style. Designed to run on the Java Virtual Machine (JVM), Kotlin inherits the architecture (near-)independent advantages from Java. 

The evolution of programming languages is related to the evolution of development culture, practices, design principles, the software industry and theory in computer science. Kotlin is a relatively new language, and since it was designed by JetBrains in 2011 it has gained widespread adoption, and it is currently integrated into the Android Studio development suite. Its growth may be attributed to some interesting language features and properties, some of which will be mentioned in this note.

# Patterns

The software development culture has seen a number of design problems occuring time after time. The solutions to these recurrent problems have been referred to as *design patterns* -- a group of design best-practises to a group of common scenarios. In this note, I demonstrate how the [strategy pattern](#strategy-pattern-in-kotlin) and the [singleton pattern](#singleton-pattern-in-kotlin) can be applied in Kotlin. 

## Strategy Pattern in Kotlin

The strategy pattern is one of the original behaviour patterns defined in Gamma, "Design Patterns". According to Gamma, the intent of a strategy pattern is to 

*Define a family of algorithms, encapsulate each one, and make interchangeable. Strategy lets the algorithm vary independently from clients that use it.*

Adopting this pattern makes it easier to apply several operations that conform to a common contract. And no subclassing or inheritance is necessary using *Strategy*. 

Consider a simple class with one method. In Kotlin, it is possible to make several overrideable methods (strategies) in this way:
    
    class Example(val CoreStrategy: (Double, Double) -> Double) {
        fun calculate(a: Double, b: Double){
            println("calculation: ${CoreStrategy.invoke(a, b)}")
        }
    }

    val strategy1 = { x: Double, y: Double -> x + y }
    val strategy2 = { x: Double, y: Double -> x * y }


    fun main(args: Array<String>) {

        val example1 = Example(strategy1);
        val example2 = Example(strategy2);

        example1.calculate(3.0, 4.0);
        example2.calculate(3.0, 4.0);
    }

Two strategies have been defined. One that adds two numbers, and another that multiplies numbers. Running this code with `x = 3.0` and  `y = 4.0` would (not unexpectedly) output,

    calculation: 7.0
    calculation: 12.0


To achieve the same thing in Java we would declare an interface (according to Java coding style). In Kotlin, however, strategy pattern can be achieved through concepts such as [Function Type](https://kotlinlang.org/docs/reference/lambdas.html#function-types) and [Higher Order Functions and Lambdas](https://www.kotlinlang.org/docs/reference/lambdas.html). A *Function Type* is a type signature not unlike those found in Haskell. In the above code example we see that the strategy `CoreStrategy` is specified as a function type `val CoreStrategy: (Double, Double) -> Double` (a function signature accepting two arguments each of type double, and returns a value of type double). The function signature matches the structure of the strategy operation lambda definitions (`strategy1` and `strategy2`). 

As a side note, we also see that in Kotlin it is possible to define functions in the same namespace as classes, much the same way as in Python. 

## Singleton Pattern in Kotlin

It is sometimes useful to embed instance control into the design. According to Gamma "Design Patterns", the intent of a singleton is to,

*Ensure a class only has one instance, and provide a global point of access to it.*

Kotlin has native support for object declarations,

    object TestObject
        {
            fun testMethod() {
                // definition
            }
        }

The `testMethod` method can be used in the code as `TestObject.testMethod()`. 

The `object` definitions in Kotlin is thread-safe. Moreover, since there is no "static" keyword in Kotlin (static members can not be declared explicitly), the `object` offer a static-like behaviour, which is sometimes useful. 

On the level of the JVM, an `object` is implemented as a class with static members that keeps track of the creation of the instance. In Java we would have to implement this class ourselves (with the potential pitfalls involved in thread-handling). However, Kotlin takes care of instance-handling, in a safe manner. 
