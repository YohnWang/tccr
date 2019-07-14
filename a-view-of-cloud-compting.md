# A view of cloud compting



> Cloud computing, the long-held dream of computing as a utility, has the potential to transform a large part of the IT industry, making software even more attractive as a service and shaping the way IT hardware is designed and purchased. Developers with innovative ideas for new Internet services no longer require the large capital outlays in hardware to deploy their service or the human expense to operate it. They need not be concerned about overprovisioning for a service whose popularity does not meet their predictions, thus wasting costly resources, or underprovisioning for one that becomes wildly popular, thus missing potential customers and revenue. Moreover, companies with large batch-oriented tasks can get results as quickly as their programs can scale, since using 1,000 servers for one hour costs no more than using one server for 1,000 hours. This elasticity of resources, without paying a premium for large scale, is unprecedented in the history of IT.

云计算是计算机作为一种实用工具的长期梦想，它有可能改变IT行业的大部分，使软件作为服务更具吸引力，并塑造IT硬件的设计和购买方式。对新互联网服务有创新想法的开发人员不再需要硬件上的大量资本支出来部署他们的服务或人力开支来运营它。他们不必担心过度配置的服务，其受欢迎程度不符合他们的预测，因此浪费了昂贵的资源，或者对于那些变得非常受欢迎的服务的供应不足，从而错过了潜在的客户和收入。此外，具有大批量任务的公司可以在程序可以扩展的同时尽快获得结果，因为使用1,000台服务器一小时的成本仅比使用一台服务器长达1,000小时。在没有大规模支付高价的情况下，这种资源弹性在IT历史上是前所未有的。

> As a result, cloud computing is a popular topic for blogging and white papers and has been featured in the title of workshops, conferences, and even magazines. Nevertheless, confusion remains about exactly what it is and when it’s useful, causing Oracle’s CEO Larry Ellison to vent his frustration: “The interesting thing about cloud computing is that we’ve redefined cloud computing to include everything that we already do…. I don’t understand what we would do differently in the light of cloud computing other than change the wording of some of our ads.” Our goal in this article is to reduce that confusion by clarifying terms, providing simple figures to quantify comparisons between of cloud and conventional computing, and identifying the top technical and non-technical obstacles and opportunities of cloud computing. (Armbrust et \${al}^{4}\$ is a more detailed version of this article.)

因此，云计算是博客和白皮书的热门话题，并已在研讨会，会议甚至杂志的标题中出现。然而，混淆仍然是它究竟是什么以及什么时候它有用，导致甲骨文首席执行官拉里埃里森发泄他的沮丧：“云计算的有趣之处在于我们重新定义了云计算以包括我们已经做过的所有事情......除了改变我们的一些广告的措辞之外，我不明白我们会根据云计算做些什么。“我们在本文中的目标是通过澄清术语来减少这种混淆，提供简单的数字来量化之间的比较。云和传统计算，并确定云计算的顶级技术和非技术障碍和机会。（Armbrust et \${al}^{4}\$ 是本文的更详细版本。）

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

> Our proposed definition allows us to clearly identify certain installations as examples and non-examples of cloud computing. Consider a public-facing Internet service hosted on an ISP who can allocate more machines to the service given four hours notice. Since load surges on the public Internet can happen much more quickly than that (Animoto saw its load double every 12 hours for nearly three days), this is not cloud computing. In contrast, consider an internal enterprise data center whose applications are modified only with significant advance notice to administrators.
> In this scenario, large load surges on the scale of minutes are highly unlikely, so as long as allocation can track expected load increases, this scenario fulfills one of the necessary conditions for operating as a cloud. The enterprise data center may still fail to meet other conditions for being a cloud, however, such as the appearance of infinite resources or fine-grained billing. A private data center may also not benefit from the economies of scale that make public clouds financially attractive.

我们提出的定义允许我们清楚地将某些安装标识为云计算的示例和非示例。考虑一个托管在ISP上的面向公众的Internet服务，它可以在四小时通知的情况下为服务分配更多的机器。由于公共互联网上的负载激增可能比这更快（Animoto在近12天内每12小时看到其负载翻倍），这不是云计算。相比之下，考虑一个内部企业数据中心，其应用程序仅在向管理员提前通知的情况下进行修改。
在这种情况下，分钟级别的大量负载激增的可能性极小，因此只要分配可以跟踪预期的负载增加，此方案就可以满足作为云运行的必要条件之一。然而，企业数据中心可能仍然无法满足作为云的其他条件，例如无限资源的出现或细粒度计费。私人数据中心也可能无法从规模经济中受益，这使得公共云具有财务吸引力。

