# RL Notes:

## Lecture 7:
---
* Rather than evaluating Q and V and then define a policy based on that (eg: greedy), we can directly approximate the policy function itself using parameters, these are called policy gradient methods.
* In some cases, using a policy gradient method is more efficient than a value function, esp. in continuous state spaces and high dimensional spaces, they converge better. They might be inefficient and have high variance.
* Actor Critic algorithms combine both policy-based and value-based function approximators.
* Policy based methods allow us to use stochastic/random policies which sometimes turn out to be the optimal policy for a given scenario rather than a deterministic one (eg: rock paper scissors)
* If we are in a POMDP or using a set of features for a state that don't fully capture that state, state aliasing may occur (two different states have the same feature representation) and a deterministic policy (based on the same value function) will perform poorly, while a stochastic policy (has randomness) would be optimal.