## TAG Development Manifesto
This document presents principles, guidelines and opinions on how to build idiomatic software for Telekom Austria Group. It is mainly based upon best practices and techniques that are known to have worked in the past. It does not provide detailed information on how to setup development environments, dev ops tool chains or CI pipelines. It rather provides an overview on technologies that should be leveraged when building proof of concept implementations as well as production relevant software systems for TAG.

## Sources that this Manifesto is based upon
The TAG development manifesto is heavily influenced by both the ideas and principles, as well as the style of the [Reactive Manifesto](http://www.reactivemanifesto.org). When referring to systems properties that are declared in the Reactive Manifesto - such as Responsiveness or Elasticity - we will not explicitly cite the Reactive Manifesto in this document. 

Other principles and best practices that are not based upon our own past experience are explicitly backed by the related source (i.e. URL).

## Building Idiomatic TAG Software 
The overall goal when building software systems for TAG is to deliver best-of-breed OTT solutions. Main characteristics of this OTT solution delivery process are *cost-effectiveness*, *time-to-value*, *customer satisfaction* as well as *sustainability*. Those rather high-level and business centric goals can be broken down into the following technical considerations. Cost-effectiveness and time-to-value can both be achieved by relying on *reproducable* software components and *immutable* infrastructures [1](#fowler1). 

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

### References
<a href="http://chadfowler.com/blog/2013/06/23/immutable-deployments/" name="fowler1">Chad Fowler: Trash Your Servers and Burn Your Code: Immutable Infrastructure and Disposable Components</a>
### Constributors
[Oliver Moser](mailto: oliver.moser@telekomaustria.com)
