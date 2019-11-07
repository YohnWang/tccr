# Resource Management with Deep Reinforcement Learning

> Abstract– Resource management problems in systems and networking often manifest as difficult online decision making tasks where appropriate solutions depend on understanding the workload and environment. Inspired by recent advances in deep reinforcement learning for AI problems, we consider building systems that learn to manage resources directly from experience. We present DeepRM, an example solution that translates the problem of packing tasks with multiple resource demands into a learning problem. Our initial results show that DeepRM performs comparably to state-oftheart heuristics, adapts to different conditions, converges quickly, and learns strategies that are sensible in hindsight.

摘要–系统和网络中的资源管理问题通常表现为困难的在线决策任务，其中适当的解决方案取决于对工作量和环境的理解。受AI问题深度强化学习的最新进展启发，我们考虑构建可直接从经验中学习管理资源的系统。我们提供DeepRM，这是一个示例解决方案，可以将具有多种资源需求的打包任务的问题转换为学习问题。我们的初步结果表明，DeepRM与最新的启发式算法具有可比性，可以适应不同的条件，可以快速收敛，并且可以学习事后明智的策略。

## 1. INTRODUCTION

> Resource management problems are ubiquitous in computer systems and networks. Examples include job scheduling in compute clusters [17], bitrate adaptation in video streaming [23, 39], relay selection in Internet telephony [40], virtual machine placement in cloud computing [20, 6], congestion control [38, 37, 13], and so on. The majority of these problems are solved today using meticulously designed heuristics. Perusing recent research in the field, the typical design flow is: (1) come up with clever heuristics for a simplified model of the problem; and (2) painstakingly test and tune the heuristics for good performance in practice. This process often has to be repeated if some aspect of the problem such as the workload or the metric of interest changes.
>
> We take a step back to understand some reasons for why real world resource management problems are challenging:
>
> 1. The underlying systems are complex and often impossible to model accurately. For instance, in cluster scheduling, the running time of a task varies with data locality,server characteristics, interactions with other tasks, and interference on shared resources such as CPU caches, network bandwidth, etc [12, 17].
> 2. Practical instantiations have to make online decisions with noisy inputs and work well under diverse conditions. A video streaming client, for instance, has to choose the bitrate for future video chunks based on noisy forecasts of available bandwidth [39], and operate well for different codecs, screen sizes and available bandwidths (e.g., DSL vs. T1).
> 3. Some performance metrics of interest, such as tail performance [11], are notoriously hard to optimize in a principled manner.

资源管理问题在计算机系统和网络中无处不在。示例包括计算集群中的作业调度[17]，视频流中的比特率自适应[23、39]，互联网电话中的中继选择[40]，云计算中的虚拟机放置[20、6]，拥塞控制[38、37，13]，等等。今天，这些问题中的大多数都是使用精心设计的启发式方法解决的。仔细研究该领域的最新研究，典型的设计流程是：（1）提出了巧妙的启发式方法来简化问题模型；（2）认真测试和调整启发式方法，以在实践中取得良好的性能。如果问题的某些方面（例如工作量或兴趣度量）发生变化，则通常必须重复此过程。

我们退后一步来了解现实世界中的资源管理问题为何具有挑战性的一些原因：

1. 基础系统很复杂，通常无法准确建模。例如，在集群调度中，任务的运行时间随数据位置，服务器特性，与其他任务的交互以及对共享资源（如CPU缓存，网络带宽等）的干扰而变化[12，17]。
2. 实际实例化必须做出带有噪声输入的在线决策，并且必须在各种条件下都能正常工作。例如，视频流客户端必须根据对可用带宽的嘈杂预测来选择未来视频块的比特率[39]，并且必须在不同的编解码器，屏幕尺寸和可用带宽（例如DSL与T1）之间运行良好。
3. 众所周知，一些令人感兴趣的性能指标，例如尾翼性能[11]，很难以有原则的方式进行优化。

> In this paper, we ask if machine learning can provide a viable alternative to human-generated heuristics for resource management. In other words: Can systems learn to manage resources on their own?
>
> This may sound like we are proposing to build Skynet [1], but the recent success of applying maching learning to other challenging decision-making domains [29, 33, 3] suggests that the idea may not be too far-fetched. In particular, Reinforcement Learning (RL) (§2) has become an active area in machine learning research [30, 28, 32, 29, 33]. RL deals with agents that learn to make better decisions directly from experience interacting with the environment. The agent starts knowing nothing about the task at hand and learns by reinforcement — a reward that it receives based on how well it is doing on the task. RL has a long history [34], but it has recently been combined with Deep Learning techniques to great effect in applications such as playing video games [30], Computer Go [33], cooling datacenters [15], etc.

