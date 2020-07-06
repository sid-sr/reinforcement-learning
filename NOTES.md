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