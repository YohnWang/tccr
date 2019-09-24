# Towards task scheduling in a cloud-fog computing system

> Abstract—In recent years, with the advent of the Internet of Things (IoT), fog computing is introduced as a powerful complement to the cloud to handle the IoT’s data and communications needs. The interplay and cooperation between the edge (fog) and the core (cloud) has recently received considerable attention. In this paper, we consider task scheduling in a cloud-fog computing system, where a fog provider can exploit the collaboration between its own fog nodes and the rented cloud nodes for efficiently executing users’ large-scale offloading applications. We first formulate the task scheduling problem in such cloud-fog environment and then propose a heuristic-based algorithm, whose major objective is achieving the balance between the makespan and the monetary cost of cloud resources. The numerical results show that our proposed algorithm achieves better tradeoff value than other existing algorithms.
> Index Terms—cloud computing, fog computing, task scheduling, Internet of Things.

摘要——近年来，随着物联网（IoT）的出现，雾计算被引入作为对云的强大补充，以处理物联网的数据和通信需求。边缘（雾）和核心（云）之间的相互作用和协作最近受到了相当大的关注。在本文中，我们考虑了云雾计算系统中的任务调度，在该系统中，雾提供者可以利用其自身的雾节点与租用的云节点之间的协作来高效执行用户的大型卸载应用程序。我们首先在这种云雾环境中制定任务调度问题，然后提出一种基于启发式的算法，其主要目的是在云资源的制造期和货币成本之间取得平衡。数值结果表明，与现有算法相比，本文算法具有更好的折衷价值。
索引词-云计算，雾计算，任务调度，物联网。

## I. INTRODUCTION

> Fog computing is a promising solution to deal with the demands of the ever-increasing number of Internet-connected devices. The idea of fog computing is to extend the cloud to be closer to the things that produce and act on IoT data. Instead of forcing all processing to back-end clouds, fog computing aims to process part of the services’ workload locally on fog nodes, which are served as a near-end computing proxies between the front-end IoT devices and the back-end cloud servers. Putting resources at the edge of the network only one or two hops from the data sources allows fog nodes to perform low latency processing while latency-tolerant and large-scale tasks can still be efficiently processed by the cloud. In addition, the cost and scale benefits of the cloud can help the fog to serve peak demands of IoT devices if the resources of fog nodes are not sufficient. Also, many applications require the interplay and cooperation between the edge (fog) and the core (cloud), particularly for the IoT and big data analysis [1]. From this point of view, fog computing is not aimed to replace cloud computing, but to complement it in a new computing paradigm, cloud-fog computing, which is to satisfy the increasingly sophisticated applications demanded by users.

雾计算是一种有前途的解决方案，可以满足越来越多的Internet连接设备的需求。雾计算的想法是扩展云，使其更接近于产生和作用于IoT数据的事物。雾计算不是将所有处理都强加到后端云，而是旨在在雾节点上本地处理部分服务工作负载，这些雾节点用作前端物联网设备和后端云服务器之间的近端计算代理。将资源放在网络边缘仅距离数据源一跳或两跳，可使雾节点执行低延迟处理，而云仍然可以有效处理延迟等待和大规模任务。此外，如果雾节点的资源不足，云的成本和规模优势可帮助雾满足物联网设备的峰值需求。另外，许多应用程序需要边缘（雾）和核心（云）之间的相互作用和协作，特别是对于物联网和大数据分析[1]。从这个角度来看，雾计算的目的不是替代云计算，而是在一种新的计算范例云雾计算中对其进行补充，以满足用户日益复杂的应用程序的需求。

