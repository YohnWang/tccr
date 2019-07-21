# Cloud Computing: Issues and Challenges

> Abstract— Many believe that Cloud will reshape the entire ICT industry as a revolution. In this paper, we aim to pinpoint the challenges and issues of Cloud computing. We first discuss two related computing paradigms - Service-Oriented Computing and Grid computing, and their relationships with Cloud computing We then identify several challenges from the Cloud computing adoption perspective. Last, we will highlight the Cloud interoperability issue that deserves substantial further research and development.

摘要 - 许多人认为，云计算将重塑整个ICT行业的革命。在本文中，我们旨在确定云计算的挑战和问题。我们首先讨论两种相关的计算范例 - 面向服务的计算和网格计算，以及它们与云计算的关系然后我们从云计算采用的角度确定了几个挑战。最后，我们将重点介绍值得进行大量进一步研究和开发的云互操作性问题。

> Keywords: Cloud computing; Servcice-Oriented Computing; Distributed Comptuing; Web Services

关键词：云计算;面向服务的计算;分布式计算;Web服务

## I. INTRODUCTION

> Cloud computing has recently emerged as a buzz word in the distributed computing community. Many believe that Cloud is going to reshape the IT industry as a revolution. So, what is Cloud Computing? How is it different from service-oriented computing and Grid computing? What are those general challenges and issues for both cloud providers and consumers?
> In answering these questions, we aim to define key research issues and articulate future research challenges and directions for cloud computing. To do this, we take an outside-in approach to organize this paper. We first examine a number of cloud applications that exhibit several key characteristics. We then discuss the relationship between Cloud computing and Service-Oriented Computing (SOC) and the relationship between Cloud and Grid computing (i.e. High-Performance Computing). We compare these three computing paradigms and draw attention to how they will benefit each other in a coexistent manner. Next, we discuss service models and deployment models of cloud computing. We elaborate service model and deployment model of a cloud, which leads to the discussion of several data-related issues and challenges such as multi-tenancy, security, and so forth. Finally, we discuss interoperability and standardization issues.

云计算最近成为分布式计算社区的热门话题。许多人认为，云计算将重塑IT行业的革命。那么，什么是云计算？它与面向服务的计算和网格计算有何不同？云提供商和消费者的一般挑战和问题是什么？
在回答这些问题时，我们的目标是定义关键的研究问题，并阐明未来云计算的研究挑战和方向。为此，我们采用从外到内的方法来组织本文。我们首先研究了许多具有几个关键特性的云应用程序。然后，我们讨论云计算和面向服务的计算（SOC）之间的关系以及云和网格计算（即高性能计算）之间的关系。我们比较这三种计算范式，并提请注意它们如何以共存的方式相互受益。接下来，我们将讨论云计算的服务模型和部署模型。我们详细阐述了云的服务模型和部署模型，从而讨论了多个与数据相关的问题和挑战，如多租户，安全性等。最后，我们讨论互操作性和标准化问题。

## II. CLOUD: OVERVIEW