> Omitting private clouds from cloud computing has led to considerable debate in the blogosphere. We believe the confusion and skepticism illustrated by Larry Ellison’s quote occurs when the advantages of public clouds are also claimed for medium-sized data centers. Except for extremely large data centers of hundreds of thousands of machines, such as those that might be operated by Google or Microsoft, most data centers enjoy only a subset of the potential advantages of public clouds, as Table 1 shows. We therefore believe that including traditional data centers in the definition of cloud computing will lead to exaggerated claims for smaller, so-called private clouds, which is why we exclude them. However, here we describe how so-called private clouds can get more of the benefits of public clouds through *surge computing or hybrid cloud computing*.

从云计算中省略私有云已引起博客圈的大量争论。我们认为拉里·埃里森引用的混淆和怀疑主义是在中型数据中心也声称公共云的优势时发生的。除了数十万台机器的超大型数据中心，例如可能由谷歌或微软运营的数据中心，大多数数据中心只享有公共云潜在优势的一部分，如表1所示。因此，我们认为将传统数据中心纳入云计算的定义将导致对较小的，所谓的私有云的夸大宣称，这就是我们排除它们的原因。但是，在这里我们描述了所谓的私有云如何通过浪涌计算或混合云计算获得公共云的更多好处。

## Classes of Utility Computing

> Any application needs a model of computation, a model of storage, and a model of communication. The statistical multiplexing necessary to achieve elasticity and the appearance of infinite capacity available on demand requires automatic allocation and management.
> In practice, this is done with virtualization of some sort. Our view is that different utility computing offerings will be distinguished based on the cloud system software’s level of abstraction and the level of management of the resources.

任何应用程序都需要计算模型，存储模型和通信模型。实现弹性所需的统计多路复用和按需可用的无限容量的出现需要自动分配和管理。
实际上，这是通过某种虚拟化来完成的。我们的观点是，将根据云系统软件的抽象级别和资源管理级别来区分不同的效用计算产品。

> Amazon EC2 is at one end of the spectrum. An EC2 instance looks much like physical hardware, and users can control nearly the entire software stack, from the kernel upward. This low level makes it inherently difficult for Amazon to offer automatic scalability and failover because the semantics associated with replication and other state management issues are highly application-dependent. At the other extreme of the spectrum are application domain-specific platforms such as Google AppEngine, which is targeted exclusively at traditional Web applications, enforcing an application structure of clean separation between a stateless computation tier and a stateful storage tier. AppEngine’s impressive automatic scaling and high-availability mechanisms, and the proprietary MegaStore data storage available to AppEngine applications, all rely on these constraints. Applications for Microsoft’s Azure are written using the .NET libraries, and compiled to the Common Language Runtime, a language-independent managed environment. The framework is significantly more flexible than AppEngine’s, but still constrains the user’s choice of storage model and application structure.Thus, Azure is intermediate between application frameworks like AppEngine and hardware virtual machines like EC2.

亚马逊EC2处于频谱的一端。EC2实例看起来很像物理硬件，用户可以从内核向上控制几乎整个软件堆栈。这种低级别使得亚马逊很难提供自动可扩展性和故障转移，因为与复制和其他状态管理问题相关的语义高度依赖于应用程序。另一方面，特定于应用程序领域的平台，例如Google AppEngine，专门针对传统的Web应用程序，在无状态计算层和有状态存储层之间实施清晰分离的应用程序结构。AppEngine令人印象深刻的自动扩展和高可用性机制，以及AppEngine应用程序可用的专有MegaStore数据存储都依赖于这些限制。Microsoft Azure的应用程序使用.NET库编写，并编译为Common Language Runtime，这是一种独立于语言的托管环境。该框架比AppEngine更灵活，但仍然限制了用户对存储模型和应用程序结构的选择。因此，Azure介于AppEngine等应用程序框架和EC2等硬件虚拟机之间。

## Cloud Computing Economics

