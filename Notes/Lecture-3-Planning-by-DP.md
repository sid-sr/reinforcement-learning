# RL Notes:

## Lecture 3:
---
* DP can be used to find the optimal policy, which exists for any MDP.
* Planning consists of control and prediction -> 2 different problems.
* Prediction is evaluation of a given policy for a given MDP -> can be done iteratively, to get a final value function.
* Control is choosing the right policy that maximises the reward.
* To get the optimal policy, start off with a random policy (say URP) then perform 2 steps: Evaluate it and then update the policy greedily based on the value function it generates.
* This 2 step process can be done repeatedly to get the optimal value function and hence the optimal policy.
* The cyclic process is: policy evaluation + policy improvement. This is policy iteration.
* Another method is to use value iteration. At each state, we inductively assume we know the optimal value of all the states from that state, and v* for that state is the v of the action that maximises the immediate reward + mean v* of all the other states.
* So in value iteration, we work backwards. Since we don't know which state is closest to the terminal state, we perform one step lookahead for all states.
* Policy iteration: iterate over the Bellman **expectation** equation (normal), in value iteration: iterate over the Bellman **optimality** equation.
* Value iteration does not use an explicit policy at each step, in fact intermediate value function values may not even correspond to some policy that exists.
* Same updates can be done to q values too, but it has higher time complexity.
* Extensions: In place value iteration, prioritised sweeping and real time DP.

DOUBT: Why value iteration is policy iteration with k = 1.