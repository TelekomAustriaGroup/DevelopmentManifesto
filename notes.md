# TAG Development Manifesto
This repository presents principles, guidelines and opinions on how to build software for Telekom Austria Group.

### Status of this document
- [ ] General Architecture: Microservice based, reactive, etc.
- [ ] Target Platform: Which platform should be used (e.g. JVM based, NodeJS, Ruby) for what kind of development (e.g. for throw away stuff use NodeJS because of speed and productivity, for "tracer" code and production relevant stuff use a JVM langugage etc)
- [ ]  Language Guideline: Best practices for Java, NodeJS, whatever (there are a lot of very comprehensive guidelines out there that we can reuse)
- [ ]  Deployment Approach: How to package and deliver applications (e.g. traditional AppServer based delivery vs. fat JARs vs. dockerized applications)
- [ ]  Logging/Debugging: How to handle logs, debugging and profiling
- [ ]  Testing related recommendations
- [ ]  Performance related stuff
- [ ]  Documentation
- [ ]  Versioning (it will be GIT but which git workflow to apply is the question)

## Architectural Remarks
This section describes how the overall architecture of TAG applications should look like. 

### Frontend Technologies

### Middleware Technologies

#### Microservice based SOA

#### Service Discovery

### Dataend Technologies

### Containerized Applications 

#### Docker
There is the *What is Docker?* statement from the [Docker Website](http://www.docker.io):

>Docker is an open platform for building, shipping and running distributed applications. It gives programmers, development teams and operations engineers the common toolbox they need to take advantage of the distributed and networked nature of modern applications.

If you are not familiar with Docker you should probably start by watching [this video](https://www.youtube.com/watch?v=Q5POuMHxW-0)

Here are the most important points why we use Docker

* provides you with the means to ship
  * packaged: your application is delivered as a *Docker Image* 
  * well defined: a single `Dockerfile` defines the structure and content of Docker images
  * isolated: 
  * re-locateable:
  * scalable:
* central authority (*Docker registry*) to locate and manage Docker images
  * Public or private registry (for TAG internal Docker images) 
* once you understand how Docker works, it is super easy to work with 


#### Kubernetes
## Target Platforms
This section contains recommendations on which development platform to use for certain engineering tasks.

### General Considerations
In general, use the right tool for the Job. There are tons of platforms out there that might seem to be a good choice for the particular problem you are trying to solve, however, we want you to build software either by relying on the _JVM_ or _NodeJS_. There will always be a tradeoff between productivity, performance, maturity and maintainability that has to be considered, but for the time being, we do not believe that NodeJS should be used in mission critical TAG software, for the following reasons *TODO: provide a reasonable list of arguments against NodeJS in production*:
* Debugging
* Tool support
* JavsScript: Weakly typed, dynamic type system --> Typescript as an alternative?

### Building Software for the JVM
In general, you should heavily rely on the _Spring Framework_ ecosystem. Besides [Core Spring](http://projects.spring.io/spring-framework/), there are many projects with the Spring ecosystem that can be leveraged to build elegant, scalable, maintainable and performant applications. However, building a Spring based application should always start from the _Spring Boot parent POM_:

```XML
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>${spring-boot.version}</version>
</parent>
```
With `${spring-boot.version}` set to the most recent GA version (never _never_ depend on a snapshot version!). At the time of writing, the most recent version of Spring Boot is `1.2.5.RELEASE`. If you wander what Spring Boot is, here is the short summary from the Spring website:

> Takes an opinionated view of building production-ready Spring applications. Spring Boot favors convention over configuration and is designed to get you up and running as quickly as possible.

Consult the [Spring Boot reference docs](http://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/) for details on Spring Boot.

As described above, the overall goal is to pack your application services into single fat JARs that have all their dependencies included and can be started via `java -jar MyShinyTagService.jar`

#### Build Process
* Follow the established [Maven directory structure](https://maven.apache.org/guides/introduction/introduction-to-the-standard-directory-layout.html)
* Use either [Maven](http://books.sonatype.com/mvnex-book/reference/public-book.html) or [Gradle](https://docs.gradle.org/current/userguide/userguide_single.html) to process, compile, test, package your software
* Stick to Maven best practices (most of them also apply to gradle builds). See [this resource](https://mestachs.wordpress.com/2012/05/17/maven-best-practices/) and [that resource](https://mestachs.wordpress.com/2012/05/17/maven-best-practices/) for more details.
* Consult the chapter on [Maven](http://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#using-boot-maven) and [Gradle](http://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#using-boot-gradle) from the Spring Boot reference

#### Configuration
* All application configuration has to be externalized.
* For local config files, use YAML 
* For applications that have non-trivial configuration management, use [Spring Boot Cloud Configuration Server](https://github.com/spring-cloud/spring-cloud-config) *TODO: check if there is an alternative to using git for storing properties*
* Use [Spring Profiles](http://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-profiles.html) to manage environments (dev, test, prod)

#### Logging
* Spring Boot is quite opinionated in terms of logging. You should follow those opinions
* Use logback for logging
* Apply some thought on the structure of your log messages. Eventually, log messages will end up in something like ElasticSearch for analytics and visualization, so make sure that the information in the log messages is easy to access and digest. For example, consider the following (taken from [this slideshare](http://www.slideshare.net/TrevParsons/logentries-dockerwebinarmar26-1)):
  * When the event occurred: the timestamp 
  * Structured Logs: JSON, KVP 
  * Context: if someone bought a book… what book was it
  * Unique Identiﬁers: request ID, User ID, Session ID, thread ID
  * Host Info: hostname & IP
  * Container Info: Image ID, Container ID, Process ID
* Think about the implications of your application running inside a Docker container (e.g. logs written to SDOUT, logstash, etc)
* For more details, consult the [Spring Boot logging documentation](http://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-logging.html)

#### Testing

#### Debugging

### Building Software for NodeJS

#### Build Process
* Use gulp for building NodeJS based applications

#### Testing

### TL;DR
Use NodeJS for building prototypes; Use a JVM based language for all other development tasks. In particular stick to either Java, Groovy or Scala on the JVM. 

## Language Guidelines

## Application Performance

## Documentation and Issue Tracking

## Versioning

### Constributors
[Oliver Moser](mailto: oliver.moser@telekomaustria.com)