> In this paper, we consider task scheduling in a cloud-fog computing system, where a fog provider can exploit the collaboration between its fog nodes and the rented cloud nodes for efficiently executing users’ large-scale offloading  applications. The fog nodes are local resources, which can be any devices with computing, storage, and network connectivity such as switches, routers, video surveillance cameras, etc. A simple scenario is that a shopping center can deploy many fog nodes in different floors to provide WiFi access and deliver some engaged services (i.e. indoor navigation, ads distribution, feedback collections) to its customers. However, in peak time, the capabilities of those fog nodes cannot efficiently serve the customers. Meanwhile, the fog provider, here is the shopping center, can extend its infrastructure by paying for the outsourced computation and storage resources of the cloud nodes, which can be virtual machine (VM) rented from cloud providers on a pay-per-use basis. All distributed processing nodes (cloud or fog) are managed by a resource broker, which is a resource management component and scheduler for the workflows submitted from users at the fog’s side. In this case, a task schedule, which can minimize the completion time of the workflow, but corresponds to a large amount of monetary cost, is not an optimal solution for fog providers. Thus, in this paper, we propose a task scheduling algorithm that can achieve a good tradeoff between the workflow execution time and the cost for the use of cloud resources. The experimental results show the outstanding performance of our method compared with some other works.

在本文中，我们考虑了cloud-fog计算系统中的任务调度，在该系统中，雾服务提供商可以利用其雾节点与租用云节点之间的协作来有效执行用户的大型卸载应用程序。雾节点是本地资源，可以是具有计算，存储和网络连接功能的任何设备，例如交换机，路由器，视频监控摄像机等。一个简单的场景是购物中心可以在不同楼层部署许多雾节点以提供WiFi访问并向其客户提供一些互动服务（例如室内导航，广告分发，反馈收集）。但是，在高峰时间，这些雾节点的功能无法有效地为客户服务。同时，雾提供商（这里是购物中心）可以通过支付云节点的外包计算和存储资源来扩展其基础架构，云节点可以是按使用量付费从云提供商租用的虚拟机（VM）。所有分布式处理节点（云或大雾）均由资源代理管理，资源代理是大雾侧用户提交的工作流的资源管理组件和调度程序。在这种情况下，任务计划表不是雾提供商的最佳解决方案，该任务计划表可以最大程度地缩短工作流程的完成时间，但要花大量的金钱成本。因此，在本文中，我们提出了一种任务调度算法，该算法可以在工作流执行时间和云资源的使用成本之间取得良好的折衷。实验结果表明，与其他一些工作相比，我们的方法具有出色的性能。

> The remainder of the paper is organized as follows. In section 2, we introduce some related works to the task scheduling problem in heterogeneous environments. The architecture of the cloud-fog computing system is described in section 3. In section 4, we formulate the task scheduling problem and present our proposed method. Then we describe some experimental results in section 5, followed by our conclusions and suggestions for future work in section 6.

在本文的其余部分安排如下。在第二部分中，我们介绍了有关异构环境中的任务调度问题的一些相关工作。第3节介绍了云雾计算系统的体系结构。在第4节中，我们阐述了任务调度问题并提出了我们提出的方法。然后，我们在第5节中描述了一些实验结果，然后在第6节中给出了对未来工作的结论和建议。

## II. RELATED WORK

> In heterogeneous environments, despite numerous efforts, task scheduling still remains a big challenge. As usual presentation, each application is comprised of multiple interdependent tasks and each of which is specified by an amount of processing works. It can be modeled as a Directed Acyclic Graph (DAG), in which vertices represent application tasks and edges represent intertask data dependencies. The primary goal of task scheduling is to schedule tasks on processors and minimize the makespan of the schedule, which has been shown to be NP-complete problem. The most common task scheduling algorithms are list-scheduling heuristics. For example, the Earliest Time First (ETF) algorithm [2] computes, at each step, the earliest start times of each tasks on all processors and then selects the one with the smallest start time. The Dynamic Level Scheduling (DLS) algorithm [3] selects the task-processor pair that maximizes the value of the dynamic level (DL), which is the different between the static level of a task and its earliest start time on a processor. Meanwhile, the heterogeneous earliest-finish-time (HEFT) algorithm [4] selects the tasks with the highest upward rank and then assigns it to the processor that minimizes its earliest finish time. However, how to achieve good tradeoff value between the makespan and the monetary cost is not considered in these algorithms.

