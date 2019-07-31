# G-Networks and the Modeling of Adversarial Agents

> Abstract. As a result of the structure and content transformation of an evolving society, many large scale autonomous systems emerged in diverse areas such as biology, ecology or finance. Inspired by the desire to better understand and make the best out of these systems, we propose an approach which builds stochastic mathematical models, in particular G-networks models, that allow the efficient representation of systems of agents and offer the possibility to analyze their behavior using mathematics. This approach is capable of modelling the system at different abstraction levels, both in terms of the number of agents and the size of the geographical location. We demonstrate our approach with some urban military planning scenarios and the results suggest that this approach has tackled the problem in modelling autonomous systems at low computational cost. Apart from offering the numerical estimates of the outcome, the approach helps us identify the characteristics that impact the system most and allows us to compare alternative strategies.
>
> Keywords: mathematical modelling, G-Networks, military strategy and planning, multi-agent systems.

摘要。由于不断发展的社会的结构和内容转变，许多大型自治系统出现在生物学，生态学或金融学等不同领域。受到更好地理解并充分利用这些系统的愿望的启发，我们提出了一种方法，该方法构建随机数学模型，特别是G网络模型，允许代理系统的有效表示，并提供分析其行为的可能性用数学。该方法能够在不同的抽象级别上对系统进行建模，包括代理的数量和地理位置的大小。我们用一些城市军事规划方案展示了我们的方法，结果表明这种方法解决了以低计算成本建模自治系统的问题。除了提供结果的数值估计之外，该方法还有助于我们确定最能影响系统的特征，并允许我们比较替代策略。

## 1 Introduction

> As a society evolves, its structure and content transform accordingly to reflect and address its needs. As a result, more and more large scale autonomous systems occur in various forms in the surrounding world, from diverse areas of study such as biology, ecology, finance or transportation. Large scale systems have been traditionally characterized by a large number of variables, nonlinearities and uncertainties. As an example taken from biology, a human body, where organs, containing billions of cells, perform different functions that contribute towards the operating of the body can be seen as a large scale system. Inspired by the desire to better understand and utilize the environment, we study such systems and hope to gain insights, predict the future and control them partially if not fully.
>
> There have been many attempts to model large scale systems, such as building differential equations or with simulations [1-5]. However the sheer complexity and diversity of large scale systems make them difficult to be described and modelled, and it is even more difficult to provide numerical predictions of the underlying processes of such systems. To tackle these problems, we propose to use a stochastic approach, in particular G-networks [6-10], to model the individuals of the same nature collectively. In doing so, the computational complexity is greatly reduced. Another innovative aspect of our approach is that it is able to model systems with multiple geographical locations at different levels of abstraction. With the approach, we aim to provide insights into systems in terms of their performance and behaviours, to identify the parameters which strongly influence them, and to evaluate how well an individual’s task can be achieved and, therefore compare the effects of alternative strategies.
>
> As presented in [13-17], our approach has many application areas, such as military planning, systems biology and computer networking. In this paper, we use strategic military planning in urban scenarios as an example to demonstrate our approach. We describe the systems of interest, the mathematical model, and the chosen scenarios. We illustrate two methods that we use in dealing with the situations where complete or incomplete world knowledge is available. To validate our model, we compare its results with those obtained from a simulator [11, 12] that was built in our group. We will briefly discuss the differences between these two approaches, and analyze the discrepancy between the results. The paper concludes with a discussion of potential extensions to the model.

随着社会的发展，其结构和内容也相应地转变，以反映和满足其需求。结果，越来越多的大规模自治系统以各种形式出现在周围世界中，来自生物学，生态学，金融学或运输学等不同领域。大规模系统传统上以大量变量，非线性和不确定性为特征。作为从生物学中获取的一个例子，人体，其中包含数十亿个细胞的器官执行有助于身体操作的不同功能，可被视为大规模系统。受到更好地理解和利用环境的愿望的启发，我们研究了这样的系统，并希望获得见解，预测未来并部分控制它们（如果不是完全的话）。

已经有许多尝试对大规模系统进行建模，例如建立微分方程或模拟[1-5]。然而，大规模系统的绝对复杂性和多样性使得它们难以被描述和建模，并且甚至更难以提供这种系统的基础过程的数值预测。为了解决这些问题，我们建议使用随机方法，特别是G网络[6-10]来集体模拟相同性质的个体。这样做，计算复杂性大大降低。我们方法的另一个创新方面是它能够在不同的抽象层次上对具有多个地理位置的系统进行建模。通过这种方法，我们的目标是提供系统在性能和行为方面的见解，识别对其有很大影响的参数，并评估个人任务的实现程度，从而比较替代策略的效果。

如[13-17]所述，我们的方法有许多应用领域，如军事规划，系统生物学和计算机网络。在本文中，我们以城市场景中的战略军事规划为例来说明我们的方法。我们描述了感兴趣的系统，数学模型和所选择的场景。我们举例说明了两种方法，用于处理可获得完整或不完整世界知识的情况。为了验证我们的模型，我们将其结果与从我们小组中构建的模拟器[11,12]获得的结果进行比较。我们将简要讨论这两种方法之间的差异，并分析结果之间的差异。本文最后讨论了模型的潜在扩展。

## 2 System Descriptions

