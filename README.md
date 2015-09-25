## TAG Development Manifesto
This document presents principles, guidelines and opinions on how to build idiomatic software for Telekom Austria Group. It is mainly based upon best practices and techniques that are known to have worked in the past. It does not provide detailed information on how to setup development environments, dev ops tool chains or CI pipelines. It rather provides an overview on technologies that should be leveraged when building proof of concept implementations as well as production relevant software systems for TAG.

## Sources that this Manifesto is based upon
The TAG development manifesto is heavily influenced by both the ideas and principles, as well as the style of the [Reactive Manifesto](http://www.reactivemanifesto.org). When referring to systems properties that are declared in the Reactive Manifesto - such as Responsiveness or Elasticity - we will not explicitly cite the Reactive Manifesto in this document.

Other principles and best practices that are not based upon our own past experience are explicitly backed by the related source (i.e. URL).

<img src="http://kubernetes.io/img/warning.png" alt="WARNING"
     width="25" height="25">
      ***DISCLAIMER: THIS DOCUMENT IS WORK IN PROGRESS***<img src="http://kubernetes.io/img/warning.png" alt="WARNING"
     width="25" height="25">

## Building Idiomatic TAG Software
The overall goal when building software systems for TAG is to deliver best-of-breed OTT solutions. Main characteristics of this OTT solution delivery process are __cost-effectiveness__, __time-to-value__, __customer satisfaction__ as well as __sustainability__. Those rather high-level and business centric goals can be broken down into technical considerations. Those considerations are discussed in the following.

### Immutable Infrastructure
TAG relies on __reproducable__ and __immutable__ infrastructures to deliver services. In short, immutable infrastructure is a new approach to change management that is built upon "throw-away" server nodes or containers. In case of a problem or a planned upgrade, nodes are not fixed in place but are rather replaced entirely with an updated version. Both the outdated and updated service is based upon a certain base image that includes all software and tools that are required to provide the service. However, the updated version additionally includes the patch, feature implementation or whatever the reason was for the upgrade in the first place, as well as its version number is incremented. The main reason why TAG services are provided by an immutable infrastructure is reduced stress level, both on the side of the software engineers as well as the operations staff. Engineers can work with an infrastructure setup on their laptops that resembles the production setup besides the number of nodes for each service. Operations staff on the other hand can be sure that no more hotfixes applied directly to a running server are forgotten to be added to their version control or setup scripts. Scaling out your services is supported by the inherent reproducibility of immutable infrastructures. Therefore ops guys can scale out or scale in with a single command, or even automate this process, to achieve truly **elastic** software systems. Finally, and another very important aspect, rollbacks get super easy since everything can be referred to by a version number.

Looking at TAG, immutable infrastructure is built upon [Docker](http://www.docker.io) and [Kubernetes](http://www.kubernetes.io). In short, Docker is a tool stack for operating-system level virtualization that enables software containers for controlling applications on Linux based operating-systems. It is a lightweight alternative to hypervisor based virtualization, with the added value that it comes with a large ecosystem of tools, integrations as well as a [registry](http://hub.docker.com) for readily available containers. Thereby, spinning up MongoDB, for instance, is as easy as executing the following command: `docker run mongodb/mongodb`. With Docker, we get the tools to build and ship applications that are **isolated** (dockerized applications are isolated from each other and the docker host OS), **well-defined** (a single `Dockerfile` is required to describe the contents of your containerized application), **scalable** (want to spin up several instances of your application? No problem!) and **relocatable** (you get full location transparency with Docker). Thereby, Docker provides us with the means for service based immutability (start, stop, update, restart and trash your containers as you like). However, the holistic management of your immutable infrastructure can get tedious pretty quickly. Docker itself comes with a tool  ([`docker-compose`](https://docs.docker.com/compose/)) that enables you to describe and manage multi-container applications. Using docker-compose, you can spin up your whole infrastructure with a single command. Although, what is required, ultimately, is a tool stack to manage a cluster of Docker containers. [Docker Swarm](https://docs.docker.com/swarm/) is a Docker native scheduling backend that enables you to represent a pool of Docker hosts as a single virtual host. However, for the time being, it is not considered production ready and lacks some features that TAG requires. Google's Kubernetes (k8s), on the other hand, almost feature complete from TAG requirements perspective, and is considered stable enough for production deployments. The basic concepts in k8s are **pods**, **services** and **replication controllers**. A pod is simply a set of one or more co-located (located on the same vhost) Docker containers that have shared access to resources. A service represents a logical access point for one or more pods by providing a stable IP address and DNS name (similar to a VIP address on a load balancer). Finally, the replication controller makes sure that a specified number of pods are up & running for a given service. Similar to tools like [supervisord](http://www.supervisord), it handles automatic restarts upon failure and schedules new pods in case a node goes down. Additionally, it can be used to dynamically scale out or scale in on the number of pods (hence supporting system elasticity).

For more information of immutability in infrastructure, Docker and Kubernetes refer to [[1](#fowler1), [2](#computerweek), [3](#legos), [4](#pecker), [5](#blikis), [6](#cw-k8s), [7](#docker-book)].

### Microservice Architecture (MSA)
**TODO work in progress**

For more information on Microservices and Spring Boot, see [[8](#fowler-msa), [9](#spring-boot-docs)]
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
- <a href="http://chadfowler.com/blog/2013/06/23/immutable-deployments/" name="fowler1">[1] Chad Fowler: Trash Your Servers and Burn Your Code: Immutable Infrastructure and Disposable Components</a>
- <a href="http://www.computerweekly.com/feature/Cloud-frozen-pizza-model-and-the-immutable-infrastructure" name="computerweekly">[2] Computer Weekly: Cloud, frozen pizza model and the immutable infrastructure</a>
- <a href="http://techblog.netflix.com/2011/08/building-with-legos.html" name="legos">[3] Greg Orzell: Building with Legos</a>
- <a href="http://blog.james-carr.org/2013/07/24/immutable-servers-with-packer-and-puppet/" name="pecker">[4] James Carr: Immutable Servers With Packer and Puppet</a>
- <a href="http://kief.com/immutable-server.html" name="blikis">[5] Kief Morris: Immutable Server Blikis</a>
- <a name="cw-k8s" href="http://www.computerweekly.com/feature/Demystifying-Kubernetes-the-tool-to-manage-Google-scale-workloads-in-the-cloud">[6] Computer Weekly: Demystifying Kubernetes: the tool to manage Google-scale workloads in the cloud</a>
- <a name="docker-book" href="http://www.amazon.com/Docker-Book-Containerization-new-virtualization-ebook/dp/B00LRROTI4/ref=sr_1_2?ie=UTF8&qid=1443165177&sr=8-2&keywords=docker">[7] The Docker Book: Containerization is the new virtualization</a>
- <a name="msa-fowler" href="http://martinfowler.com/articles/microservices.html">[8] Martin Fowler, James Lewis: Microservices</a>
- <a name="spring-boot-docs" href="http://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/">[9] Spring Boot Reference Documentation</a>

### Contributors
[Oliver Moser](mailto: oliver.moser@telekomaustria.com)
