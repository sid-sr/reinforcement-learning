# RL Notes:

## Lecture 5:
---
* 2 methods for model free control: On-policy learning and Off-policy learning.
* Think of the same concept in planning/modeled system. The evaluation method (which is just iterative value updates) is converted into policy iteration where we just update the policy after an evaluation.
* Same concept here, the evaluation method in a model free environment is MC/TD. So just update the policy greedily after each MC/TD eval.
* Greedy policy updation cannot be done with state value functions (because they choose actions that maximise reward + prob*val of succesive states and we don't know the STP here) but they can be done with action value functions.
* Even though we have the value function for each state, we can't choose the action at that state which leads to that value.
* Similar to state value functions, using MC/TD we can find the Q pi (action value function) for each state action pair by finding the mean return for each (s, a) pair by sampling many episodes and tracking the returns.
* So the policy for each state is the action that maximises the Q(s, a) from that state.
* An issue with this greedy policy update is that it chooses greedily over the states we have sampled and this might not include all the states in the state space.
* To solve this, we need to ensure we explore to an extent in addition to always choosing the greedy action. This is called epsilon-greedy exploration.
* Epsilon here is the probability that we choose a random action for a state (for exploration), 1-epsilon is the chance that we choose the greedy action.
* All m actions have epsilon/m probability in our policy and the greedy action has an additional 1-epsilon chance of being chosen.
* Epsilon greedy policy updates will always improve the value (or at least be equal to) the old value function. 
* In MC we keep running episodes to find q pi, however we can start updating the policy at the end of each episode. (ie: our freshest estimate of the action value function). 
* In GLIE (Greedy in the Limit of Exploration), we ensure 2 properties: 1. all (s, a) pairs will be explored infinitely many times given infinitely many episodes. 2. The policy at the end (after an infinite number of episodes) must converge to a (full) greedy policy.
* One way to do this is to set epsilon to 1/num_episodes_seen. This ensures as the episodes go on, the exploration probability reduces and in the limit to infinity, we reach a greedy policy. 
* GLIE Monte Carlo control consists of 2 steps: 1. For an episode, for each state-action, update the q value by its (return - old estimate) (the error). 2. After the kth episode ends, update policy by epsilon greedy update using epsilon as 1/k. This ensures q converges to q*.
* Intial Q values matter only when a constant alpha is used, if 1/n is used, they don't matter.
* Same concept can be applied with TD too (TD with epsilon-greedy policy), this is called SARSA.
* For SARSA to converge we have 2 conditions: 1. use GLIE (ie: variable epsilon) and 2. Robbins-Monro sequence for alpha, meaning sum of alphas over inf time is infinite and that the change in alpha over time steps vanishes at infinity, ie: constant alpha.
* In practice SARSA converges even without these 2 conditions. 
* N step returns can also be taken into account, and the same algo, SARSA(lambda) can be used to geometrically weight each step return based on lambda and update that (s, a) pair by this mean value over all step returns weighted by lambda.
* Again this is not an online algo, to solve that we use eligibilty traces for each (s, a) pair again.
* Disadvantage of SARSA(0) is that it only really updates one state, action pair after each episode (the one before the final reward) the rest just use 0 reward + their successor states' approximation, which is also 0 at this time.
* So it needs a lot of episodes to approximate Q, but SARSA(lambda) fixes this as each step along the episode gets some update to it's Q based on it's eligibility, so after 1 episode, all Q's are already non zero
* Beats the tyranny of the time step. Lambda also controls the effect of decay in the eligibilty trace, so lambda controls variance in that sense too, like how far back should states be in order to be eligible to receive that update. (farther it is, more the variance).