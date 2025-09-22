Neural networks have been show to be the most useful machine learning model for things like stock price prediction, handwriting/speech recognition


The first neural networks - artificial neural networks - were made in 1943. The idea is to simulate, in the computer, neural networks in the brain. Inputs are combined, and if the combined input assessed is above a “threshold”, the trigger/output would be 1 and the neuron fires, else 0.

> Like in the human brain, over time, neurons change and get strengthened between various neurones, and this is matched in the neural network.

In 1949 - the first learning rule where the weights automatically adjusted - instead of changing them manually. During the 50s and 60s, the perceptron caused great excitement.
However, it was learnt that there was a limitation in important functions (non-linear separable) and caused a 15-year AI winter.

Interest increased in the mid-80s where researchers discovered multi-layer networks. These could be used to solve non-linear separable.


Training:
An epoch is …. 

```
While epoch results in an error
	Check next inputs (pattern) from epoch
	Err = Y - O
	If Err != 0 then
		w1 = w1 + LR * X1 * Err
	End if
End While
```

w1: previous model’s weights
LR: learning rate; how quickly the network converges

Training value Y: The value we require the network to produce.
Error: The output by the network O differs from the training value Y.

The measure of performance (loss error) is the mean squared error - if 0, then it may be overfitted.

Visualisations
Plotting the sets of input against the output can allow us to


Linearly separable: where output data points (clsses) can be separated using a linear boundary. **Only these functions can be represented by a single layer neural network.** 



**Benefits**
- Artificial neural networks can learn more very complicated class boundaries
- Can be more accurate
- Has the ability to handle a large number of features. 
By adjusting the weights, its learning is very accurate and can handle things like natural language translation - much more so than a simple decision tree.

**Drawbacks**
- It is hard to implement: trial and error for choosing parameters and network structure. *However, more so now than ever, packages and libraries can be used to fine-tune and much more easily create our own neural network.*
- It has a slow training time and learning time based on its parameters, i.e. settings and configurations. Nonetheless, it is much slower than a decision tree, taking seconds vs milliseconds.
- It can overfit the data or even find patterns in random noise


### Neural Network extension: Deep Learning
This involves a large number (more than just 1 or 2) hidden layers (steps between the input and output). It is a simulation of the human brain, with multiple layers of connected neurones progressively extracting features from data.


Convolutional neural network: feed forward deep learning neural network that learns feature engineering. Each layer applies a sliding window, with it learning patterns of local features. 


Transformers
A type of NN that transforms an input sequence into an output sequence
The input is 


“all models are wrong, but some are useful” - they are not the extact representation of ht relationships in the real world, as they are base don assumptions. Our job is to find the useful models within these.

#### ANN Data Preparation
Data processing is the same as in a decision tree.
We can have the train_test_split

#### Code example
```python

# <train_test_predict here>

# Import multi layer perception 
from sklearn.neural_network import MLPClassifier

# The library assigns random weights first and it will gradually converge over time
mlp = MLPClassifer(hidden_layer_sizes = (3,6), max_iter=3000)

# Repeatedly adjust weight based on inpt/expected output and the learning rate, do this repeatedly until the min^2^ arrows are minimised.
mlp.fit(X_train, Y_train)

from sklearn import metrics

y_pred = mlp.predict(x_test)

print(metrics.accuracy_score(y_test, y_pred)) #  compares actual output vs predicted output trained by the neural network

# if we are not quite sure, instead of randomly partitioning the dataset, it can partition data according to the parameters. each time, uses 1 part for testing and the other for training, repeat this across all X times and output the best trained MLP model.
from sklearn.model_selection import cross_val_score
acc_ann = cro………


#  as the trained neural network is  difficult to understand as i’s a series of combinations and linear regression sequences, weights do not have any meanings to humans
print(f”Number of outputs: {mlp.num_imputs}”)

```

![[Pasted image 20250220104520.png]]