在本文中，我们询问机器学习是否可以为人为启发式资源管理提供一种可行的替代方法。换句话说：系统是否可以学习自行管理资源？

听起来好像我们正在提议构建天网[1]，但是最近将行进式学习应用于其他具有挑战性的决策领域[29、33、3]的成功表明，这个想法可能不会太牵强。特别是，强化学习（RL）（§2）已成为机器学习研究中的活跃领域[30，28，32，29，33]。RL与能够直接从与环境互动的经验中学习做出更好决策的代理商打交道。代理开始对手头的任务一无所知，并通过强化学习—基于其在该任务上做得如何的奖励。RL历史悠久[34]，但最近已与深度学习技术相结合，在诸如玩视频游戏[30]，Computer Go [33]，冷却数据中心[15]等应用中发挥了巨大作用。

> Revisiting the above challenges, we believe RL approaches are especially well-suited to resource management systems. First, decisions made by these systems are often highly repetitive, thus generating an abundance of training data for RL algorithms (e.g., cluster scheduling decisions and the resulting performance). Second, RL can model complex systems and decision-making policies as deep neural networks analogous to the models used for game-playing agents [33, 30]. Different “raw” and noisy signals1 can be incorporated as input to these neural networks, and the resultant strategy can be used in an online stochastic environment. Third, it is possible to train for objectives that are hard-to-optimize directly because they lack precise models if there exist reward signals that correlate with the objective. Finally, by continuing to learn, an RL agent can optimize for a specific workload (e.g., small jobs, low load, periodicity) and be graceful under varying conditions.
>
> As a first step towards understanding the potential of RL for resource management, we design (§3) and evaluate (§4) DeepRM, a simple multi-resource cluster scheduler. DeepRM operates in an online setting where jobs arrive dynamically and cannot be preempted once scheduled. DeepRM learns to optimize various objectives such as minimizing average job slowdown or completion time. We describe the model in §3.1 and how we pose the scheduling task as an RL problem in §3.2. To learn, DeepRM employs a standard policy gradient reinforcement learning algorithm [35] described in §3.3.

回顾上述挑战，我们认为RL方法特别适合于资源管理系统。首先，由这些系统做出的决策通常是高度重复的，从而为RL算法生成了大量的训练数据（例如，集群调度决策和所产生的性能）。其次，RL可以将复杂的系统和决策策略建模为类似于用于游戏代理的模型的深层神经网络[33，30]。可以将不同的“原始”和嘈杂信号1合并为这些神经网络的输入，并且所得策略可以在在线随机环境中使用。第三，可以训练难以直接优化的目标，因为如果存在与目标相关的奖励信号，则它们缺乏精确的模型。最后，通过继续学习，RL代理可以针对特定的工作负载（例如，小工作，低负载，周期性）进行优化，并在变化的条件下保持优雅。

作为了解RL在资源管理方面的潜力的第一步，我们设计（§3）和评估（§4）DeepRM，它是一种简单的多资源集群调度程序。DeepRM在在线设置下运行，其中作业动态到达，并且一旦计划就无法抢占。DeepRM学会优化各种目标，例如最大程度地减少平均作业速度或完成时间。我们将在第3.1节中描述模型，并在第3.2节中将调度任务作为RL问题来处理。要学习，DeepRM采用第3.3节中描述的标准策略梯度强化学习算法[35]。

> We conduct simulated experiments with DeepRM on a synthetic dataset. Our preliminary results show that across a wide range of loads, DeepRM performs comparably or better than standard heuristics such as Shortest-Job-First (SJF) and a packing scheme inspired by Tetris [17]. It learns strategies such as favoring short jobs over long jobs and keeping some resources free to service future arriving short jobs directly from experience. In particular, DeepRM does not require any prior knowledge of the system’s behavior to learn these strategies. Moreover, DeepRM can support a variety of objectives just by using different reinforcement rewards.
>
> Looking ahead, deploying an RL-based resource manager in real systems has to confront additional challenges. To name a few, simple heuristics are often easier to explain, understand, and verify compared to an RL-based scheme. Heuristics are also easier to adopt incrementally. Nevertheless, given the scale and complexity of many of the resource management problems that we face today, we are enticed by the possibility to improve by using reinforcement learning.

我们在综合数据集上使用DeepRM进行了模拟实验。我们的初步结果表明，在广泛的负载范围内，DeepRM的性能与标准启发式算法（例如，最短工作优先（SJF）和受Tetris启发的打包方案）相当或更好。它学习一些策略，例如从长期的工作中偏爱短期的工作，以及保留一些资源直接根据经验来为将来到达的短期工作提供服务。特别是，DeepRM不需要任何有关系统行为的先验知识即可学习这些策略。而且，DeepRM可以通过使用不同的强化奖励来支持各种目标。

