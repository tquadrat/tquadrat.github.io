# Java Stuff
Information about the Java programming language, the Java eco-system, the JVM itself, and about other programming languages that are implemented for the JVM. Here I collected various stuff related to these topics that I encountered in the past and found useful.

## Contents

 1. **[The Java Language Specification](#the-java-language-specification)
 1. **[JVM Languages](#jvm-languages)
 1. **[AWT and Swing](#awt-and-swing)
 1. **[Additional Libraries](#additional-libraries)
 1. **[Debugging Tools](#debugging-tools)
 1. **[JShell Startup Configuration](#jshell-startup-configuration)**
 2. **[Code Snippets](# code-snippets)

## The Java Language Specification
The "Java Language Specification" is the authoritative source for all questions concerning the Java programming language. See [here](https://docs.oracle.com/javase/specs/) for the various versions of the *JLS* and also the Java Virtual Machine Specifications for the various editions, beginning with Java 6. Both documents are available as PDF, too. See [here](http://titanium.cs.berkeley.edu/doc/java-langspec-2.0.pdf) for "The Java Language Specification, Second Edition", covering the language as it was before Java&nbsp;5.

For the currently relevant versions, the respective links are in the sections for that version, below.

Important changes were made in [Java&nbsp;5](http://www.inf.unibz.it/~calvanese/teaching/java-docs/5.0/guide/language/index.html) (Generics, enum, static imports …), [Java&nbsp;8](https://docs.oracle.com/javase/specs/jls/se8/html/index.html) (Lambdas, …), and [Java&nbsp;9](https://docs.oracle.com/javase/specs/jls/se9/html/index.html) (Modules, …).

### Java 17
 - [JDK 17 Documentation](https://docs.oracle.com/en/java/javase/17/)
 - [Java® Platform, Standard Edition & Java Development Kit Version 17 API Specification](https://docs.oracle.com/en/java/javase/17/docs/api/index.html)
 - [Java Language Specification](https://docs.oracle.com/javase/specs/jls/se17/html/index.html)

### Java 21
 - [JDK 21 Documentation](https://docs.oracle.com/en/java/javase/21/)
 - [Java® Platform, Standard Edition & Java Development Kit Version 21 API Specification](https://docs.oracle.com/en/java/javase/21/docs/api/index.html)
 - [Java Language Specification](https://docs.oracle.com/javase/specs/jls/se21/html/index.html)

### Java 25
 - [JDK 25 Documentation](https://docs.oracle.com/en/java/javase/25/)
 - [Java® Platform, Standard Edition & Java Development Kit Version 25 API Specification](https://docs.oracle.com/en/java/javase/25/docs/api/index.html)
 - [Java Language Specification](https://docs.oracle.com/javase/specs/jls/se25/html/index.html)

## JVM Languages
Java is not the only language that can be executed on the JVM.

 - [List of JVM languages](https://en.wikipedia.org/wiki/List_of_JVM_languages)\
   The Wikipedia article about the alternative JVM languages, with a current list of the various implementations.
 - [Alternative Languages for the JVM](https://www.oracle.com/technical-resources/articles/java/architect-languages.html)\
   This article deals not only with languages that can be used with the Scripting API, but with other first class languages like Scala, too.
 - [A Complete Guide to JVM Languages](https://www.whizlabs.com/blog/jvm-languages/)\
   This article deals mainly with alternative languages on the JVM, and ignores their use as script languages inside a Java application.
 - [An Overview of the JVM Languages](https://www.baeldung.com/jvm-languages)\
   Another article about the first class languages.

### The Java Scripting API (JSR223)
The Java Scripting API describes how to use other languages for scripting inside a Java application.
 - [JSR 223: Scripting for the JavaTM Platform](https://www.jcp.org/en/jsr/detail?id=223) – The original Java Specification Request for Java Scripting
 - [Java Platform, Standard Edition Java Scripting Programmer's Guide](https://docs.oracle.com/javase/8/docs/technotes/guides/scripting/prog_guide/) for Java 8
 - [Java Scripting Programmer's Guide](https://docs.oracle.com/javase/7/docs/technotes/guides/scripting/programmer_guide/index.html) for Java 7
 - [Open Source Scripting Languages in Java](https://java-source.net/open-source/scripting-languages)
 - [Lua](../UsefulLinks.md#lua)
 - [Python](../UsefulLinks.md#python-and-jython)

## AWT and Swing
 - [Using Headless Mode in the Java SE Platform](https://www.oracle.com/technical-resources/articles/javase/headless.html)\
   This article explains how to use the headless mode capabilities of the Java Platform, Standard Edition (Java SE, formerly referred to as J2SE). It is a little bit old, but still valid, as long as AWT (and Swing) are part of the Java Platform.\
   JavaFX does not provide a headless mode, but if `java.awt.headless="true"` is set, a JavaFX GUI will most probably not start, too.

## Additional Libraries
 - **[ActiveMQ](https://activemq.apache.org/)**\
   Multi-Protocol Messaging
   
 - **[Bouncy Castle](https://www.bouncycastle.org/)**\
   The Bouncy Castle project offers open-source APIs for Java that support cryptography and cryptographic protocols. This is the de-facto standard for Java cryptography.
    
 - **[CommonMark Java](https://github.com/commonmark/commonmark-java)**\
   A Java library for parsing and rendering [Markdown](https://daringfireball.net/projects/markdown/) text according to the [CommonMark specification](https://commonmark.org/). See also [here](../UsefulLinks.md/#markdown).
    
 - **[H2 Database Engine](https://www.h2database.com/html/main.html)**\
   An RDBMS implemented in pure Java.
   
 - **[HikariCP](https://github.com/brettwooldridge/HikariCP)\
   A high-performance JDBC connection pool.
   
 - **[ICU](https://www.google.com/url?q=https%3A%2F%2Funicode-org.github.io%2Ficu-docs%2Fapidoc%2Freleased%2Ficu4j%2F&sa=D&sntz=1&usg=AOvVaw1YNhEXLu7oP-dfkiCyiJMP)\
   I18n utilities; for further details regarding this library and how to use it, see [here](#icu--international-components-for-unicode).
   
 - **[JavaFX](https://openjfx.io/)**\
   A library for the creation of sophisticated GUIs for Java programs; originally meant as a replacement for AWT and Swing it is now separated from core Java.
   
 - **[JavaMail](https://eclipse-ee4j.github.io/mail/)**\
   The email Handling Library for Java, now named JakartaMail, maintained by the Eclipse Foundation.
   
 - **[Java Parser](https://javaparser.org/)**\
   The de-facto standard for the parsing of Java source code.
   
 - **[Java Secure Channel](http://www.jcraft.com/jsch/?utm_source=sftptogo&utm_medium=blog)**\
   A pure Java implementation of the [SSH2](https://datatracker.ietf.org/wg/secsh/about/), allowing to use for example `sftp` file transfer inside a Java program.
   
 - **[JGit](https://git-scm.com/book/en/v2/Appendix-B%3A-Embedding-Git-in-your-Applications-JGit)**\
   Embedding Git in Java Applications.
   
 - **[Lucene](https://lucene.apache.org/)**\
   Ultra-fast searching within a Java application; for further details, see [here](../UsefulLinks.md#lucene).

 - **[Neo4J](https://neo4j.com/)**\
   A graph data platform; more than a database.
   
 - **[XChart](https://knowm.org/open-source/xchart/)**\
   A free Java library for the creation of charts.

## Debugging Tools
 - [IBM Pattern Modeling and Analysis Tool for Java Garbage Collector (PMAT)](https://www.ibm.com/support/pages/ibm-pattern-modeling-and-analysis-tool-java-garbage-collector-pmat)
 - [IBM Thread and Monitor Dump Analyzer for Java (TMDA)](https://www.ibm.com/support/pages/ibm-thread-and-monitor-dump-analyzer-java-tmda)
 - [IBM HeapAnalyzer](https://www.ibm.com/support/pages/ibm-heapanalyzer)
 - [Tagtraum GCViewer 1.29](https://www.tagtraum.com/gcviewer-download.html)
 - [Tagtraum GCViewer 1.36](https://github.com/chewiebug/GCViewer)
 - [Eclipse Memory Analyzer™](https://projects.eclipse.org/projects/tools.mat)

## [JShell Startup Configuration](stuff/jshellConfig.md)
Pre-load and execute code in JShell on startup.

## Code Snippets
This is a collection of useful code snippets that are not necessarily worth to be implemented as a utility method (or they cannot be generalised).

 1. [Snippet](#snippet)
 
 ### Snippet
 