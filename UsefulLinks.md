# Useful Links

Ok, more than just links … but that's what I started with.

## Contents

  1. [Linux Stuff](#linux-stuff)
  2. [MacOS Stuff](#macos-stuff)
  3. [The Raspberry&nbsp;Pi]()
  4. []()
  5. []()
  6. []()
  7. []()
  8. []()
  9. []()
  10. []()
  11. []()
  12. []()
  13. []()
  14. []()

---
## [Linux Stuff](stuff/LinuxStuff.md)

Several tips and tricks for the Linux operating system, together with some useful links – not only for desktop and laptop installations, but also for the Raspberry&npsp;Pi. Some stuff is useful even for the Mac.

---
## [MacOS Stuff](stuff/MacStuff.md)

## [Windows Stuff](stuff/WindowsStuff.md)

---
## [The Raspberry&nbsp;Pi](stuff/RaspberryStuff.md)

Information about the Raspberry&npsp;Pi, projects based on that computer and related stuff.

---
## The Arduino and alike

This section is under construction … ok, nothing here yet.

---
## Java

Information about the Java programming language, the JVM itself, and about other programming languages that are implemented for the JVM.

### General Stuff

#### The Java Language Specification
See [here](https://docs.oracle.com/javase/specs/) for the various versions of the *JLS* and also the Java Virtual Machine Specifications for the various editions, beginning with Java 6. Both documents are available as PDF, too. See [here](http://titanium.cs.berkeley.edu/doc/java-langspec-2.0.pdf) for "The Java Language Specification, Second Edition", covering the language as it was before Java&nbsp;5.

For the currently relevant versions, the respective links are in the sections for that version, below.

Important changes were made in [Java&nbsp;5](http://www.inf.unibz.it/~calvanese/teaching/java-docs/5.0/guide/language/index.html) (Generics, enum, static imports …), [Java&nbsp;8](https://docs.oracle.com/javase/specs/jls/se8/html/index.html) (Lambdas, …), and [Java&nbsp;9](https://docs.oracle.com/javase/specs/jls/se9/html/index.html) (Modules, …),

#### JVM Languages
- [List of JVM languages](https://en.wikipedia.org/wiki/List_of_JVM_languages)\
  The Wikipedia article about the alternative JVM languages, with a current list of the various implementations.
- [Alternative Languages for the JVM](https://www.oracle.com/technical-resources/articles/java/architect-languages.html)\
  This article deals not only with languages that can be used with the Scripting API, but with other first class languages like Scala, too.
- [A Complete Guide to JVM Languages](https://www.whizlabs.com/blog/jvm-languages/)\
  This article deals mainly with alternative languages on the JVM, and ignores their use as script languages inside a Java application.
- [An Overview of the JVM Languages](https://www.baeldung.com/jvm-languages)\
  Another article about the first class languages

###### The Java Scripting API (JSR223)
- [JSR 223: Scripting for the JavaTM Platform](https://www.jcp.org/en/jsr/detail?id=223) - The original Java Specification Request for Java Scripting
- [Java Platform, Standard Edition Java Scripting Programmer's Guide](https://docs.oracle.com/javase/8/docs/technotes/guides/scripting/prog_guide/) for Java 8
- [Java Scripting Programmer's Guide](https://docs.oracle.com/javase/7/docs/technotes/guides/scripting/programmer_guide/index.html) for Java 7
- [Open Source Scripting Languages in Java](https://java-source.net/open-source/scripting-languages)
- [Lua](#lua)
- [Python](#python-and-jython)

#### AWT and Swing
- [Using Headless Mode in the Java SE Platform](https://www.oracle.com/technical-resources/articles/javase/headless.html)\
  This article explains how to use the headless mode capabilities of the Java Platform, Standard Edition (Java SE, formerly referred to as J2SE). It is a little bit old, but still valid, as long as AWT (and Swing) are part of the Java Platform.\
  JavaFX does not provide a headless mode, but if `java.awt.headless="true"` is set, a JavaFX GUI will most probably not start, too.

### Java 17
- [JDK 17 Documentation](https://docs.oracle.com/en/java/javase/17/)
- [Java® Platform, Standard Edition & Java Development Kit Version 17 API Specification](https://docs.oracle.com/en/java/javase/17/docs/api/index.html)
- [Java Language Specification](https://docs.oracle.com/javase/specs/jls/se17/html/index.html)

### Java 21
- [JDK 21 Documentation](https://docs.oracle.com/en/java/javase/21/)
- [Java® Platform, Standard Edition & Java Development Kit Version 21 API Specification](https://docs.oracle.com/en/java/javase/21/docs/api/index.html)
- [Java Language Specification](https://docs.oracle.com/javase/specs/jls/se21/html/index.html)

### Java 22
- [JDK 22 Documentation](https://docs.oracle.com/en/java/javase/22/)
- [Java® Platform, Standard Edition & Java Development Kit Version 22 API Specification](https://docs.oracle.com/en/java/javase/22/docs/api/index.html)
- [Java Language Specification](https://docs.oracle.com/javase/specs/jls/se22/html/index.html)

### Additional Libraries
- [ActiveMQ](https://activemq.apache.org/): Multi-Protocol Messaging
- [Bouncy Castle](https://www.bouncycastle.org/): The Bouncy Castle project offers open-source APIs for Java that support cryptography and cryptographic protocols. This is the de-facto standard for Java cryptography. 
- [CommonMark Java](https://github.com/commonmark/commonmark-java): A Java library for parsing and rendering [Markdown](https://daringfireball.net/projects/markdown/) text according to the [CommonMark specification](https://commonmark.org/). 
- [H2 Database Engine](https://www.h2database.com/html/main.html): RDBMS implemented in Java
- [HikariCP](https://github.com/brettwooldridge/HikariCP): A high-performance JDBC connection pool.
- [ICU](https://www.google.com/url?q=https%3A%2F%2Funicode-org.github.io%2Ficu-docs%2Fapidoc%2Freleased%2Ficu4j%2F&sa=D&sntz=1&usg=AOvVaw1YNhEXLu7oP-dfkiCyiJMP): I18n utilities
  - For further details, see [here](#icu--international-components-for-unicode)
- [JavaFX](https://openjfx.io/): GUI for Java programs
- [JavaMail](https://eclipse-ee4j.github.io/mail/): The email Handling Library for Java, now named JakartaMail, maintained by the Eclipse Foundation
- [Java Secure Channel](http://www.jcraft.com/jsch/?utm_source=sftptogo&utm_medium=blog): A pure Java implementation of the [SSH2](https://datatracker.ietf.org/wg/secsh/about/), allowing to use for example `sftp` file transfer inside a Java program.
- [JGit](https://git-scm.com/book/en/v2/Appendix-B%3A-Embedding-Git-in-your-Applications-JGit): Embedding Git in Java Applications
- [Lucene](https://lucene.apache.org/): Ultra-fast Searching from the Apache Foundation
  - For further details, see [here](#lucene)
- [Neo4J](https://neo4j.com/): Graph Data Platform 
- [XChart](https://knowm.org/open-source/xchart/): A free Java library for the creation of charts.

### Debugging Tools
- [IBM Pattern Modeling and Analysis Tool for Java Garbage Collector (PMAT)](https://www.ibm.com/support/pages/ibm-pattern-modeling-and-analysis-tool-java-garbage-collector-pmat)
- [IBM Thread and Monitor Dump Analyzer for Java (TMDA)](https://www.ibm.com/support/pages/ibm-thread-and-monitor-dump-analyzer-java-tmda)
- [IBM HeapAnalyzer](https://www.ibm.com/support/pages/ibm-heapanalyzer)
- [Tagtraum GCViewer 1.29](https://www.tagtraum.com/gcviewer-download.html)
- [Tagtraum GCViewer 1.36](https://github.com/chewiebug/GCViewer)
- [Eclipse Memory Analyzer™](https://projects.eclipse.org/projects/tools.mat)

### Downloads

---

## Lua

- [The Programming Language Lua](https://www.lua.org)
- [Lua — a language meant to be embedded](https://medium.com/avenga/lua-a-language-meant-to-be-embedded-1cd2488b4370)
- Luaj [on SourceForge](https://sourceforge.net/projects/luaj/) or on [GitHub](https://github.com/luaj)
- [luajava](https://github.com/jasonsantos/luajava)

---

## Python and Jython
- [HomePage](https://www.python.org/): The starting point for Python development
- [Jython](https://www.jython.org/) (find it on GitHub [here](https://github.com/jython/jython))
- [Learn Jython](https://www.tutorialspoint.com/jython/index.htm)

### Python IDEs and Development Tools
-  [PyCharm](https://www.jetbrains.com/pycharm/): The Python IDE from JetBrains

---

## HTML

---

## XML

---

## Markdown
- [Basic Markdown writing and formatting (Github)](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
- [Codecademy Markdown Tutorial](https://www.codecademy.com/resources/docs/markdown)

---

## Github
- [Help for the Jekyll theme 'Dinky'](https://githubhelp.com/pages-themes/dinky)
- [Install the Git-Credential-Manager](https://github.com/microsoft/Git-Credential-Manager-for-Mac-and-Linux/blob/master/Install.md)\
  This is required to push to github without the need to provide the password (access token) manually.

---

## WebEx
- [Building Bots](https://developer.webex.com/docs/bots)

---

## ICU – International Components for Unicode
- [Homepage](https://icu.unicode.org/)
- [Github](https://unicode-org.github.io/icu/): The new home for ICU since August 2020

---

## Lucene
- [Lucene Core 9.3.0](https://lucene.apache.org/core/9_3_0/core/index.html) JavaDoc
- [Lucene Core 9.4.0](https://lucene.apache.org/core/9_4_0/core/index.html) JavaDoc
- [Baeldung: Guide to Lucene Analyzers](https://www.baeldung.com/lucene-analyzers)

---

## TeX and LaTeX
- [Additional Links and Infos](stuff/TexStuff.md)

---

## Graphics and Image Handling
- [Graphviz](https://graphviz.org/) Generation of graphs

