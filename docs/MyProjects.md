# My Projects
I do this stuff only for my own pleasure. If you like some of this stuff – have fun! And if you have questions, please feel free to send me an email (to <tquadrat.do@gmail.com>) or you can connect me on Telegram (at `@tquadrat_do`). If you have a suggestion for an improvement, or if you find a bug, I would be happy to hear from you, too.

When programming, I write code mainly in Java, preferred using the latest stable (LTS) language version (as of now – 2026-05-13 – this is Java 25) even with the preview features switched on. I also use Go, Python and some other languages when appropriate (or I want to have some extra fun).

To build Java projects, I am using Gradle because I think it is superior over Maven (and that was quite powerful already).

And I still prefer Subversion over Git as my SCM. This means that my repositories here on Github are more or less mirrors of those on my Subversion server that I really use to manage my sources – perhaps you want to have a look to my [`gitpublisher` Gradle Plugin](#gitpublisher) that does the mirroring?

My target operating system is Linux, both on PCs (Ubuntu) and on Raspberry PIs (Raspberry Pi OS), although sometimes I do something for MacOS and/or Windows as well. Ok, when using Java, it usually does not matter which operating system you use, but when JavaFX comes into play (or local files …), this changes. So when some code does not run on your Windows box, it may be because I built it for Linux and never tested it elsewhere. But you can tell me, and I will try to fix it.

I am a big friend of documentation, and in my opinion, most documentation should be placed as close to the code as possible. Therefore it is really helpful that I am also a big fan of Javadoc (for Java) and related tools (for other languages). So at least for the tools and libraries, most if not all information you need to use them can be found in the Javadoc reference documents – as said: as close to the code as possible. General information is placed to the overview, sometimes also in the package overview documents. If you miss something (or the documentation raises more questions than providing answers), please contact me.

By the way, the generated Javadoc does also provide links to the related source code in most cases.

Oh, and before I forget to mention: a lot of the stuff is work in progress or otherwise in complete. Use with caution!

## Applications
### *[The Shooting Timer](https://tquadrat.github.io/shootingtimer)*
A tool that may help with the training for some shooting competitions.

### *[Bloodpressure Statistics](https://tquadrat.github.io/bloodpressure)*
A program for the statistical analysis of blood pressure values. Currently quite basic, and running in a terminal only, but I am still planning to build a GUI for it.

Make your doctors happy and provide them with some statistics about your blood pressure data – ok, that requires that you collect them first …

## Tools
### *[foundation-javadoc](https://tquadrat.github.io/foundation-javadoc)*
This is an extension to the standard `javadoc` tool, providing a UML graph, the capability to include arbitray files and some more features. Have a look to the generated Javadoc documentation for my other projects to see the results.

You can use this extensions in your project quite easy, I stripped down the dependencies to other stuff as far as possible.

## Annotation Processors
Most of the annotation processors here are meant to work with some of the libraries below.

### *[foundation-i18n-ap](https://tquadrat.github.io/foundation-i18n-ap)*
Generates resource bundles from annotated Strings; the annotations and some additional tools are defined in *[foundation-i18n](https://tquadrat.github.io/foundation-i18n)*

### *[foundation-config-ap](https://tquadrat.github.io/foundation-config-ap)*
Generates a JavaBean from a *Configuration Bean Specification* that is meant as central repository for the configuration values required by an application. For the details, refer to *[foundation-config](https://tquadrat.github.io/foundation-config)*, the library that defines the necessary annotations and the additional stuff needed.

## Gradle Plugins
Some helpers for the build process.

### *[gitpublisher](https://tquadrat.github.io/gitpublisher)*
For several reasons, I am using Subversion as the SCM for my projects. But as Git has been established as the standard for publishing projects, and GitHub and Bitbucket – currently the most often used platforms for publishing this kind of stuff – are using Git to keep the data, I decided that I need to make use of Git, too – at least for publishing my stuff.

The *Git Publisher* Gradle plugin is the answer: it publishes the files of a project to a (remote) Git repository like Github or BitBucket during the build process.

## Libraries
Most of my Java libraries are written as a Java module. When you use them within a project that does not use modules itself, you may have access to classes that are not meant to be visible outside the library itself. To give you some hints on what is part of the library's API and what is internal, I use the annotations from the library [@APIGuardian](https://github.com/apiguardian-team/apiguardian). It provides the annotation `@API` with the attribute `status` that has the value `STABLE` for all classes that can be used safely. This status is inherited to all public elements of a class, although I marked the `static final` members of utility classes individually in most cases. So keep your fingers off from stuff that is marked as `INTERNAL`, and use stuff marked as `MAINTAINED` or `EXPERIMENTAL` with care. Things marked as `DEPRECATED` will be removed at some time, so you should modify your code that it will not longer refer to those elements. 

### The *Foundation* Libraries
I collected a bunch of libraries under the header *Foundation*; a lot of that stuff is more than 20 years old now, always updated to the latest language version. The latest and most demanding change so far was to adoption of modularisation (JigSaw) when Java 9 came up.

#### *[foundation-base](https://tquadrat.github.io/foundation/base)*
The base for all the other stuff, although it is not much useful without the *[foundation-util](https://tquadrat.github.io/foundation-util)* library. But for some tools *foundation-util* is not necessary or just to big, so I separated some functionality into this library.

#### *[foundation-util](https://tquadrat.github.io/foundation-util)*
Add this library to make the most often used features available to your project.

#### *[foundation-testutil](https://tquadrat.github.io/foundation-testutil)*
Some tool classes that I use for my JUnit tests.

#### *[foundation-apbase](https://tquadrat.github.io/foundation-apbase)*
The base for my annotation processors (see [above](#annotation-processors)).

#### *[foundation-i18n](https://tquadrat.github.io/foundation-i18n)*
The definition of the annotations that allow *[foundation-i18n-ap](https://tquadrat.github.io/foundation-i18n-ap)* to generate resource bundles for the internationalisation of your application.

#### *[foundation-inifile](https://tquadrat.github.io/foundation-inifile)*
The API for the access to Windows-style configuration files (the so-called *INI*-Files).

#### *[foundation-value](https://tquadrat.github.io/foundation-value)*
The definition of "values" – numbers with dimensions.

#### *[foundation-xml](https://tquadrat.github.io/foundation-xml)*
Helpers for the handling of XML files, both generation and parsing.

#### *[foundation-svg](https://tquadrat.github.io/foundation-svg)*
Helpers for the generation of SVG files.

#### *[foundation-javacomposer](https://tquadrat.github.io/foundation-javacomposer)*
A library for the generation of Java source code; basically a fork of JavaPoet.

#### *[foundation-config](https://tquadrat.github.io/foundation-config)*
Defines a *Configuration Bean Specification* that allows the generation of a JavaBean that is meant as central repository for the configuration values required by an application (using *[foundation-config-ap](https://tquadrat.github.io/foundation-config-ap)*). It provides various means to load these configuration values (from a resource file, from the Preferences, from a Windows-style configuration file, from the command line) and it can be easily extended to other sources. 

#### *[foundation-fx](https://tquadrat.github.io/foundation-fx)*
A library with some utilities for the work with JavaFX, plus a few extensions to JavaFX, like an adapter for JavaFX's `StringConverter` to that I created for *Foundation* in `foundation-base`.

#### *[foundation-mgmt](https://tquadrat.github.io/foundation-mgmt)*
A library that allows the on-the-fly generation of a DynamicMBean, together with other JMX related stuff.

#### *[foundation-sql](https://tquadrat.github.io/foundation-sql)*
A library with database/JDBC related stuff.

#### *[foundation-jsonbuilder](https://tquadrat.github.io/foundation-jsonbuilder)*
A very simple and straight-forward JSON *building* tool, designed for a minimum footprint.

#### *[foundation-perflog](https://tquadrat.github.io/foundation-perflog)*
Defines a mean to easily integrate performance logging and monitoring to an application. The feature makes use of JMX to propagate the performance data. The project *[foundation-perflogremote](https://tquadrat.github.io/foundation-perflogremote)* provides the base for a remote client gathering the information provided by this library.

### Other Libraries
Not much here yet …