> **A. Definition**
>
> What is Cloud Computing? Although many formal definitions have been proposed in both academia and industry, the one provided by U.S. NIST (National Institute of Standards and Technology) [1] appears to include key common elements widely used in the Cloud Computing community:
>
> *Cloud computing is a model for enabling convenient, ondemand network access to a shared pool of configurable computing resources (e.g., networks, servers, storage, applications, and services) that can be rapidly provisioned and released with minimal management effort or service provider interaction [1].*
>
> This definition includes cloud architectures, security, and deployment strategies. In particular, five essential elements of cloud computing are clearly articulated:
>
> On-demand self-service: A consumer with an instantaneous need at a particular timeslot can avail computing resources (such as CPU time, network storage, software use, and so forth) in an automatic (i.e. convenient, self-serve) fashion without resorting to human interactions with providers of these resources.
>
> Broad network access: These computing resources are delivered over the network (e.g. Internet) and used by various client applications with heterogeneous platforms (such as mobile phones, laptops, and PDAs) situated at a consumer's site.
>
> Resource pooling. A cloud service provider’s computing resources are 'pooled' together in an effort to serve multiple consumers using either the multi-tenancy or the virtualization model, "with different physical and virtual resources dynamically assigned and reassigned according to consumer demand" [1]. The motivation for setting up such a pool-based computing paradigm lies in two important factors: economies of scale and specialization. The result of a pool-based model is that physical computing resources become 'invisible' to consumers, who in general do not have control or knowledge over the location, formation, and originalities of these resources (e.g. database, CPU, etc.) . For example, consumers are not able to tell where their data is going to be stored in the Cloud.
>
> Rapid elasticity. For consumers, computing resources become immediate rather than persistent: there are no up-front commitment and contract as they can use them to scale up whenever they want, and release them once they finish to scale down. Moreover, resources provisioning appears to be infinite to them, the consumption can rapidly rise in order to meet peak requirement at any time.
>
> Measured Service. Although computing resources are pooled and shared by multiple consumers (i.e. multi-tenancy), the cloud infrastructure is able to use appropriate mechanisms to measure the usage of these resources for each individual consumer through its metering capabilities.

**A.定义**

什么是云计算？尽管学术界和工业界都提出了许多正式定义，但美国国家标准与技术研究院（国家标准与技术研究院）[1]提供的定义似乎包括云计算社区广泛使用的关键共同要素：

云计算是一种模型，用于实现对可配置计算资源（例如，网络，服务器，存储，应用程序和服务）的共享池的方便的按需网络访问，这些资源可以通过最少的管理工作或服务提供商交互进行快速配置和发布[1]。

该定义包括云架构，安全性和部署策略。特别是，云计算的五个基本要素被清楚地表达出来：

按需自助服务：在特定时间段具有即时需求的消费者可以通过自动（即方便，自助服务）方式利用计算资源（例如CPU时间，网络存储，软件使用等），而无需诉诸与这些资源的提供者的人际互动。

广泛的网络访问：这些计算资源通过网络（例如，因特网）传送，并由位于消费者站点的异构平台（例如移动电话，膝上型电脑和PDA）的各种客户端应用程序使用。

资源池：云服务提供商的计算资源被“汇集”在一起，以便使用多租户或虚拟化模型为多个消费者服务，“根据消费者需求动态分配和重新分配不同的物理和虚拟资源”[1]。建立这种基于池的计算范式的动机在于两个重要因素：规模经济和专业化。基于池的模型的结果是物理计算资源对于消费者变得“不可见”，消费者通常不具有对这些资源（例如，数据库，CPU等）的位置，形成和原始性的控制或知识。例如，消费者无法分辨他们的数据将存储在云中的哪个位置。

快速弹性：对于消费者而言，计算资源变得直接而非持久：没有前期承诺和合同，因为他们可以随时使用它们进行扩展，并在缩小规模后释放它们。此外，资源供应对他们来说似乎是无限的，消费可以迅速上升，以便随时满足高峰需求。

测量服务。虽然计算资源由多个消费者汇集和共享（即多租户），但是云基础设施能够使用适当的机制通过其计量能力来测量每个个体消费者对这些资源的使用。

