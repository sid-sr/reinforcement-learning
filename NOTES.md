# RL Notes:

## Lecture 2:
---
* Markov Decision Processes are Markov Reward Processes with decisions.
* In MDP's, STP matrix is action dependent.
* The reward function is also action dependent.
* The policy is a probability distribution of choosing a particular action given a particular state.
* In MDPs, policies are only current state based and don't require the history.
* They are also time independent ie: purely based on state and not time step.
* Once sequence of states is chosen using the STP with the fixed policy, sequence of states and sequence or states + rewards are both MPs.
* Conversion of MDP to MRP can be done by averaging the STP matrices of each action over the policy function, same for reward.
* Action value function tells us what is the expected total reward on choosing a particular action 'a' from a particular state 's'.
* Bellman Equation recursively defines what the value/action-value will be at a particular state/state-action pair.
* Bellman Equation ordering for action-value function is state first then action in the next state(s).
* Bellman Equation ordering for value function is action first and then state(s) after choosing that action.
* An action does not actually tell the state we end up in, just gives us a new STP which we can then use to tell for each state we end up in, what's the value for that state, summed up -> and this entire value summed up over every action we take + the reward for that action.
* The optimal action value function for a given state and action is: the reward for that (s, a) + mean probability over all the optimal value functions of the states it can reach after that action.
* The optimal state value function is the max of all the optimal action value functions (over all the actions that can be taken from that state).
* The optimal policy function should choose the action that gives max q* from that state. So, unity for that action from that state, all other actions from that state have 0 probability in the optimal policy.

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

## Lecture 4
---
* Monte Carlo learning, Temporal Difference learning and TD(lambda) are 3 ways to evaluate a policy in an MDP that has no prior info of the rules/rewards.
* MC requires episodic MDPs where we average out the return of each episode as the value function.
* The value of a particular state is the mean of the return (Gt's) that we get where the St is that state.
* So for each state, we need to track the accumulated return and a counter for number of times visited, the ratio of these two is the value for that state.
* We accumulate reward and increment the counter only once for each episode (for a given state) -> First visit MC. 
* Every visit in an episode can also be taken into account -> Every visit MC.
* The mean (which is the value) can be updated incrementally as we see the Gt for that state appear by just correcting what we thought the mean was by the error (difference between mean and the Gt that we see now).
* Step size can be a fixed value too (rather than 1/num_seen).
* TD works on incomplete episodes, by bootstrapping.
* 2 terms: TD target (immediate reward + gamma * value of next state) and the difference between target and previous estimate is the TD error. This is for TD(0).
* TD is an online algorithm that updates the values of the states during the episode, while MC updates only after the episode terminates.
* TD has much lower variance compared to MC, as in TD we only look ahead by one step and update based on the value of the next state whereas in MC we update based on the unbiased estimate of the value for that state. (lot of noise based on randomness of successive states chosen)