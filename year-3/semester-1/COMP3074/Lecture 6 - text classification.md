### Labs

- front loaded, first ~5 are more like long, advanced lecture notes.
- after the 5th lab, they become deeper and coursework-focused



### Overview
There are many ways to classify values. For example, say there is a series of points plotted, and they are determined to be positive and negative.

It could be:
- Memorising the data
	- Very poor, not generalisable for new data
	- Takes a lot of space but very fast.
- Linear classifier
	- Fairly easy to generalise even in multiple dimensions
	- Fast
- Nearest neighbour classifier
	- Similar to linear but allows for more complex modelling
- Based on threshold values (tree)
	- Family of models are decision tree
	- Draws more complex decision boundaries in the data which may generalise well and has good modelling power

> Modelling = adapting to the dataset; generalising = adapting to data we cannot see


### Classification as generalisation
Generalisation is based on the assumption that the data being tested on is representative of the real world (i.e. a good example is using a subset of the data).

However, there are geographical differences (language - English, French, Chinese); cultural differences (words changing, new words, slang and acceleration of changes); time difference (change in vocabulary, concept drift)

### ML is the art of generalisation

ML: techniques that enable a computer to learn from examples

Deep learning: neural networks with multiple deep layers

Training: iterating modifying parameters to minimise training error such that generalisation error is reduced, estimated with the testing error.


Training error: how good is the model with training data (available and observed).
Testing data: how good is the model with testing data (available but unobserved until after the training run).
Generalisation error: how good is the model with real world data? (unavailable during any evaluation).

Deep learning models go into an implicit step of representation learning 

### Machine learning

- Supervised:known ground truth about the data, i.e. each data point has a label.
- Unsupervised: there is no ground truth known about the data, i.e. no labels
- Semi-supervised: there is ground truth known about some of the data, i.e. some data points have labels, others do not.
- Reinforcement learning: we are trying to learn policies/sequences of action, i.e. there is a ground truth, but it is very detached from the data (e.g., win/loss in a chess match)

### Gradient-based learning

Hyperparameters: parameters external to the training process, and are not modified because of this. 




### (Traditional) neural networks

If the output is an error, we can go backwards and modify the weights of each layer to resolve the error.

Deep learning models are this on a larger scale. The more layers in the network, the better the output.  Research focuses on enforcing structure in the data to make it learn faster and with less data, or generalise better (dropout, mixup and augmentation).

However, this can cause overfitting. With each hidden layer, models can learn more complex concepts even though the training error gets smaller. 

#### Regularisation
Regularisation is a set of techniques used to prevent overfitting. There are several ways to do this:

- L2 regularisation (Tikhonov)
- L1 regularisation (Lasso)
- Elastic Net regularisation (linear combination of L1 & L2)

Current technique examples, amongst those being actively researched, also include:

- early stopping: stopping the learning process before convergence.
- data augmentation: creating noisy, synthetic data through invariance-preserving transforms
- drop-out: randomly "disabling" neural units or whole layers during training
- mix-up: creating noisy synthetic data through interpolation.

Batch learning is when the model is trained on the full dataset all at once. Training happens offline and the model does not update automatically with new data. This differs to online learning, where the model's parameters are continually updated with each new data input. However, online learning models can be sensitive to noisy or corrupted live data, and generally have to be smaller and do not have time to be rigourously optimised for higher accuracy on stable datasets like in batch learning models.

### Coursework

Will need to take in input, and then find out what the user wants. This will be done via:
- intent classification, sentiment intent, and guardrails

Similarity retrieval, classification and more module concepts will be required for the coursework to build and evaluate a chatbot.