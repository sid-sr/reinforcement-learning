# RL Notes:

## Lecture 6:
---
* Real world problems have too many states to store in a table. To solve this, we use function approximation.
* Here, we try to predict the real Vpi(s, a) and Qpi(s, a) using a smaller set of parameters (say using a neural network). 
* This approach reduces memory and also allows us to generalise value functions of unseen states (by NN predictions, say). So the input to the NN is our current state, or state-action. Output can be the estimated V val, Q val (action in) or Q val (action out) for each action from that state.
* 2 main methods we use are linear functions and NNs
* Our NN must be able to handle non stationary data, meaning the function we're trying to approximate keeps changing as we train, unlike a traditional supervised mode.
* In linear functions, we approximate V for each state based on weight w and if we had the actual value function v pi, we can use SGD.
* Here, we can do online updates. Whenever we see a state, we update our weight vector by learning_rate * (actual - observed value) * diff. of function wrt w. In SGD, states in the sequence are like training examples.