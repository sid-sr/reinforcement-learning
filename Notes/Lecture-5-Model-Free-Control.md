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
