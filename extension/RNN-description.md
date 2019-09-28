# 节选自RANDOM NEURAL NETWORK METHODS AND DEEP LEARNING 

## Model description

> Within the RNN system with $L$ neurons, all neurons communicate with each other with stochastic unit amplitude spikes while receiving external spikes. The potential of the $l\!\!-\!\!th$ neuron, denoted by $k(t) \ge 0$, is dynamically changing in continuous time, and the $l\!\!-\!\!th$ neuron is said to be excited if its potential $k(t)$ is larger than zero. An excitatory spike arrival to the $l\!\!-\!\!th$ neuron increases its potential by $1$, denoted by $k(t+) ← k(t) + 1$; while an inhibitory spike arrival decreases its potential by $1$ if it is larger than zero, denoted by $k(t+) ← max(k(t) − 1, 0)$, where $max(a, b)$ produces the larger element between $a$ and $b$.

在一个RNN系统内部有L个神经元，在接受到外部脉冲时，所有的神经元都与其他神经元以随机单元振幅脉冲的方式通信。第l个神经元的潜力，记为$k(t) \ge 0$，它会在连续时间内被动态改变，并且第l个神经元被称为兴奋，如果它的$k(t)$大于0的话。一个兴奋脉冲到达第l个神经元时会使他的潜力增加$1$，记为$k(t+) ← k(t) + 1$；当一个抑制脉冲到达时会使它的潜力减$1$（如果潜力大于$1$的话），记为$k(t+) ← max(k(t) − 1, 0)$，其中$max(a,b)$返回元素$a$和$b$中大的那个。

