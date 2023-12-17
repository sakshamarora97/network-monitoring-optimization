# Problem Background
Ensuring the security of critical infrastructures such as water distribution networks is crucial for
the welfare and prosperity of our society. Such infrastructure networks may span huge geographical
areas, and are inherently vulnerable to disruptions. In recent years, numerous incidents have been
reported that highlight the inherent vulnerability of infrastructure networks (website). 

Operations Research can provide new solutions to help the water utilities to proactively recognize the security
risks to their infrastructure, and develop specific capabilities to reduce them.
In this project, a water utility company, and more specifically a network operator, is interested
in allocating pressure sensors on nodes in order to detect pipe bursts in its water distribution
network. The network is located in Kentucky, and is composed of 1123 pipes and 811 nodes. It
provides 2.09 million gallons of water per day to its 5,010 customers. The layout of the water
distribution network is given in Figure 1.

We denote V the set of 811 nodes/sensor locations, and E the set of 1123 network pipes.
Each node can receive at most one sensor. You will be given a detection matrix, denoted F ∈
{0, 1}|E|×|V|, that represents the sensing capabilities of the pressure sensors. F is a binary matrix
of size |E| × |V| = 1123 × 811, and is such that fe,v = 1 if a sensor placed at location v ∈ V can
detect a burst of pipe e ∈ E.

<img width="400" alt="image" src="https://github.com/sakshamarora97/network-monitoring-optimization/assets/62840042/8620a0f0-5a3a-4a70-8097-3531259b31bd">

# Questions:
#### (a) In this first question, we want to determine the minimum number of sensors, and where to locate them, so that if any pipe bursts, then at least one sensor will detect it. Formulate this problem as an integer program.

**Decision Variable :**

$$
\begin{aligned}
& x_v= \begin{cases}1 & \text {: sensor is placed at node $v$ } \forall \ v \in \mathcal{V} \\
0 & \text {: otherwise}\end{cases} \end{aligned} \\
$$

**Objective Function :** 

Minimize the number of sensors so that if any pipe bursts, then at least one sensor will detect it.

$$
min \quad \sum_{v=1}^{811} \ x_v \\
$$

**Constraints:**
* Each pipe should be detected by at least one sensor

$$ 
 \quad \sum_{v=1}^{811} \ f_{e,v} x_v >= 1  \quad \forall \ e \in \mathcal{E}\\\\
$$

#### (b) Code and solve your optimization model. How many sensors are needed to detect any pipe burst?

19.0

#### (c) Next, we suppose instead that the network operator possesses b pressure sensors (typically less than the number of sensors found in part (b)). We also assume that each pipe independently bursts with probability 0.1. Formulate an integer program that determines the location of the b sensors that maximizes the expected number of pipe bursts that are detected.

*Given :*

We are given a binary detection matrix $F \in \{{0,1}\}^{|{\mathcal{E}| \times |\mathcal{V}}|}$ that represents the sensing capabilities of the pressure
sensors. The dimensions of this matrix are 1123 x 811, where every element $f_{e,v} = 1$ if a sensor placed at location $v \in \mathcal{V}$ can detect a burst of pipe $e \in \mathcal{E}$.

*Problem Formulation*

Let $Y_e$ be a discrete random variable which denotes whether pipe $e$ bursts. Thus we have, 

$$
\begin{aligned}
& p_{Y_e}(y)= \begin{cases}0.1 & \text {:$y = 1$ } \\
0.9 & \text {:$y = 0$}\end{cases} \end{aligned}
$$

Let $p_e$ be an integer denoting if pipe $e$ is detectable by any sensor. 

$$
\begin{aligned}
& p_e= \begin{cases}1 & \text {: pipe e is detected by any sensor } \\
0 & \text {: otherwise}\end{cases} \end{aligned}
$$

Let $D_e$ be another discrete random variable which denotes whether pipe burst of $e$ will be detected.
  
Thus, we know,

$$
\begin{aligned}
& p_{D_e|Y_e=1}(d)= \begin{cases}p_e & \text {:$d = 1$ } \\
1 - p_e & \text {:$d = 0$}\end{cases} \end{aligned}
$$
$$
\begin{aligned}
& p_{D_e|Y_e=0}(d)= \begin{cases}0 & \text {:$d = 1$ } \\
1 & \text {:$d = 0$}\end{cases} \end{aligned}
$$

From total probability theorem we can write,

$$
\begin{aligned}
& p_{D_e}(d=1) = p_{D_e|Y_e=0}(d=1) p_{Y_e}(y=0) + p_{D_e|Y_e=1}(d=1) p_{Y_e}(y=1)   \\
& p_{D_e}(d=0) = p_{D_e|Y_e=0}(d=0) p_{Y_e}(y=0) + p_{D_e|Y_e=1}(d=0) p_{Y_e}(y=1)   \\
\end{aligned}
$$

Solving, we get,

$$
\begin{aligned}
& p_{D_e}(d)= \begin{cases}0.1p_e & \text {$d=1$ } \\
1- 0.1p_e & \text {$d=0$}\end{cases} \end{aligned}
$$