> We see three particularly compelling use cases that favor utility computing over conventional hosting. A first case is when demand for a service varies with time. For example, provisioning a data center for the peak load it must sustain a few days per month leads to underutilization at other times.
> Instead, cloud computing lets an organization pay by the hour for computing resources, potentially leading to cost savings even if the hourly rate to rent a machine from a cloud provider is higher than the rate to own one. A second case is when demand is unknown in advance. For example, a Web startup will need to support a spike in demand when it becomes popular, followed potentially by a reduction once some visitors turn away. Finally, organizations that perform batch analytics can use the “cost associativity” of cloud computing to finish computations faster: using 1,000 EC2 machines for one hour costs the same as using one machine for 1,000 hours.

我们看到三个特别引人注目的用例有利于公用计算而不是传统托管。第一种情况是对服务的需求随时间变化。例如，为峰值负载配置数据中心必须每月维持几天，导致其他时间利用不足。相反，云计算允许组织按小时计算计算资源，即使从云提供商租用计算机的小时费率高于拥有计算机的费率，也可能节省成本。第二种情况是提前需求未知。例如，一个网络创业公司需要在它变得流行时支持需求激增，之后可能会在一些访问者拒绝后减少。最后，执行批量分析的组织可以使用云计算的“成本关联性”来更快地完成计算：使用1,000台EC2机器一小时的成本与使用一台机器1000小时相同。

> Although the economic appeal of cloud computing is often described as “converting capital expenses to operating expenses” (CapEx to OpEx), we believe the phrase “pay as you go” more directly captures the economic benefit to the buyer. Hours purchased via cloud computing can be distributed non-uniformly in time (for example, use 100 server-hours today and no server-hours tomorrow, and still pay only for 100); in the networking community, this way of selling bandwidth is already known as usage-based pricing. In addition, the absence of up-front capital expense allows capital to be redirected to core business investment.

虽然云计算的经济吸引力通常被描述为“将资本支出转换为运营支出”（CapEx to OpEx），但我们认为“随用随付”这一短语更直接地抓住了买方的经济利益。通过云计算购买的小时数可以及时非均匀地分发（例如，今天使用100个服务器小时，明天不使用服务器小时，并且仍然仅支付100个）;在网络社区，这种销售带宽的方式已经被称为基于使用的定价。此外，缺乏前期资本支出可以将资金重定向到核心业务投资。

> Therefore, even if Amazon’s pay-as-you-go pricing was more expensive than buying and depreciating a comparable server over the same period, we argue that the cost is outweighed by the extremely important cloud computing economic benefits of elasticity and transference of risk, especially the risks of overprovisioning (underutilization) and underprovisioning (saturation).

因此，即使亚马逊的按需付费定价比同期购买和折旧同类服务器更昂贵，我们认为弹性和风险转移的极其重要的云计算经济效益抵消了成本，特别是过度供应（利用不足）和供应不足（饱和）的风险。

> We start with elasticity. The key observation is that cloud computing’s ability to add or remove resources at a fine grain (one server at a time with EC2) and with a lead time of minutes rather than weeks allows matching resources to workload much more closely. Real world estimates of average server utilization in data centers range from 5% to 20%. This may sound shockingly low, but it is consistent with the observation that for many services the peak workload exceeds the average by factors of 2 to 10. Since few users deliberately provision for less than the expected peak, resources are idle at nonpeak times. The more pronounced the variation, the more the waste.

我们从弹性角度开始。关键的观察结果是，云计算能够以细粒度（使用EC2一次一个服务器）添加或删除资源，并且提前几分钟而不是几周，这样可以更加紧密地将资源与工作负载相匹配。现实世界对数据中心平均服务器利用率的估计在5％到20％之间。这可能听起来令人震惊地低，但这与观察结果一致，即对于许多服务而言，峰值工作量超过平均值2到10倍。由于很少用户故意提供低于预期峰值的资源，因此资源在非峰值时间处于空闲状态。变化越明显，浪费越多。

> For example, Figure 2a assumes our service has a predictable demand where the peak requires 500 servers at noon but the trough requires only 100 servers at midnight. As long as the average utilization over a whole day is 300 servers, the actual cost per day (area under the curve) is 300 × 24 = 7,200 server hours; but since we must provision to the peak of 500 servers, we pay for 500 × 24 = 12,000 server-hours, a factor of 1.7 more. Therefore, as long as the pay-asyougo cost per server-hour over three years (typical amortization time) is less than 1.7 times the cost of buying the server, utility computing is cheaper.