展望未来，在实际系统中部署基于RL的资源管理器必须面对其他挑战。仅举几例，与基于RL的方案相比，简单的启发式方法通常更易于解释，理解和验证。启发式方法也更容易逐步采用。但是，考虑到我们当今面临的许多资源管理问题的规模和复杂性，我们对使用强化学习来改善的可能性很感兴趣。

## 2. BACKGROUND

> We briefly review Reinforcement Learning (RL) techniques that we build on in this paper; we refer readers to [34] for a detailed survey and rigorous derivations.
>
> **Reinforcement Learning.** Consider the general setting shown in Figure 1 where an agent interacts with an environment. At each time step $t$, the agent observes some state $s_t$, and is asked to choose an action $a_t$. Following the action, the state of the environment transitions to $s_{t+1}$ and the agent receives reward $r_t$. The state transitions and rewards are stochastic and are assumed to have the Markov property; i.e. the state transition probabilities and rewards depend only on the state of the environment $s_t$ and the action taken by the agent $a_t$.
>
>  It is important to note that the agent can only control its actions, it has no apriori knowledge of which state the environment would transition to or what the reward may be. By interacting with the environment, during training, the agent can observe these quantities. The goal of learning is to maximize the expected cumulative discounted reward: $\mathbb{E}[\sum_{t=0}^\infin \gamma^tr_t]$, where   $\gamma \in (0,1]$ is a factor discounting future rewards.





> **Policy.** The agent picks actions based on a policy, defined as a probability distribution over actions $\pi$ : $\pi(s,a) \to [0,1]$; $\pi(s,a)$ is the probability that action $a$ is taken in state $s$. In most problems of practical interest, there are many possible {state, action} pairs; up to $2^{100}$ for the problem we consider in this paper (see §3). Hence, it is impossible to store the policy in tabular form and it is common to use function approximators [7, 27]. A function approximator has a manageable number of adjustable parameters, $\theta$; we refer to these as the policy parameters and represent the policy as $\pi_{\theta}(s,a)$. The justification for approximating the policy is that the agent should take similar actions for “close-by" states.
>
> Many forms of function approximators can be used to represent the policy. For instance, linear combinations of features of the state/action space (i.e., $\pi_{\theta}(s,a) = \theta^T \phi(s,a)$) are a popular choice. Deep Neural Networks (DNNs) [18] have recently been used successfully as function approximators to solve large-scale RL tasks [30, 33]. An advantage of DNNs is that they do not need hand-crafted features. Inspired by these successes, we use a neural network to represent the policy in our design; the details are in §3.





> **Policy gradient methods.** We focus on a class of RL algorithms that learn by performing gradient-descent on the policy parameters. Recall that the objective is to maximize the expected cumulative discounted reward; the gradient of this objective given by [34]:
> $$
> \nabla_{\theta} \mathbb{E}_{\pi_{\theta}}\left[\sum_{t=0}^{\infty} \gamma^{t} r_{t}\right]=\mathbb{E}_{\pi_{\theta}}\left[\nabla_{\theta} \log \pi_{\theta}(s, a) Q^{\pi_{\theta}}(s, a)\right]
> $$
> Here, $Q^{\pi\theta}(s,a)$ is the expected cumulative discounted reward from (deterministically) choosing action $a$ in state $s$, and subsequently following policy $\pi_\theta$. The key idea in policy gradient methods is to estimate the gradient by observing the trajectories of executions that are obtained by following the policy. In the simple Monte Carlo Method [19], the agent samples multiple trajectories and uses the empirically computed cumulative discounted reward, $v_t$, as an unbiased estimate of $Q^{\pi\theta}(s_t,a_t)$. It then updates the policy parameters via gradient descent:
> $$
> \theta \leftarrow \theta+\alpha \sum_{t} \nabla_{\theta} \log \pi_{\theta}\left(s_{t}, a_{t}\right) v_{t}
> $$
> where $\alpha$ is the step size. This equation results in the well-known REINFORCE algorithm [35], and can be intuitively understood as follows. The direction $\nabla_{\theta} \log \pi_{\theta}\left(s_{t}, a_{t}\right)$ gives how to change the policy parameters in order to increase $\pi_\theta(s_t,a_t)$ (the probability of action $a_t$ at state $s_t$). Equation 2 takes a step in this direction; the size of the step depends on how large is the return $v_t$. The net effect is to reinforce actions that empirically lead to better returns. In our design, we use a slight variant [32] that reduces the variance of the gradient estimates by subtracting a baseline value from each return $v_t$. More details follow.