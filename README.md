## TAG Development Manifesto
This document presents principles, guidelines and opinions on how to build idiomatic software for Telekom Austria Group. It is mainly based upon best practices and techniques that are known to have worked in the past. It does not provide detailed information on how to setup development environments, dev ops tool chains or CI pipelines, but rather provides an overview on technologies that should be leveraged when building proof of concept implementations as well as production relevant software systems for TAG.

## Sources that this Manifesto is based upon
The TAG development manifesto is heavily influenced by both the ideas and principles, as well as the style of the [Reactive Manifesto](http://www.reactivemanifesto.org). When referring to systems properties that are declared in the Reactive Manifesto - such as Responsiveness or Elasticity - we will not explicitly cite the Reactive Manifesto in this document. 

Other principles and best practices that are not based upon our own past experience are explicitly backed by the related source (i.e. URL).


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


### Constributors
[Oliver Moser](mailto: oliver.moser@telekomaustria.com)
