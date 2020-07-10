# RL Notes:

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
* Bootstrapping means we don't take the real return Gt at the end of the episode, rather update based on the estimated return (ie gamme * value of next state). DP does this too. MC doesn't, it takes the real return at the end of an episode.
* 2 terms: TD target is (immediate reward + gamma * value of next state) and the difference between target and previous estimate is the TD error. This is for TD(0).
* TD is an online algorithm that updates the values of the states during the episode, while MC updates only after the episode terminates.
* TD has much lower variance compared to MC, as in TD we only look ahead by one step and update based on the value of the next state whereas in MC we update based on the unbiased estimate of the value for that state. (lot of noise based on randomness of successive states chosen)
* TD and DP are similar as they both do one step lookahead,this one step lookahead and update is called bootstrapping.
But they differ because TD (and MC too) samples some sequence, while DP searches all actions and transitions.
* MC may work better for non-Markovian environments. TD exploits the Markov property.
* TD(lambda) is a spectrum across TD(0) (one step lookahead only) and TD(1) (MC learning). Between this, the lambda param weights different step lookahead values geometrically and averages them. (beyond the terminal state, the entire area is dedicated to the MC term).
* There are 2 equivalent views to this, forward view where we wait for an episode to complete then update the value based on this average or the backward view where we use elgibility traces to proportionally update the value of that state based on its recency and frequency.
* The backward view is an online algorithm. In this, at each step of the episode, every state gets updated by the TD error (for some state) proportional to it's eligibility to receive that error.