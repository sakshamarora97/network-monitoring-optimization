# network-monitoring-optimization
Course Project for ISYE 6333 Operations Research 1

# Problem Background
Ensuring the security of critical infrastructures such as water distribution networks is crucial for
the welfare and prosperity of our society. Such infrastructure networks may span huge geographical
areas, and are inherently vulnerable to disruptions. In recent years, numerous incidents have been
reported that highlight the inherent vulnerability of infrastructure networks (website). Operations
Research can provide new solutions to help the water utilities to proactively recognize the security
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

<img width="385" alt="image" src="https://github.com/sakshamarora97/network-monitoring-optimization/assets/62840042/8620a0f0-5a3a-4a70-8097-3531259b31bd">

# Questions:
### (a) (10 points) In this first question, we want to determine the minimum number of sensors, and where to locate them, so that if any pipe bursts, then at least one sensor will detect it. Formulate this problem as an integer program.
### (b) (10 points) Code and solve your optimization model. How many sensors are needed to detect any pipe burst?
### (c) (10 points) Next, we suppose instead that the network operator possesses b pressure sensors (typically less than the number of sensors found in part (b)). We also assume that each pipe independently bursts with probability 0.1. Formulate an integer program that determines the location of the b sensors that maximizes the expected number of pipe bursts that are detected.
### (d) (10 points) Code and solve the optimization model formulated in part (c) for b ∈ {0, . . . , 20} using the Gurobi solver. Plot and analyze the optimal value of the problem as a function of the number of sensors b.
### (e) (15 points) Instead, the operator wants to investigate a faster solution approach, where sensor locations are sequentially (and myopically) selected. Specifically, the operator takes their first sensor, and places it at the node that detects the maximum expected number of pipe bursts. Then, the operator takes the second sensor, and places it at the node that detects the maximum 2 expected number of pipe bursts that were not previously detected, and so on until all sensors are positioned. Code this iterative algorithm, and plot the resulting expected number of pipe bursts that are detected by that solution, as a function of the number of sensors available, b ∈ {0, . . . , 20}. Compare this plot with the one obtained in part (d).
### (f) (15 points) It turns out that some pipes are more critical than others, depending on their locations. For example, a pipe burst next to a hospital will be more problematic than a pipe burst in a remote area. Each pipe e ∈ E is assigned a criticality level we ∈ [0, 1]. The higher we is, the more critical pipe e is. The goal of the network operator is to position their b sensors as to minimize the highest criticality of a pipe that is not detected by any sensor. Formulate
this problem as an IP. 
### (g) (10 points) Code and solve the optimization model formulated in part (f) for b ∈ {0, . . . , 20} using Gurobi Solver. Plot and analyze the optimal value of the problem as a function of the number of sensors b.
### (h) (20 points) Present your project. Your presentation should introduce the problem (for the students who have not worked on this project), and describe your results to the questions in a clean and organized manner.