> **B. Servcice Model**
>
> In addition to these five essential characteristics, the cloud community has extensively used the following three service models to categories the cloud services:
>
> Software as a Service (SaaS). Cloud consumers release their applications on a hosting environment, which can be accessed through networks from various clients (e.g. web browser, PDA, etc.) by application users. Cloud consumers do not have control over the Cloud infrastructure that often employs a multi-tenancy system architecture, namely, different cloud consumers' applications are organized in a single logical environment on the SaaS cloud to achieve economies of scale and optimization in terms of speed, security, availability, disaster recovery, and maintenance. Examples of SaaS include SalesForce.com, Google Mail, Google Docs, and so forth.
>
> Platform as a Service (PaaS). PaaS is a development platform supporting the full "Software Lifecycle" which allows cloud consumers to develop cloud services and applications (e.g. SaaS) directly on the PaaS cloud. Hence the difference between SaaS and PaaS is that SaaS only hosts completed cloud applications whereas PaaS offers a development platform that hosts both completed and in-progress cloud applications. This requires PaaS, in addition to supporting application hosting environment, to possess development infrastructure including programming environment, tools, configuration management, and so forth. An example of PaaS is Google AppEngine.
>
> Infrastructure as a Service (IaaS). Cloud consumers directly use IT infrastructures (processing, storage, networks, and other fundamental computing resources) provided in the IaaS cloud. Virtualization is extensively used in IaaS cloud in order to integrate/decompose physical resources in an ad-hoc manner to meet growing or shrinking resource demand from cloud consumers. The basic strategy of virtualization is to set up independent virtual machines (VM) that are isolated from both the underlying hardware and other VMs. Notice that this strategy is different from the multi-tenancy model, which aims to transform the application software architecture so that multiple instances (from multiple cloud consumers) can run on a single application (i.e. the same logic machine). An example of IaaS is Amazon's EC2.
>
> Data storage as a Service (DaaS). The delivery of virtualized storage on demand becomes a separate Cloud service - data storage service. Notice that DaaS could be seen as a special type IaaS. The motivation is that on-premise enterprise database systems are often tied in a prohibitive upfront cost in dedicated server, software license, post-delivery services, and in-house IT maintenance. DaaS allows consumers to pay for what they are actually using rather than the site license for the entire database. In addition to traditional storage interfaces such as RDBMS and file systems, some DaaS offerings provide table-style abstractions that are designed to scale out to store and retrieve a huge amount of data within a very compressed timeframe, often too large, too expensive or too slow for most commercial RDBMS to cope with. Examples of this kind of DaaS include Amazon S3, Google BigTable, and Apache HBase, etc.
>
> 

**B.服务模式**

除了这五个基本特征外，云社区还广泛使用以下三种服务模型对云服务进行分类：

软件即服务（SaaS）。云消费者在托管环境中发布他们的应用程序，托管环境可以由应用程序用户通过来自各种客户端（例如网络浏览器，PDA等）的网络访问。云消费者无法控制通常采用多租户系统架构的云基础架构，即不同的云消费者应用程序组织在SaaS云上的单一逻辑环境中，以实现规模经济和速度优化，安全性，可用性，灾难恢复和维护。SaaS的示例包括SalesForce.com，Google Mail，Google Docs等。

平台即服务（PaaS）。PaaS是一个支持完整“软件生命周期”的开发平台，允许云消费者直接在PaaS云上开发云服务和应用程序（例如SaaS）。因此，SaaS和PaaS之间的区别在于SaaS仅托管已完成的云应用程序，而PaaS提供了一个托管已完成和正在进行的云应用程序的开发平台。这要求PaaS除支持应用程序托管环境外，还拥有包括编程环境，工具，配置管理等在内的开发基础架构。PaaS的一个例子是Google AppEngine。

基础架构即服务（IaaS）。云消费者直接使用IaaS云中提供的IT基础架构（处理，存储，网络和其他基础计算资源）。虚拟化广泛用于IaaS云，以便以临时方式集成/分解物理资源，以满足云消费者不断增长或缩减的资源需求。虚拟化的基本策略是建立与底层硬件和其他VM隔离的独立虚拟机（VM）。请注意，此策略与多租户模型不同，后者旨在转换应用程序软件体系结构，以便多个实例（来自多个云消费者）可以在单个应用程序（即同一逻辑机器）上运行。IaaS的一个例子是亚马逊的EC2。

