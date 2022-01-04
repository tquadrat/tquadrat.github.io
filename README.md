# tquadrat.github.io

## Artifacts Repository
You can pull the artifacts from my projects from this repository
- [tquadrat's Archiva Repository](http://tquadrat.org/archiva/)

## My Projects
I do this stuff only for own pleasure. If you like some of this – have fun! And if you have questions, please feel free to send me an email (to <tquadrat.do@gmail.com>) or you can connect me on Telegram (at @tquadrat_do).

I write code mainly in Java, preferred using the latest language version (as of now – 2022-01-04 – this is Java 17) even with the preview features switched on.

To build the code, I am using Gradle (switched to it recently, previously I used Maven).

I am a big friend of documentation, and in my opinion, most documentation should be placed as close to the code as possible. Therefor it is really helpful that I am also a big fan of JavaDoc (for Java) and related tools (for other languages). So at least for the tools and libraries, most if not all information you need to use them can be found in the JavaDoc reference – as said as close to the code as possible. General information is placed to the overview, in exceptions also in the package overview documents. If you miss something (or the documentation raises more questions than providing answers), please contact me.

By the way, the JavaDoc provides links to the sources in most cases.

### Applications
Not yet much stuff here, but I am working on publishing it soon – after I move the build to Gradle and the code to Java 17.

### Tools
Same here …

### Libraries
Most of my libraries are written as a module. When you use them within a project that does not use modules itself, you may have access to classes that are not meant to be visible outside the library itself. To give you some hints on what is part of the API and what is internal, I use the library [@APIGuardian](https://github.com/apiguardian-team/apiguardian). It provides the annotation `@API` with the attribute `status` that has the value `STABLE` for all classes that can be used safely. This status is inherited to all public elements of a class, although I marked the `static final` members of utility classes individually in most cases. So keep your fingers off stuff that is marked as `DEPRECATED` or `INTERNAL`, and use stuff marked as `MAINTAINED` or `EXPERIMENTAL` with care.

#### The *Foundation* Libraries
I collected a bunch of libraries under the header *Foundation*; a lot of that stuff is 20 years old now, always updated to the latest language version. The latest and most demanding change was to adoption of modularisation (JigSaw).

##### *[foundation-base](https://tquadrat.github.io/foundation-base)*
The base for all the other stuff, althoug it is not much useful without the *[foundation-util](https://tquadrat.github.io/foundation-util)* library. But for some tools this is not necessary or just to big, so I separated some functionality into this library.

##### *[foundation-util](https://tquadrat.github.io/foundation-util)*
Add this library to make the most often used features available to your project.

##### *[foundation-testutil](https://tquadrat.github.io/foundation-testutil)*
Some tool classes that I use for my JUnit tests.

### Other Stuff
… stay tuned!