在异构环境中，尽管付出了很多努力，但是任务调度仍然是一个很大的挑战。与通常的演示一样，每个应用程序都包含多个相互依赖的任务，每个任务都由大量的处理工作指定。可以将其建模为有向无环图（DAG），其中顶点表示应用程序任务，边表示任务间数据依赖性。任务调度的主要目标是在处理器上调度任务，并最大程度地减少调度的完成时间，这已被证明是NP完全问题。最常见的任务调度算法是列表调度启发法。例如，最早时间优先（ETF）算法[2]在每个步骤中计算所有处理器上每个任务的最早开始时间，然后选择启动时间最小的时间。动态级别调度（DLS）算法[3]选择使动态级别（DL）的值最大化的任务处理器对，该值是任务的静态级别与其在处理器上的最早启动时间之间的差。同时，异构最早完成时间（HEFT）算法[4]选择具有最高排名的任务，然后将其分配给处理器以最大程度地缩短其最早完成时间。然而，在这些算法中没有考虑如何在制造期和货币成本之间实现良好的折衷值。

> For a large scale environment, e.g. cloud computing system, there had been also numerous scheduling approaches proposed with the goal achieving both the better application execution and cost saving for cloud resources. Bossche at al. [5] introduce a cost-oriented scheduling algorithm to select the most proper system (private or public cloud) for executing the incoming workflows based on the ability of meeting the deadline of each workflow and cost savings. The budget constraints for using the cloud resource are considered in ScaleStar [6], whose task assignment is based on a novel objective function Comparative Advantage (CA). This algorithm achieves good balance between cost savings and schedule length, however, the high complexity of CA hinder the algorithm to be applied to the large-scale workflows.

对于大型环境，例如在云计算系统中，还提出了许多调度方法，旨在实现更好的应用程序执行和节省云资源的成本。博什等人[5]引入了一种面向成本的调度算法，根据能够满足每个工作流的最后期限和节省成本的能力，选择最合适的系统（私有或公共云）来执行传入的工作流。在ScaleStar [6]中考虑了使用云资源的预算约束，其任务分配基于一种新颖的目标函数比较优势（CA）。该算法在节省成本和调度长度之间取得了很好的平衡，但是，CA的高复杂性阻碍了该算法应用于大规模工作流。

## III. SYSTEM MODEL

> Our cloud-fog computing system has three layers in a hierarchy network, as represented in Figure 1. The front-end layer consists of IoT devices, which serve as user interfaces that send requests from users. The fog layer, which is formed by a set of near-end fog nodes, receives and processes part of a workload of users’ requests. The cloud layer, which hosts a number of computing machines or cloud nodes, provides outsourced resources to execute the workload dispatched from the fog layer. Because the computing resources of our system are dispersed into cloud nodes and fog nodes, there is a smart gateway or broker, which is a centralized management component and task scheduler. The broker (1) receives all requests of users; (2) manages available resources on cloud and fog nodes (e.g. processing capacity, network bandwidth) as well as processing and communication costs together with results of data query returned from nodes; and (3) creates the most appropriate schedule for an input workflow.

我们的云雾计算系统在层次结构网络中具有三层，如图1所示。前端层由IoT设备组成，它们充当用户界面，用于发送来自用户的请求。由一组近端雾节点组成的雾层接收并处理用户请求的部分工作负载。托管许多计算机或云节点的云层提供外包资源，以执行从雾层分派的工作负载。由于我们系统的计算资源分散在云节点和雾节点中，因此存在一个智能网关或代理，它是集中式管理组件和任务调度程序。代理（1）接收用户的所有请求；（2）管理云和雾节点上的可用资源（例如处理能力，网络带宽）以及处理和通信成本，以及从节点返回的数据查询结果；（3）为输入工作流程创建最合适的时间表。

![fig1](resource/Towards-task-scheduling-in-a-cloud-fog-computing/1.png)

## IV. TASK SCHEDULING IN CLOUD-FOG COMPUTING SYSTEM