数据存储即服务（DaaS）。按需提供虚拟化存储成为单独的云服务 - 数据存储服务。请注意，DaaS可以被视为特殊类型的IaaS。其动机是，内部部署的企业数据库系统通常在专用服务器，软件许可证，交付后服务和内部IT维护中处于禁止的前期成本中。DaaS允许消费者为实际使用的内容而不是整个数据库的站点许可付费。除了传统的存储接口（如RDBMS和文件系统）之外，一些DaaS产品还提供表格式抽象，旨在扩展以在非常压缩的时间范围内存储和检索大量数据，通常过大，过于昂贵或过于庞大。对于大多数商业RDBMS来说，应对的速度很慢。此类DaaS的示例包括Amazon S3，Google BigTable和Apache HBase等。

> **C. Deployment Model**
>
> More recently, four cloud deployment models have been defined in the Cloud community:
>
> Private cloud. The cloud infrastructure is operated solely within a single organization, and managed by the organization or a third party regardless whether it is located premise or off premise. The motivation to setup a private cloud within an organization has several aspects. First, to maximize and optimize the utilization of existing in-house resources. Second, security concerns including data privacy and trust also make Private Cloud an option for many firms. Third, data transfer cost [2] from local IT infrastructure to a Public Cloud is still rather considerable. Fourth, organizations always require full control over mission-critical activities that reside behind their firewalls. Last, academics often build private cloud for research and teaching purposes.
>
> Community cloud. Several organizations jointly construct and share the same cloud infrastructure as well as policies, requirements, values, and concerns. The cloud community forms into a degree of economic scalability and democratic equilibrium. The cloud infrastructure could be hosted by a third-party vendor or within one of the organizations in the community.
>
> Public cloud. This is the dominant form of current Cloud computing deployment model. The public cloud is used by the general public cloud consumers and the cloud service provider has the full ownership of the public cloud with its own policy, value, and profit, costing, and charging model. Many popular cloud services are public clouds including Amazon EC2, S3, Google AppEngine, and Force.com.
>
> Hybrid cloud. The cloud infrastructure is a combination of two or more clouds (private, community, or public) that remain unique entities but are bound together by standardized or proprietary technology that enables data and application portability (e.g., cloud bursting for load-balancing between clouds). Organizations use the hybrid cloud model in order to optimize their resources to increase their core competencies by margining out peripheral business functions onto the cloud while controlling core activities on-premise through private cloud. Hybrid cloud has raised the issues of standardization and cloud interoperability that will be discussed in later sections.
>
> Interestingly, Amazon Web Services (AWS) has recently rolled out a new type of deployment model - Virtual Private Cloud (VPC), a secure and seamless bridge between an organization’s existing IT infrastructure and the Amazon public cloud. This is positioned as a mixture between Private Cloud and Public Cloud. It is Public because it still uses computing resources pooled by Amazon for the general public. However, it is virtually private for two reasons. Firstly, the connection between IT legacy and the cloud is secured through a virtual private network, thereby having the security advantage of Private Cloud. In fact, all corporate security policies still apply to resources on the cloud even though it is on the Public Cloud. Second, AWS will dedicate a set of 'isolated' resources to the VPC. However, this does not mean users have to pay these isolated resources up-front. Users still enjoy "pay-per-use" on these isolated resources. VPC represents a perfect balance between control (Private Cloud) and flexibility (Public Cloud).
>
> Notice that the service model is orthogonal to the deployment model. For example, an SaaS could provisioned on a Public cloud or Private cloud.

最近，Cloud社区中定义了四种云部署模型：

私有云。云基础架构仅在单个组织内运行，由组织或第三方管理，无论其位于局部还是外部。在组织内设置私有云的动机有几个方面。首先，最大化和优化现有内部资源的利用。其次，包括数据隐私和信任在内的安全问题也使私有云成为许多公司的选择。第三，从本地IT基础设施到公共云的数据传输成本[2]仍然相当可观。第四，组织总是要求完全控制驻留在防火墙后面的关键任务活动。最后，学者们经常为研究和教学目的构建私有云。

