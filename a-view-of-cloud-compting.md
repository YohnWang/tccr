# A view of cloud compting



> Cloud computing, the long-held dream of computing as a utility, has the potential to transform a large part of the IT industry, making software even more attractive as a service and shaping the way IT hardware is designed and purchased. Developers with innovative ideas for new Internet services no longer require the large capital outlays in hardware to deploy their service or the human expense to operate it. They need not be concerned about overprovisioning for a service whose popularity does not meet their predictions, thus wasting costly resources, or underprovisioning for one that becomes wildly popular, thus missing potential customers and revenue. Moreover, companies with large batch-oriented tasks can get results as quickly as their programs can scale, since using 1,000 servers for one hour costs no more than using one server for 1,000 hours. This elasticity of resources, without paying a premium for large scale, is unprecedented in the history of IT.

云计算是计算机作为一种实用工具的长期梦想，它有可能改变IT行业的大部分，使软件作为服务更具吸引力，并塑造IT硬件的设计和购买方式。对新互联网服务有创新想法的开发人员不再需要硬件上的大量资本支出来部署他们的服务或人力开支来运营它。他们不必担心过度配置的服务，其受欢迎程度不符合他们的预测，因此浪费了昂贵的资源，或者对于那些变得非常受欢迎的服务的供应不足，从而错过了潜在的客户和收入。此外，具有大批量任务的公司可以在程序可以扩展的同时尽快获得结果，因为使用1,000台服务器一小时的成本仅比使用一台服务器长达1,000小时。在没有大规模支付高价的情况下，这种资源弹性在IT历史上是前所未有的。

> As a result, cloud computing is a popular topic for blogging and white papers and has been featured in the title of workshops, conferences, and even magazines. Nevertheless, confusion remains about exactly what it is and when it’s useful, causing Oracle’s CEO Larry Ellison to vent his frustration: “The interesting thing about cloud computing is that we’ve redefined cloud computing to include everything that we already do…. I don’t understand what we would do differently in the light of cloud computing other than change the wording of some of our ads.” Our goal in this article is to reduce that confusion by clarifying terms, providing simple figures to quantify comparisons between of cloud and conventional computing, and identifying the top technical and non-technical obstacles and opportunities of cloud computing. (Armbrust et $\mathrm{al}^{4}$ is a more detailed version of this article.)

因此，云计算是博客和白皮书的热门话题，并已在研讨会，会议甚至杂志的标题中出现。然而，混淆仍然是它究竟是什么以及什么时候它有用，导致甲骨文首席执行官拉里埃里森发泄他的沮丧：“云计算的有趣之处在于我们重新定义了云计算以包括我们已经做过的所有事情......除了改变我们的一些广告的措辞之外，我不明白我们会根据云计算做些什么。“我们在本文中的目标是通过澄清术语来减少这种混淆，提供简单的数字来量化之间的比较。云和传统计算，并确定云计算的顶级技术和非技术障碍和机会。（Armbrust et $\mathrm{al}^{4}$ 是本文的更详细版本。）

## Defining Cloud Computing

> Cloud computing refers to both the applications delivered as services over the Internet and the hardware and systems software in the data centers that provide those services. The services themselves have long been referred to as Software as a Service (SaaS). Some vendors use terms such as IaaS (Infrastructure as a Service) and PaaS (Platform as a Service) to describe their products, but we eschew these because accepted definitions for them still vary widely. The line between “low-level” infrastructure and a higher-level “platform” is not crisp. We believe the two are more alike than different, and we consider them together. Similarly, the related term “grid computing,” from the high-performance computing community, suggests protocols to offer shared computation and storage over long distances, but those protocols did not lead to a software environment that grew beyond its community.

