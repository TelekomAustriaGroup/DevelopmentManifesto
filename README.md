## TAG Development Manifesto
This document presents principles, guidelines and opinions on how to build idiomatic software for Telekom Austria Group. It is mainly based upon best practices and techniques that are known to have worked in the past. It does not provide detailed information on how to setup development environments, dev ops tool chains or CI pipelines. It rather provides an overview on technologies that should be leveraged when building proof of concept implementations as well as production relevant software systems for TAG.

## Sources that this Manifesto is based upon
The TAG development manifesto is heavily influenced by both the ideas and principles, as well as the style of the [Reactive Manifesto](http://www.reactivemanifesto.org). When referring to systems properties that are declared in the Reactive Manifesto - such as Responsiveness or Elasticity - we will not explicitly cite the Reactive Manifesto in this document. 

Other principles and best practices that are not based upon our own past experience are explicitly backed by the related source (i.e. URL).

## Building Idiomatic TAG Software 
The overall goal when building software systems for TAG is to deliver best-of-breed OTT solutions. Main characteristics of this OTT solution delivery process are *cost-effectiveness*, *time-to-value*, *customer satisfaction* as well as *sustainability*. Those rather high-level and business centric goals can be broken down into the technical considerations. Those considerations are discussed in the following.

### Immutable Infrastructure 
We rely on *reproducable* and *immutable* infrastructures to deliver TAG services. In short, immutable infrastructure is a new approach to change managemengt that is build upon "throw-away" server nodes or containers. In case of a problem or a planned upgrade, nodes are not fixed in place but are rather replaced entirely with an updated version. Both the outdated and updated service is based upon a certain base image that includes all software and tools that are required to provide the service. However, the updated version additionally includes the patch, feature implementation or whatever the reason was for the upgrade in the first place, as well as its version number is incremented. The main reason why TAG services are provided by an immutable infrastructure is reduced stress level, both on the side of the sofware engineers as well as the operations staff. Engineers can work with an infrastructure setup on their laptops that resembles the production setup besides the number of nodes for each service. Opertations staff on the other hand can be sure that no more hotfixes applied directly to a running server are forgotten to be added to their version control or setup scripts. And, rollbacks get super easy since everything can be referred to by a version number. 
In TAG, immutable infrastructure is based upon [Docker](http://www.docker.io) and [Kubernetes](http://www.kubernetes.io). *TODO describe II based on k8s and docker here*

For more information of immutabiltity in infrastructure, Docker and Kubernetes refer to [[1](#fowler1), [2](#computerweek), [3](#legos), [4](#blikis)]. 

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
<a href="http://chadfowler.com/blog/2013/06/23/immutable-deployments/" name="fowler1">[1] Chad Fowler: Trash Your Servers and Burn Your Code: Immutable Infrastructure and Disposable Components</a>
<a href="http://www.computerweekly.com/feature/Cloud-frozen-pizza-model-and-the-immutable-infrastructure" name="computerweekly">[2] Computer Weekly: Cloud, frozen pizza model and the immutable infrastructure</a>
<a href="http://techblog.netflix.com/2011/08/building-with-legos.html" name="legos">[3] Greg Orzell: Building with Legos</a>
<a href="http://blog.james-carr.org/2013/07/24/immutable-servers-with-packer-and-puppet/" name="pecker">[4] James Carr: Immutable Servers With Packer and Puppet</a>
<a href="http://kief.com/immutable-server.html" name="blikis">[5] Kief Morris: Immutable Server Blikis</a>


### Constributors
[Oliver Moser](mailto: oliver.moser@telekomaustria.com)