社区云。一些组织共同构建和共享相同的云基础架构以及策略，要求，价值和关注点。云社区形成一定程度的经济可扩展性和民主均衡。云基础架构可以由第三方供应商托管，也可以在社区中的一个组织内托管。

公共云。这是当前云计算部署模型的主要形式。公共云由普通公共云消费者使用，云服务提供商拥有公共云的完全所有权，具有自己的策略，价值和利润，成本计算和计费模型。许多流行的云服务都是公共云，包括Amazon EC2，S3，Google AppEngine和Force.com。

混合云。云基础架构是两个或多个云（私有云，社区云或公共云）的组合，这些云仍然是独特的实体，但通过标准化或专有技术绑定在一起，从而实现数据和应用程序的可移植性（例如，用于云之间负载平衡的云爆发）。组织使用混合云模型来优化其资源，通过将外围业务功能保留到云上，同时通过私有云控制内部部署的核心活动来增加其核心竞争力。混合云提出了标准化和云互操作性的问题，将在后面的章节中讨论。

有趣的是，亚马逊网络服务（AWS）最近推出了一种新型部署模式 - 虚拟私有云（VPC），它是组织现有IT基础架构与亚马逊公共云之间的安全无缝桥梁。这是私有云和公共云之间的混合体。它是公开的，因为它仍然使用亚马逊汇集的计算资源给公众。然而，由于两个原因，它几乎是私人的。首先，IT遗留和云之间的连接通过虚拟专用网络得到保护，从而具有私有云的安全优势。事实上，即使是在公共云上，所有企业安全策略仍然适用于云上的资源。其次，AWS将为VPC提供一组“隔离”资源。但是，这并不意味着用户必须预先支付这些孤立的资源。用户仍然喜欢这些孤立资源的“按使用付费”。VPC代表了控制（私有云）和灵活性（公共云）之间的完美平衡。

请注意，服务模型与部署模型正交。例如，可以在公共云或私有云上配置SaaS。

## III. CLOUD, SOC, AND GRID

> In this section, we identify relationships between Cloud Computing, Service-Oriented Computing (SOC) and Grid Computing.
>
> **A. Cloud and Service-Oriented Computing**
>
> The encapsulation, componentization, decentralization, and integration capability provided by SOC are substantial: they provide both architectural principles and software specifications to connect computers and devices using standardized protocols across the Internet [3]. In fact, the notion of Cloud is more or less based on the evolving development on SOC, in particular the SaaS service model.
>
> Advances in SOC can benefit Cloud Computing in several ways.
>
> Service Description for Cloud Services. Web Services Description Language (WSDL) and the REST protocol are two widely used interface languages to describe Web services. They have been utilized to describe Cloud API specification.
>
> Service Discovery for Cloud Services. Various service discovery models can be leveraged for cloud resource discovery, selection and service-level agreement verification.
>
> Service Composition for Cloud Service. Since Web services are born to compose business applications, a great deal of research in this area can be leveraged for cloud services integration, collaboration, composition.
>
> Service Management for Cloud Service. Research and practices in SOA governance and services management can be adapted and reused in the cloud infrastructure management.
>
> 

在本节中，我们将确定云计算，面向服务的计算（SOC）和网格计算之间的关系。

**A.云和面向服务的计算**

SOC提供的封装，组件化，分散和集成功能非常重要：它们提供了体系结构原则和软件规范，以便通过Internet使用标准化协议连接计算机和设备[3]。实际上，云的概念或多或少基于SOC的不断发展，特别是SaaS服务模型。

SOC的进步可以通过多种方式使云计算受益。

云服务的服务描述。Web服务描述语言（WSDL）和REST协议是两种广泛使用的接口语言来描述Web服务。它们已被用于描述Cloud API规范。