Now computing expectation of random variable $D_e$, we get

$$
\begin{aligned}
& E(D_e) = \sum_{d} \ d*p_{D_e}(d)\
E(D_e) & = 0.1p_e
\end{aligned}
$$

Now, our problem is to maximize expected number of pipe bursts detected, given b sensors
The expected number of pipe bursts is given by:

$$
\begin{aligned}
max \quad E(\sum_{e=1}^{1123} \ D_e)\\
max \quad \sum_{e=1}^{1123} \ E(D_e) & \text{(since $D_e$'s and $Y_e$'s are independent random variables)}\\
max \quad \sum_{e=1}^{1123} \ 0.1p_e
\end{aligned}
$$

**Decision Variable :**

$$
\begin{aligned}
& x_v = \begin{cases}1 & \text {: sensor is placed at node $\ v$ } \forall \ v \in \mathcal{V} \\
0 & \text {: otherwise}\end{cases} \\
& p_e = \begin{cases}1 & \text {: pipe $\ e$ is detectable by any sensor } \forall \ e \in \mathcal{E} \\
0 & \text {: otherwise}\end{cases} \end{aligned}
$$

**Objective Function :**
Maximize the expected number of pipe bursts that are detected

$$
max \quad \sum_{e=1}^{1123} \ 0.1p_e\\
$$

**Constraints:**

* Number of Sensors are limited to $b$

$$
\quad 
 \sum_{v=1}^{811} x_v=b \\
$$

* If a pipe is detected, then it should be detectable by at least one of the sensors

$$
p_e \leqslant \sum_{v=1}^{811} f_{e,v} x_v \quad \forall \ e \in \mathcal{E} \\
$$

#### (d) Code and solve the optimization model formulated in part (c) for b ∈ {0, . . . , 20} using the Gurobi solver. Plot and analyze the optimal value of the problem as a function of the number of sensors b.

<img width="800" alt="image" src="https://github.com/sakshamarora97/network-monitoring-optimization/assets/62840042/b067b1fd-b92a-4e7c-a66b-b93c9f497209">

#### (e) Instead, the operator wants to investigate a faster solution approach, where sensor locations are sequentially (and myopically) selected. Specifically, the operator takes their first sensor, and places it at the node that detects the maximum expected number of pipe bursts. Then, the operator takes the second sensor, and places it at the node that detects the maximum 2 expected number of pipe bursts that were not previously detected, and so on until all sensors are positioned. Code this iterative algorithm, and plot the resulting expected number of pipe bursts that are detected by that solution, as a function of the number of sensors available, b ∈ {0, . . . , 20}. Compare this plot with the one obtained in part (d).

<img width="800" alt="image" src="https://github.com/sakshamarora97/network-monitoring-optimization/assets/62840042/4cce06f3-d8aa-4d0b-86b8-29e1d446a0fb">


#### (f) It turns out that some pipes are more critical than others, depending on their locations. For example, a pipe burst next to a hospital will be more problematic than a pipe burst in a remote area. Each pipe e ∈ E is assigned a criticality level we ∈ [0, 1]. The higher we is, the more critical pipe e is. The goal of the network operator is to position their b sensors as to minimize the highest criticality of a pipe that is not detected by any sensor. Formulate this problem as an IP. 

**Decision Variable :**

$$
\begin{aligned}
& x_v = \begin{cases}1 & \text {: sensor is placed at node $\ v$ } \forall \ v \in \mathcal{V} \\
0 & \text {: otherwise}\end{cases} \\
& p_e = \begin{cases}1 & \text {: pipe $\ e$ is detectable by any sensor } \forall \ e \in \mathcal{E} \\
0 & \text {: otherwise}\end{cases} \end{aligned}
$$

**Objective Function :**
We want to minimize the highest crticality of the pipe which are not detected by the placed sensors

$$
\min \quad \max _{\ e \in \mathcal{E}}\left(w_e\left(1-p_e\right)\right) \\
$$

Formulating minmax problem as a linear programming formulation: 

$$
\min \quad z \\
s.t.
\ \ z \geqslant w_e\left(1-p_e\right) \quad \forall \ e \in \mathcal{E} 
$$

**Constraints:**

* Total number of sensors are limited to $\ b$

$$
 \sum_{v=1}^{811} x_v=b \\
 $$

* If a pipe is detected, then it should be detectable by at least one of the sensors

$$
 p_e \leqslant \sum_{v=1}^{811} f_{e,v} x_v \quad \forall \ e \in \mathcal{E} \\
$$
  

#### (g) Code and solve the optimization model formulated in part (f) for b ∈ {0, . . . , 20} using Gurobi Solver. Plot and analyze the optimal value of the problem as a function of the number of sensors b.

<img width="800" alt="image" src="https://github.com/sakshamarora97/network-monitoring-optimization/assets/62840042/2a0bd04a-05c6-4ebc-9ed8-bd222004ea71">