> **A. Task graph**
>
> A task graph is represented by a Directed Acyclic Graph (DAG), $G=(V,E)$, where the set of vertices $V = \{v_1,v_2,...,v_n\}$ denotes the set of parallel subtasks and each edge $e_{ij} \in E$ represents the precedence constraint such that task $v_i$ should complete its execution before task $v_j$ starts. 
>
> Each task $v_i \in V$ has positive workload $w_i$ representing the amount of computing works (e.g. the number of instructions), which have to be processed at the computing resources. And each edge $e_{ij} \in E$ has nonnegative weight $c_{ij}$ representing the amount of communication data transfered from task $v_i$ and used as input data for task $v_j$ . We assume that the sufficient input data of each task is gathered not only from the preceding tasks but also from other data sources (i.e. data storages) on both cloud and fog infrastructure. A task cannot begin execution until all its inputs have arrived. 
>
> The set of all direct predecessors and successors of $v_i$ is denoted as $pred(v_i)$ and $succ(v_i)$ respectively. We assume that $G$ has an entry task, $v_{entry}$, without any predecessors and an exit task, $v_{exit}$, without any successors.

**A. 任务图**

任务图由有向无环图（DAG）表示，$ G =（V，E）$，其中顶点集$ V = \{v_1，v_2，...，v_n \} $表示 并行子任务，并且每个边$ e_ {ij} \in E$表示优先约束，因此任务 $v_i $应该在任务$ v_j $开始之前执行完成。
每个任务$v_i \in V$有正的工作负载$w_i$表示必须在计算资源上处理的计算工作量（例如指令数）。并且每条边$e_{ij} \in E$有一个非负权重$c_{ij}$代表从任务$v_i$传输的通信数据量和用作任务$v_i$的输入数据量。我们假设每个任务的充足输入数据不仅从前面的任务中收集，而且还从云和雾基础设施上的其他数据源（即数据存储）中收集。任务的所有输入都到达后才能开始执行。

所有$v_i$直接的前置和后置任务的集合被记为$pred(v_i)$和$succ(v_i)$。我们假定$G$有一个入口任务$v_{entry}$，他没有任何的前置任务，和一个退出任务$v_{exit}$，他没有任何后继任务。

> **B. Processor graph**
>
> A processor graph $PG = (N,D)$ denotes the topology of a cloud-fog network, where the set of vertices $N = \{P_1,P_2,...,P_n\}$ denotes the set of processors, each of which is cloud or fog node and an edge $d_{ij} \in D$ denotes a link between processor $P_i$ and $P_j$ . Let $N_{cloud}$ and $N_{fog}$ denotes the set of cloud nodes and the set of fog nodes respectively.
> Hence, $N = N_{cloud} \cup N_{fog}$. Each processor $P_i$ has processing rate $p_i$ and the link $d_{ij}$ between processor $P_i$ and $P_j$ has bandwidth $bw_{ij}$ .

**B. 处理器图**

处理器图$ PG =(N,D)$表示云雾网络的拓扑，其中顶点集合$ N = \{P_1，P_2，...，P_n \} $表示处理器集合， 每个节点都是云或雾节点，并且每条边$d_{ij} \in D$表示处理器$ P_i $和$ P_j $之间的链接。 令$ N_ {cloud} $和$ N_ {fog} $分别表示云节点集和雾节点集。 因此，$ N = N_ {cloud} \cup N_ {fog} $。 每个处理器$ P_i $具有处理速率$ p_i $，并且处理器$ P_i $和$ P_j $之间的链接$ d_ {ij} $具有带宽$ bw_ {ij} $。