云服务的服务发现。可以利用各种服务发现模型进行云资源发现，选择和服务级别协议验证。

Cloud Service的服务组合。由于Web服务是由组成业务应用程序而诞生的，因此可以利用该领域的大量研究来实现云服务集成，协作和组合。

云服务的服务管理。SOA治理和服务管理的研究和实践可以在云基础架构管理中进行调整和重用。

> On the other hand, we need to consider what is missing in SOC, especially from the perspective of small and medium enterprises? SOC represents a high level of abstraction from the integration and business process perspective. However, SOC does not provide a practical computational models for running services. For example, how to run my services with minimum cost? How to scale in/out my applications built on top of Service-Oriented Architecture. These computational details have to be dealt with in a project-specific and ad-hoc manner, which burdens the workload for SOC developers and IT department in SMEs. In addition, how to include services at different levels into a coherent organizational entity is an open question in SOC. For example, how to maximize the utilization of my IT services in order to support my business services? Therefore, we believe Cloud computing can benefit Service-Oriented Computing research in several important ways.

另一方面，我们需要考虑SOC中缺少什么，特别是从中小企业的角度来看？SOC代表了集成和业务流程视角的高级抽象。但是，SOC没有提供运行服务的实用计算模型。例如，如何以最低成本运行我的服务？如何扩展/扩展基于面向服务的体系结构构建的应用程序。这些计算细节必须以项目特定和临时方式处理，这会增加SOC开发人员和中小企业IT部门的工作量。此外，如何将不同层次的服务纳入一个连贯的组织实体是SOC中的一个悬而未决的问题。例如，如何最大限度地利用我的IT服务以支持我的业务服务？因此，我们认为云计算可以通过几种重要方式使面向服务的计算研究受益。

> Cloud for Web Service Development. Cloud can host service-oriented development under the PaaS service deploy model. SOC development often requires distributed computing resources that are difficult to obtain for SMEs. For example, Google's AppEngine (the platform, its SDK, and client IDE) provides a full-fledged development platform in which developers can develop and deploy Java Web services to build their applications. In addition, the Yahoo Pipe platform illustrates the potential that Cloud can serve as the design-time and run-time for service Mashups and Composition.
>
> Cloud for Web Service Testing. Web services developers could tap into infinite computing resources in a Public Cloud to simulate real-world automated machine requests and network flows as a means of load testing and stress testing for services. The ability and cost to simulate network traffic for WS testing has been an inhibitor to overall Web reliability. The low cost and accessibility of the Cloud’s extremely large computing resources provides the ability to replicate real world usage of these systems by geographically distributed users, executing wide varieties of user scenarios, at scales previously unattainable in traditional testing environments.
>
> Cloud for Web Service Deployment. Using IaaS, Web services deployment can be streamlined. For example, under the Amazon EC2 setting, service deployers can use the Amazon Machine Image (AMI) to distribute their offerings. When requests are present, a service deployment image will be loaded into a specified virtual machine to serve the client requests. Stateful information produced during service interactions can be also kept persistent onto the AMI when Web services are resumed from the suspended mode (e.g. from a long-last transaction).
>
> Cloud for Service Process Enactment. The integration and composition of services become frequent problems and their solutions can be packaged as services deployed in the cloud environment. Therefore, a prevailing approach is to exploit the power of crowd (service users) to allow the re-use of solutions that are ready-to-use with minor configuration and composition patterns using various algorithms (e.g. Case-Based Reasoning).
>
> The integration question of Cloud and SOA/SOC is an interesting one. Are they at the same technical/business level? Do they aim to achieve the same goal? Can they be employed at the same time? If so, how? These are research challenges that can be addressed with the further development and adoption of cloud computing.