例如，图2a假设我们的服务具有可预测的需求，其中峰值在中午需要500台服务器，但是低谷在午夜仅需要100台服务器。只要一整天的平均利用率为300台服务器，每天的实际成本（曲线下面积）为300×24 = 7,200服务器小时;但由于我们必须提供500台服务器的峰值，我们支付500×24 = 12,000服务器小时，相当于1.7倍。因此，只要三年（每个服务器小时）的付费使用成本（典型的摊还时间）小于购买服务器的成本的1.7倍，公用计算就更便宜。

> In fact, this example underestimates the benefits of elasticity, because in addition to simple diurnal patterns, most services also experience seasonal or other periodic demand variation (for example, e-commerce in December and photo sharing sites after holidays) as well as some unexpected demand bursts due to external events (for example, news events). Since it can take weeks to acquire and rack new equipment, to handle such spikes you must provision for them in advance. We already saw that even if service operators predict the spike sizes correctly, capacity is wasted, and if they overestimate the spike they provision for, it’s even worse.

事实上，这个例子低估了弹性的好处，因为除了简单的昼夜模式，大多数服务还会遇到季节性或其他周期性需求变化（例如，12月的电子商务和假期后的照片共享网站）以及一些意外的由于外部事件（例如，新闻事件）而导致需求突发。由于可能需要数周时间才能获得并装备新设备，因此必须提前为这些尖峰进行处理。我们已经看到，即使服务运营商正确地预测了峰值大小，也会浪费容量，如果他们高估了他们提供的峰值，那就更糟了。

> They may also underestimate the spike (Figure 2b), however, accidentally turning away excess users. While the cost of overprovisioning is easily measured, the cost of underprovisioning is more difficult to measure yet potentially equally serious: not only do rejected users generate zero revenue, they may never come back. For example, Friendster’s decline in popularity relative to competitors Facebook and MySpace is believed to have resulted partly from user dissatisfaction with slow response times (up to 40 seconds). Figure 2c aims to capture this behavior: Users will desert an underprovisioned service until the peak user load equals the data center’s usable capacity, at which point users again receive acceptable service.

他们也可能低估了尖峰（图2b），然而，意外地拒绝了多余的用户。虽然过度配置的成本很容易衡量，但是欠配置的成本更难以衡量，但可能同样严重：不仅被拒绝的用户产生零收入，他们可能永远不会回来。例如，相对于竞争对手Facebook和MySpace而言，Friendster的受欢迎程度下降被认为部分是由于用户对响应时间较慢（最多40秒）的不满.图2c旨在捕捉这种行为：用户将抛弃未充分利用的服务，直到峰值用户负载等于数据中心的可用容量，此时用户再次接收可接受的服务。

> For a simplified example, assume that users of a hypothetical site fall into two classes: active users (those who use the site regularly) and defectors (those who abandon the site or are turned away from the site due to poor performance).Further, suppose that 10% of active users who receive poor service due to underprovisioning are “permanently lost” opportunities (become defectors), that is, users who would have remained regular visitors with a better experience. The site is initially provisioned to handle an expected peak of 400,000 users (1,000 users per server × 400 servers), but unexpected positive press drives 500,000 users in the first hour. Of the 100,000 who are turned away or receive bad service, by our assumption 10,000 of them are permanently lost, leaving an active user base of 390,000. The next hour sees 250,000 new unique users. The first 10,000 do fine, but the site is still overcapacity by 240,000 users. This results in 24,000 additional defections, leaving 376,000 permanent users. If this pattern continues, after lg(500,000) or 19 hours, the number of new users will approach zero and the site will be at capacity in steady state. Clearly, the service operator has collected less than 400,000 users’ worth of steady revenue during those 19 hours, however, again illustrating the underutilization argument—to say nothing of the bad reputation from the disgruntled users.

举一个简单的例子，假设一个假设网站的用户分为两类：活跃用户（定期使用网站的用户）和叛逃者（放弃网站或由于性能不佳而拒绝网站的用户）。此外，假设由于资金不足而接受服务质量差的10％的活跃用户是“永久性失去”的机会（成为叛逃者），也就是那些本来可以保持常规访问者并获得更好体验的用户。该网站最初配置为处理400,000个用户的预期峰值（每个服务器1,000个用户×400个服务器），但意外的正压力在第一个小时内驱动500,000个用户。在被拒绝或接受不良服务的100,000人中，我们假设其中10,000人永久丢失，留下了390,000的活跃用户群。下一个小时将看到250,000个新的唯一身份用户。前10,000个很好，但该网站仍有240,000个用户的产能过剩。这导致24,000次额外叛逃，留下376,000名永久用户。如果此模式继续，在lg(500,000)或19小时之后，新用户的数量将接近零，并且站点将处于稳定状态的容量。显然，服务运营商在这19个小时内收集了不到40万用户的稳定收入，然而，再次说明了未充分利用的论点 —— 更不用说心怀不满的用户的不良声誉。

