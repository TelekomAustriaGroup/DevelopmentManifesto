# TAG Development Manifesto
This repository presents principles, guidelines and opinions on how to build software for Telekom Austria Group.

### Status of this document

- [ ] Target Platform: Which platform should be used (e.g. JVM based, NodeJS, Ruby) for what kind of development (e.g. for throw away stuff use NodeJS because of speed and productivity, for "tracer" code and production relevant stuff use a JVM langugage etc)
- [ ]  Language Guideline: Best practices for Java, NodeJS, whatever (there are a lot of very comprehensive guidelines out there that we can reuse)
- [ ]  Deployment Approach: How to package and deliver applications (e.g. traditional AppServer based delivery vs. fat JARs vs. dockerized applications)
- [ ]  Logging/Debugging: How to handle logs, debugging and profiling
- [ ]  Testing related recommendations
- [ ]  Performance related stuff
- [ ]  Documentation
- [ ]  Versioning (it will be GIT but which git workflow to apply is the question)

## Target Platforms
This section contains recommendations on which development platform to use for certain engineering tasks.

### General Considerations
In general, use the right tool for the Job. There are tons of platforms out there that might seem to be a good choice for the particular problem you are trying to solve, however, we want you to build software either by relying on the _JVM_ or _NodeJS_. There will always be a tradeoff between productivity, performance, maturity and maintainability that has to be considered, but for the time being, we do not believe that NodeJS should be used in mission critical TAG software, for the following reasons:
* Debugging
* Tool support
* JavsScript: Weakly typed, dynamic type system --> Typescript as an alternative?

### Building Software for the JVM

#### Build Process
* Follow the established [Maven directory structure](https://maven.apache.org/guides/introduction/introduction-to-the-standard-directory-layout.html)
* Use either [Maven](http://books.sonatype.com/mvnex-book/reference/public-book.html) or [Gradle](https://docs.gradle.org/current/userguide/userguide_single.html) to process, compile, test, package your software
* Stick to Maven best practices (most of them also apply to gradle builds). See [this resource](https://mestachs.wordpress.com/2012/05/17/maven-best-practices/) and [that resource](https://mestachs.wordpress.com/2012/05/17/maven-best-practices/) for more details.



#### Testing

### Building Software for NodeJS

#### Build Process
* Use gulp for building NodeJS based applications

#### Testing

### TL;DR
Use NodeJS for building prototypes; Use a JVM based language for all other development tasks. In particular stick to either Java, Groovy or Scala on the JVM. 

### Constributors
[Oliver Moser](mailto: oliver.moser@telekomaustria.com)
