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
* Each state can be represented by a feature vector (a set of useful attributes that describe that state) which compresses all the info about that state -> makes learning easy.
* So we just do a Linear Regression model with weights multiplied by their corresponding features for each state. States act like training examples here and we updates online (m = 1) and minimise MSE.
* Table lookup approximation is a special case of VFA, where our linear function just chooses a unique weight for the given state (and the weight here is the approximate value).
* Actual vpi however cannot be known (targets for our ML algorithm), so we use estimates depending on the method: MC: use return from that state Gt, TD: Use TD target from that state as ml target variables, TD(lambda): use lambda weighted return Gt lambda as target for the algo.
* TD(0) is biased but it still converges. 
* We essentially build a dataset of (state, target) pairs as we go and incrementally update online (at the end of the episode/during each state depending on the algo).
* Backward view of TD(lambda) can be applied here too, the ET is smaller as it's the size of the feature space, each feature is decayed with time and increased by it's magnitude at each time step and delta W is updated by alpha * TD error * eligibility vector (rather than the magnitudes themselves like in MSE LR).