> Do such scenarios really occur in practice? When Animoto3 made its service available via Facebook, it experienced a demand surge that resulted in growing from 50 servers to 3,500 servers in three days. Even if the average utilization of each server was low, no one could have foreseen that resource needs would suddenly double every 12 hours for three days. After the peak subsided, traffic fell to a lower level. So in this real-world example, scale-up elasticity was not a cost optimization but an operational requirement, and scaledown elasticity allowed the steady-state expenditure to more closely match the steady-state workload.

这种情况真的发生在实践中吗？当Animoto3通过Facebook提供服务时，它经历了需求激增，导致在三天内从50台服务器增长到3,500台服务器。即使每台服务器的平均利用率很低，也没有人能够预见到资源需求会在12天内突然翻倍，持续3天。高峰消退后，交通量降至较低水平。因此，在这个现实世界的例子中，放大弹性不是成本优化而是操作要求，并且缩放弹性允许稳态支出更紧密地匹配稳态工作负荷。

## Top 10 Obstacles and Opportunities for Cloud Computing

> Table 2 summarizes our ranked list of critical obstacles to growth of cloud computing. The first three affect adoption, the next five affect growth, and the last two are policy and business obstacles. Each obstacle is paired with an opportunity to overcome that obstacle, ranging from product development to research projects.

表2总结了我们对云计算增长的关键障碍的排名列表。前三个影响采用，后五个影响增长，后两个影响政策和业务障碍。每个障碍都与克服障碍的机会相结合，从产品开发到研究项目。

### Number 1. Business Continuity and Service Availability

> Organizations worry about whether utility computing services will have adequate availability, and this makes some wary of cloud computing. Ironically, existing SaaS products have set a high standard in this regard. Google Search has a reputation for being highly available, to the point that even a small disruption is picked up by major news sources. 

组织担心效用计算服务是否具有足够的可用性，这使得人们对云计算持谨慎态度。具有讽刺意味的是，现有的SaaS产品在这方面已经树立了很高的标准。谷歌搜索以其高可用性而闻名，即使主要新闻来源即使是一个小小的中断也是如此。

> Users expect similar availability from new services, which is difficult to do. Table 3 shows recorded outages for Amazon Simple Storage Service (S3), AppEngine and Gmail in 2008, and explanations for the outages. Note that despite the negative publicity due to these outages, few enterprise IT infrastructures are as good. Technical issues of availability aside, a cloud provider could suffer outages for nontechnical reasons, including going out of business or being the target of regulatory action (a recent example of the latter occurred last year, as we describe later).

用户希望新服务具有类似的可用性，这很难做到。表3显示了2008年亚马逊简单存储服务（S3），AppEngine和Gmail的记录中断，以及对中断的解释。请注意，尽管由于这些中断导致负面宣传，但很少有企业IT基础架构同样出色。除了可用性的技术问题之外，云提供商可能因非技术原因而遭受停机，包括停业或成为监管行动的目标（最近的一个例子发生在去年，如我们后面所述）。

> Although they have not done so, cloud vendors could offer specialized hardware and software techniques in order to deliver higher reliability, presumably at a high price. This reliability could then be sold to users as a service-level agreement. But this approach only goes so far. The high-availability computing community has long followed the mantra “no single point of failure,” yet the management of a cloud computing service by a single company is in fact a single point of failure. Even if the company has multiple data centers in different geographic regions using different network providers, it may have common software infrastructure and accounting systems, or the company may even go out of business. Large customers will be reluctant to migrate to cloud computing without a business-continuity strategy for such situations. We believe the best chance for independent software stacks is for them to be provided by different companies, as it has been difficult for one company to justify creating and maintain two stacks in the name of software dependability. Just as large Internet service providers use multiple network providers so that failure by a single company will not take them off the air, we believe the only plausible solution to very high availability is multiple cloud computing providers.