> As an example of a potential application, we consider a closed system containing N distinct geographic locations and a set of C agent classes. Locations may have obstacles that an agent cannot physically enter, such as stretches of water, trees, buildings and so on. Obstacles depend of course on the physical objects that the agents represent (e.g. land and air vehicles will have different kinds of obstacles). At the moment, we do not take the local minimum problem into consideration and we assume all obstacles in the terrain are convex in shape. 
>
> In these systems, agents take actions to achieve their goals, which are reflected by their motions and behaviors. A goal, be it stationary or motion-oriented, attracts agents to move towards it. A stationary goal is a specific location, whereas a motionoriented goal refers to the situation where an agent itself is the goal (target) of others. Agents either protect or destroy their motion-oriented goals. To achieve this, agents might need to cooperate or compete with others in the system. The difference in nature of the goals results in agents belonging to different adversary teams. Teams in the same group collaborate with each other to achieve their goals, while those in adversarial groups would exhibits competing behaviors to prevent others accomplishing their goals.
>
> Motion in the system is a result of forces exercised by the goal and agents. There are three types of forces in our system: attractive, repulsive and long-range attractive and short-range repulsive. A straightforward example of an attractive force would be the force that a stationary goal (i.e. the destination) applies on an agent. A repulsive force can be interpreted as the tension of moving away. For example, if agent D’s aim is to destroy agent B, then agent B applies an attractive force on D. On the other hand, agent D exercises a repulsive force on B. A long-range attractive and shortrange repulsive force makes a group of agents stay together and keeps their distance at the same time. Thus if the agents are too close, repulsive forces are applied, otherwise, attractive forces are applied.

作为潜在应用程序的示例，我们考虑一个包含N个不同地理位置和一组C代理类的封闭系统。地点可能有代理人无法进入的障碍物，例如水域，树木，建筑物等。障碍当然取决于代理人所代表的物理对象（例如陆地和空中交通工具将具有不同类型的障碍物）。目前，我们没有考虑局部最小问题，我们假设地形中的所有障碍物都是凸形的。

在这些系统中，代理人采取行动来实现他们的目标，这些目标通过他们的动作和行为来反映。一个目标，无论是静止的还是以动作为导向的，都会吸引代理商向目标迈进。固定目标是特定位置，而面向动作的目标是指代理本身是其他人的目标（目标）的情况。代理商要么保护或破坏他们以运动为导向的目标。为实现此目的，代理可能需要与系统中的其他人合作或竞争。目标性质的差异导致代理人属于不同的对手团队。同一组中的团队相互协作以实现他们的目标，而对抗组中的团队将展示竞争行为以阻止其他人实现他们的目标。

系统中的运动是目标和代理人所施加的力量的结果。我们的系统有三种类型的力量：吸引力，排斥性和远程吸引力和短程排斥力。吸引力的直接例子是静止目标（即目的地）施加在代理上的力。排斥力可以解释为离开的紧张。例如，如果药剂D的目的是破坏药剂B，则药剂B在D上施加吸引力。另一方面，药剂D在B上施加排斥力。远程吸引力和短程排斥力使得一组特工们待在一起，同时保持距离。因此，如果试剂太靠近，则施加排斥力，否则施加吸引力。

## 3 The Mathematical Model

> Let $i = g(t, c, k)$ denote the location at time $t$ of agent $k$ belonging to team $c$. The location $i$ may be a single variable or a vector, depending on the geographic representation that is being used, e.g. the$ (x, y, z)$ coordinates of a location on a map, where $z$ may represent elevation when this is relevant. Thus in a two-dimensional coordinate space, a location will be denoted by $i=(x(i),y(i))$ and a neighboring location will be denoted by some $j=i+d$ where $d ∈{(0,0), (±1,0), (0,±1), (±1,±1)}$. It is assumed that each agent has an initial location denoted by $S(c, k)$, and it may have (though this is not necessary) a final destination $D(c, k)$. We also assume that agents may die as a result of adversarial effects, or for other reasons, in which case they are relocated to “heaven” denoted by $H$. For the purpose of this model, we assume that there is justo ne heaven for everyone.
> 
> The mathematical model we develop aims at being able to compute, over a large number of experiments, quantities such as the probability $q(i, c, k)$ that agent $k$ of team $c$ is in location $i$. Such probabilities will also be used to compute indirectly the average time it may take certain agents to reach specific locations. The approach we take is based on constructing an ergodic model, i.e. one which has a stationary probability distribution, so that:
> 
>$$
> q(i, c, k)=\lim _{t \rightarrow \infty} \operatorname{prob}[g(t, c, k)=i]
>$$

设$ i = g(t,c,k)$表示属于团队$ c $的代理商$ k $的$ t $位置。位置$ i $可以是单个变量或向量，这取决于正在使用的地理表示，例如，地图上某个位置的$(x,y,z)$坐标，其中$ z $可能代表相关时的高程。因此，在二维坐标空间中，位置将由$ i =(x(i),y(i))$表示，并且邻近位置将由某些$ j = i + d $表示，其中$d∈{(0,0),(±1,0),(0，±1),(±1，±1)} $。假设每个代理具有由$ S(c，k)$表示的初始位置，并且它可能具有（尽管这不是必需的）最终目的地$ D(c，k)$。我们还假设代理人可能因对抗性影响而死亡，或者出于其他原因，在这种情况下，他们被重新安置到由H $表示的“天堂”。为了这个模型的目的，我们假设每个人都有天堂。

我们开发的数学模型旨在能够在大量实验中计算数量，例如$ q（i，c，k）$代理$ k $团队$ c $的位置$ i $。这些概率还将用于间接计算某些代理可能需要到达特定位置的平均时间。我们采用的方法是基于构建遍历模型，即具有静态概率分布的模型，以便：
$$
q(i, c, k)=\lim _{t \rightarrow \infty} \operatorname{prob}[g(t, c, k)=i]
$$

