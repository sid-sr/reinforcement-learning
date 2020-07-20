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
* With this online update method (say TD(0)) we can do control as follows: start off with random weights for each feature. Now using this we can approximate any Q(s, a) value, act epsilon-greedily and choose an action, now we update the network to correct it's curve to fit the TD target we saw now (ie: SDG with m=1 update) and then we take the next action based on the new estimate of Q using the new weights.
* So it is similar to table lookup except we use a function to approximate Q rather than a table and we update the function params slighty at each step to fit better to the actual Q.
* So, it never gets to Q pi, like any NN, it just approximates better and better with time.
* Exact same concepts can be applied to approximate action value function too, building a set of features for each (s, a) pair and learning some weights for each of these features to approximate Q.
* But working incrementally example by example is inefficient, rather we can work using batches of experience and try updating the weights to fit the whole batch. If we had an oracle that told us the V for each state, we can create a whole dataset of (s, v(s)) pairs and something like least squares algorithm to find the weight vector.
* Another disadvantage we see is that the weight updates often explode in the case of control or they might oscillate around the true value function.
* SGD with Experience Replay: we store an explicit dataset of (s, v(s)) pairs that we see and we treat it like a supervised learning problem where we randomise the dataset and fit a function, so the time correlation in the data is removed and **this ensures weights don't explode.**
* DQN (Deep Q Networks) use **Experience Replay** and **Fixed Q-Targets**. Steps are: 1. Create a dataset of (state, action, reward, next_state) points which is done using our epsilon greedy behaviour policy 2. Train the neural net in mini batches of these with the targets as Q-Learning targets (reward + gamma * Q(new_state, greedy_action)). 
* Fixed Q-targets: There are 2 networks (2 weight vectors), the targets that we optimise towards for each update is from the old network (old Q values), so we essentially update our weights to fit the old predictions for some time steps (say a 1000) then set the new network as the old predictions and start training another network to learn from the old target Q values. This freezing and setting as target procedure ensures weight updates don't explode.
* This is because if we update the target dynamically based on what we learn, it makes the NN unstable.
* This idea of generating a dataset and using least squares method allows us to optimise for the best weights for the given dataset using a matrix inverse (O(N^2) here  N is only the number of weights not states). This can be done with MC target, TD(0) or TD(lambda) targets too.
* Control can be done with this too LSPI (Least Squares Policy Iteration) where we start of with random weights, act greedily get a dataset then optimise the weights in one go and repeat this process again. 