虽然他们还没有这样做，但云供应商可以提供专门的硬件和软件技术，以便提供更高的可靠性，大概是以高价格。然后，这种可靠性可以作为服务级别协议出售给用户。但这种方法只是到目前为止。高可用性计算社区长期以来一直遵循“没有单点故障”的口号，但单个公司对云计算服务的管理实际上是单点故障。即使公司在不同地理区域使用不同的网络提供商拥有多个数据中心，它也可能拥有通用的软件基础设施和会计系统，或者公司甚至可能会倒闭。如果没有针对此类情况的业务连续性策略，大客户将不愿意迁移到云计算。我们认为独立软件堆栈的最佳机会是由不同公司提供，因为一家公司很难以软件可靠性的名义创建和维护两个堆栈。正如大型互联网服务提供商使用多个网络提供商，以便单个公司的失败不会使他们无法播出，我们认为高可用性的唯一可行解决方案是多个云计算提供商。

### Number 2. Data Lock-In

> Software stacks have improved interoperability among platforms, but the storage APIs for cloud computing are still essentially proprietary, or at least have not been the subject of active standardization. Thus, customers cannot easily extract their data and programs from one site to run on another. Concern about the difficulty of extracting data from the cloud is preventing some organizations from adopting cloud computing. Customer lock-in may be attractive to cloud computing providers, but their users are vulnerable to price increases, to reliability problems, or even to providers going out of business.

软件堆栈改善了平台之间的互操作性，但云计算的存储API仍然基本上是专有的，或者至少不是主动标准化的主题。因此，客户无法轻松地从一个站点提取其数据和程序以在另一个站点上运行。对从云中提取数据的难度的担忧阻碍了一些组织采用云计算。客户锁定可能对云计算提供商具有吸引力，但他们的用户很容易受到价格上涨，可靠性问题甚至服务提供商破产的影响。

> For example, an online storage service called The Linkup shut down on Aug. 8, 2008 after losing access as much as 45% of customer data. The Linkup, in turn, had relied on the online storage service Nirvanix to store customer data, which led to finger pointing between the two organizations as to why customer data was lost. Meanwhile, The Linkup’s 20,000 users were told the service was no longer available and were urged to try out another storage site.

例如，一个名为The Linkup的在线存储服务在失去了45％的客户数据后，于2008年8月8日关闭。反过来，Linkup依靠在线存储服务Nirvanix来存储客户数据，从而指导两个组织之间关于客户数据丢失的原因。同时，Linkup的20,000名用户被告知该服务已不再可用，并被敦促尝试另一个存储站点。

> One solution would be to standardize the APIsd in such a way that a SaaS developer could deploy services and data across multiple cloud computing providers so that the failure of a single company would not take all copies of customer data with it. One might worry that this would lead to a “race-to-the-bottom” of cloud pricing and flatten the profits of cloud computing providers. We offer two arguments to allay this fear.

一种解决方案是以一种SaaS开发人员可以跨多个云计算提供商部署服务和数据的方式标准化API，以便单个公司的失败不会随之获取所有客户数据副本。有人可能会担心这会导致云定价的“竞争到底”，并使云计算提供商的利润趋于平缓。我们提出两个论点来消除这种恐惧。

> First, the quality of a service matters as well as the price, so customers may not jump to the lowest-cost service. Some Internet service providers today cost a factor of 10 more than others because they are more dependable and offer extra services to improve usability.

首先，服务质量和价格都很重要，因此客户可能不会跳到成本最低的服务。如今，一些互联网服务提供商的成本比其他因素高10倍，因为它们更可靠，并提供额外的服务来提高可用性。

> Second, in addition to mitigating data lock-in concerns, standardization of APIs enables a new usage model in which the same software infrastructure can be used in an internal data center and in a public cloud. Such an option could enable hybrid cloud computing or surge computing in which the public cloud is used to capture the extra tasks that cannot be easily run in the data center (or private cloud) due to temporarily heavy workloads. This option could significantly expand the cloud computing market. Indeed, open-source reimplementations of proprietary cloud APIs, such as Eucalyptus and HyperTable, are first steps in enabling surge computing.

其次，除了减轻数据锁定问题之外，API的标准化还支持新的使用模式，其中相同的软件基础架构可用于内部数据中心和公共云。这样的选项可以实现混合云计算或浪涌计算，其中公共云用于捕获由于临时繁重的工作负载而在数据中心（或私有云）中不能轻易运行的额外任务。此选项可以显着扩展云计算市场。实际上，专有云API的开源重新实现，例如Eucalyptus和HyperTable，是启用浪涌计算的第一步。

### Number 3. Data Confidentiality/Auditability

