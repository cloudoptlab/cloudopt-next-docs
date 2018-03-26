﻿## What is Kotlin?

![Kotlin](data:image/jpeg;base64,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)

Kotlin is a statically typed programming language based on the JVM. It originated from JetBrains' St. Petersburg team, and its name are from Kotlin Island near St. Petersburg. From the well-known IDE IntelliJ IDEA (Android Studio based on this development) software development company JetBrains (located in Eastern Europe, Czech Republic).

Kotlin is a new programming language that targets the Java platform. It is clean, safe, elegant, and focused on interoperability with Java code. It can be used almost everywhere Java is used today: server-side development, Android application development, and more. Kotlin can coexist well with existing Java libraries and frameworks.

Kotlin is ideal for developing server-side applications, allowing concise, expressive code while maintaining full compatibility with existing Java-based technology stacks and a smooth learning curve:

- Expressiveness: Kotlin's innovative language features, such as support for type-safe builders and delegate attributes, help build strong, easy-to-use abstractions.

- Scalability: Kotlin's support for coroutines helps to build server-side applications that scale to moderate hardware requirements to handle large numbers of clients.

- Interoperability: Kotlin is fully compatible with all Java-based frameworks, allowing you to maintain a familiar technology stack while gaining the advantage of a more modern language.

- Migration: Kotlin supports the gradual migration of large code libraries from Java to Kotlin. You can start writing new code in Kotlin while continuing to use Java in the older parts of the system.

- Tools: In addition to great IDE support, Kotlin also provides framework-specific tools (such as Spring) for plug-ins for IntelliJ IDEA Ultimate.

- Learning curve: For Java developers, getting started with Kotlin is easy. The automatic Java to Kotlin converter included in the Kotlin plug-in helps to take the first step. Kotlin Heartprint provides a guide to the main functions of the language through a series of interactive exercises.

## Cloudopt Next and Kotlin

The interaction between Kotlin and Java is very good, it can be said to be seamless. Kotlin can freely reference Java code. Java can also directly reference Kotlin's code. Kotlin is more suitable for Cloudopt Next than languages like Scala.

The core and plug-ins of Cloudopt Next are basically developed through Kotlin. Kotlin effectively improves development efficiency and reduces the amount of code. To give you a better reading experience, the code examples in the Cloudopt Next documentation both use the Kotlin and Java syntax.