> **C. Proposed method**
>
> Given a task graph $V =\{v1, v2,...,v_n\}$ and a processor graph $P = (N,D)$, we consider to choose the most appropriate schedule to execute the tasks. Our method has two phases:
>
> 1) *Determining the task priority:* In this phase, tasks are ordered by their scheduling priorities that are based on upward ranking. Basically, the upward rank of a task $v_i$ is the length of the critical path from $v_i$ to the exit task, including the computation time of task $v_i$. Let $pri(v_i)$ be the priority value of task $v_i$ and be recursively defined by:
> $$
> pri\left(v_{i}\right)=\left\{\begin{array}{ll}{\overline{w\left(v_{i}\right)}+\max\limits_{v_{j} \in \operatorname{succ}\left(v_{i}\right)}\left[\overline{\mathcal{c}\left(e_{i j}\right)}+pri\left(v_{j}\right)\right]} & { \text { if } v_{i} \neq v_{e x i t}} \\ \overline{w\left(v_{i}\right)} {} & {\text { if } v_{i} \equiv v_{e x i t}}\end{array}\right.
> $$
> where $\overline{w(v_i)}$ is the average execution time of task $v_i$ and $\overline{c(e_{ij})}$ is the average data transfer time between two tasks $v_i$ and $v_j$. They are computed by:
> $$
> \begin{gather} \overline{w(v_{i})}=\frac{w_{i}}{\overline{W}} \\  \overline{c\left(e_{i j}\right)} =\frac{c_{i j}}{\overline{B W}} \end{gather}
> $$
> with $\overline{W}$ is the average processing rate of all processors and $\overline{BW}$ is the average transfer rate or bandwidth among all processors.

**C.建议方法**

给定任务图$ V = \{v1，v2，...，v_n \} $和处理器图$ P =(N,D)$，我们考虑选择最合适的时间表来执行任务。我们的方法分为两个阶段：

1）*确定任务优先级：*在此阶段，根据任务的调度优先级对任务进行排序，这些调度优先级基于向上排序。基本上，任务$ v_i $的向上排名是从$ v_i $到退出任务的关键路径的长度，包括任务$ v_i $的计算时间。令$ pri(v_i)$为任务$ v_i $的优先级值，并通过以下方式递归定义：
$$
pri\left(v_{i}\right)=\left\{\begin{array}{ll}{\overline{w\left(v_{i}\right)}+\max\limits_{v_{j} \in \operatorname{succ}\left(v_{i}\right)}\left[\overline{\mathcal{c}\left(e_{i j}\right)}+pri\left(v_{j}\right)\right]} & { \text { if } v_{i} \neq v_{e x i t}} \\ \overline{w\left(v_{i}\right)} {} & {\text { if } v_{i} \equiv v_{e x i t}}\end{array}\right.
$$
其中$\overline{w(v_i)}$是任务$v_i$的平均处理时间，$\overline{c(e_{ij})}$是任务$v_i$和$v_j$之间的平均数据传输时间，他们被计算为：
$$
\begin{gather} \overline{w(v_{i})}=\frac{w_{i}}{\overline{W}} \\  \overline{c\left(e_{i j}\right)} =\frac{c_{i j}}{\overline{B W}} \end{gather}
$$
其中$\overline{W}$是所有处理器的平均处理率，$\overline{BW}$是所有处理器之间的平均传输率或带宽。

> *2) Selecting the most appropriate node to execute each task:* In this phase, the two parameters Earliest Start Time (EST) and Earliest Finish Time (EFT) need to be defined. A task $v_i$ cannot begin its execution until all its inputs have been available. Let $t_{dr}(v_i)$ be the time when all input data of $v_i$ is ready to be transfered to the selected node for executing the task $v_i$. It is also the time when the last preceding task of $v_i$ is finished. Thus $t_{dr}(v_i)$ is defined by:
> $$
> t_{dr}(v_i)=\max_{v_j \in pred(v_i),P_m \in N} \left[ t_f(v_j,P_m) \right]
> $$
> where $t_f(v_j,P_m)$ is the finish time of task $v_j$ on node $P_m$. For the entry task, $t_{dr}(v_{entry}) = 0$.

*2）选择最合适的节点来执行每个任务:* 在此阶段，需要定义两个参数最早开始时间（EST）和最早结束时间（EFT）。在所有输入可用之前，任务$ v_i $无法开始执行。设$ t_ {dr}(v_i)$为$ v_i $的所有输入数据准备好传输到所选节点以执行任务$ v_i $的时间。这也是$ v_i $的最后一个前置任务完成的时间。因此，$ t_ {dr}（v_i）$定义为：
$$
t_{dr}(v_i)=\max_{v_j \in pred(v_i),P_m \in N} \left[ t_f(v_j,P_m) \right]
$$
其中$t_f(v_j,P_m)$是任务$v_j$在节点$P_m$上的完成时间。对于入口任务，$t_{dr}(v_{entry}) = 0$