用于Web服务开发的云。云可以在PaaS服务部署模型下托管面向服务的开发。SOC开发通常需要为中小企业难以获得的分布式计算资源。例如，Google的AppEngine（平台，其SDK和客户端IDE）提供了一个成熟的开发平台，开发人员可以在其中开发和部署Java Web服务来构建他们的应用程序。此外，Yahoo Pipe平台还说明了Cloud可以作为服务Mashups和Composition的设计时和运行时的潜力。

用于Web服务测试的云。Web服务开发人员可以利用公共云中的无限计算资源来模拟真实的自动化机器请求和网络流，作为负载测试和服务压力测试的一种手段。模拟WS测试的网络流量的能力和成本一直是整体Web可靠性的抑制因素。云的极大计算资源的低成本和可访问性提供了复制地理分布式用户对这些系统的实际使用的能力，执行各种各样的用户场景，这在以前在传统测试环境中无法实现的规模。

用于Web服务部署的云。使用IaaS，可以简化Web服务部署。例如，在Amazon EC2设置下，服务部署者可以使用Amazon Machine Image（AMI）来分发他们的产品。当存在请求时，服务部署映像将加载到指定的虚拟机中以提供客户端请求。当从暂停模式（例如，从最后一次交易）恢复Web服务时，在服务交互期间产生的有状态信息也可以保持在AMI上。

服务流程制定的云。服务的集成和组合成为常见问题，其解决方案可以打包为部署在云环境中的服务。因此，流行的方法是利用人群（服务用户）的力量来允许使用各种算法（例如，基于案例的推理）重复使用具有较小配置和组成模式的即用型解决方案。

云和SOA / SOC的集成问题是一个有趣的问题。他们是否处于相同的技术/业务水平？他们的目标是实现同一目标吗？他们可以同时受雇吗？如果是这样，怎么样？这些是可以通过进一步开发和采用云计算来解决的研究挑战。

> **B. Cloud and Grid Computing**
>
> Grid computing [4] is a hardware and software infrastructure motivated by real problems appearing in advanced scientific research. To our understanding, the Grid is distributed computing ‘middleware’ that provides ‘coordinated cross-organizational resource sharing’ to high-end computational applications such as science and engineering. There exists evident similarities between Cloud Computing and Grid Computing. For one thing, they both aim to achieve resource virtualization. However, they do have significant differences:
>
> Grid emphasizes the “resource sharing” to form a virtual organization. Cloud is often owned by a single physical organization (except the community Cloud, in this case, it is owned by the community), who allocates resources to different running instances.
>
> Grid aims to provide the maximum computing capacity for a huge task through resource sharing. Cloud aims to suffice as many small-to-medium tasks as possible based on users’ real-time requirements. Therefore, multi-tenancy is a very important concept for Cloud computing.
>
> Grid trades re-usability for (scientific) high performance computing. Cloud computing is directly pulled by immediate user needs driven by various business requirements.
>
> Grid strives to achieve maximum computing. Cloud is after on-demand computing – Scale up and down, in and out at the same time optimizing the overall computing capacity.

**B.云和网格计算**

网格计算[4]是由先进科学研究中出现的实际问题所驱动的硬件和软件基础设施。据我们所知，Grid是分布式计算“中间件”，为科学和工程等高端计算应用提供“协调的跨组织资源共享”。云计算与网格计算之间存在明显的相似之处。首先，它们都旨在实现资源虚拟化。但是，它们确实存在显着差异：

Grid强调“资源共享”以形成虚拟组织。云通常由单个物理组织拥有（社区云除外，在这种情况下，它由社区拥有），他们将资源分配给不同的运行实例。

Grid旨在通过资源共享为巨大的任务提供最大的计算能力。云旨在根据用户的实时要求尽可能多地完成中小型任务。因此，多租户是云计算的一个非常重要的概念。

网格交换（科学）高性能计算的可重用性。云计算直接受到各种业务需求驱动的即时用户需求的影响。

Grid致力于实现最大化计算。云是按需计算 - 在扩展和上下扩展，同时优化整体计算能力。