云计算既指通过因特网作为服务提供的应用程序，也指提供这些服务的数据中心中的硬件和系统软件。服务本身长期以来被称为软件即服务（SaaS）。一些供应商使用诸如IaaS（基础架构即服务）和PaaS（平台即服务）之类的术语来描述他们的产品，但我们避开这些术语，因为它们的公认定义仍然存在很大差异。“低级”基础设施与更高级别“平台”之间的界限并不清晰。我们相信这两者更相似而不同，我们一起考虑它们。类似地，来自高性能计算社区的相关术语“网格计算”建议用于长距离提供共享计算和存储的协议，但是这些协议不会导致超出其社区的软件环境。

> The data center hardware and software is what we will call a cloud. When a cloud is made available in a pay-asyougo manner to the general public, we call it a public cloud; the service being sold is utility computing. We use the term private cloud to refer to internal data centers of a business or other organization, not made available to the general public, when they are large enough to benefit from the advantages of cloud computing that we discuss here. Thus, cloud computing is the sum of SaaS and utility computing,but does not include small or mediumsized data centers, even if these rely on virtualization for management. People can be users or providers of SaaS, or users or providers of utility computing.We focus on SaaS providers (cloud users) and cloud providers, which have received less attention than SaaS users.Figure 1 makes provider-user relationships clear. In some cases, the same actor can play multiple roles. For instance, a cloud provider might also host its own customer-facing services on cloud infrastructure.

数据中心硬件和软件就是我们所说的云。当云以一种付费方式向公众提供时，我们将其称为公共云; 正在销售的服务是效用计算。我们使用术语私有云来指代企业或其他组织的内部数据中心，当它们足够大以便从我们在此讨论的云计算的优势中受益时，不向公众提供。因此，云计算是SaaS和效用计算的总和，但不包括小型或中型数据中心，即使这些数据中心依赖虚拟化进行管理。人们可以是SaaS的用户或提供者，或者是公用计算的用户或提供者。我们专注于SaaS提供商（云用户）和云提供商，这些提供商受到的关注程度低于SaaS用户。图1使提供者 - 用户关系清晰。在某些情况下，同一个角色可以扮演多个角色。例如，云提供商也可能在云基础架构上托管自己面向客户的服务。

> From a hardware provisioning and pricing point of view, three aspects are new in cloud computing.
>
> The appearance of infinite computing resources available on demand, quickly enough to follow load surges, thereby eliminating the need for cloud computing users to plan far ahead for provisioning.
>
> The elimination of an up-front commitment by cloud users, thereby allowing companies to start small and increase hardware resources only when there is an increase in their needs.
>
> The ability to pay for use of computing resources on a short-term basis as needed (for example, processors by the hour and storage by the day) and release them as needed, thereby rewarding conservation by letting machines and storage go when they are no longer useful.

从硬件配置和定价的角度来看，云计算中有三个方面是新的。
无限计算资源的出现可按需提供，足以快速跟踪负载激增，从而消除了云计算用户远程规划供应的需求。
消除云用户的前期承诺，从而允许公司只有在需求增加时才能从小规模开始并增加硬件资源。
能够根据需要在短期内支付使用计算资源的费用（例如，按小时处理的处理器和按天存储的费用）并根据需要发布它们，从而通过让机器和存储在不存在时进行保护来奖励保护 更长的用处。

> We argue that the construction and operation of extremely large-scale, commodity-computer data centers at low-cost locations was the key necessary enabler of cloud computing, for they uncovered the factors of 5 to 7 decrease in cost of electricity, network bandwidth, operations, software, and hardware available at these very large economies of scale. These factors, combined with statistical multiplexing to increase utilization compared to traditional data centers, meant that cloud computing could offer services below the costs of a medium-sized data center and yet still make a good profit.

我们认为，在低成本地区建设和运营极其大规模的商品计算机数据中心是云计算的关键必要推动因素，因为他们发现了电力成本，网络带宽，在这些非常大的规模经济中可用的操作，软件和硬件。与传统数据中心相比，这些因素与统计复用相结合，可提高利用率，这意味着云计算可以提供低于中型数据中心成本的服务，但仍能获得丰厚利润。

