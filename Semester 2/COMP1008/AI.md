Professor Rong Qu - PhD in Computer Science, COMP1008, University of Nottingham - Year 1, Spring Semester.
## Introduction
### What is AI?
AI was coined in 1956: “the science and engineering of making intelligent machines”

A branch of computer science and engineering that deals with intelligent behaviour, learning and adaptation of machines. (2009)

Creating a computer that can think like a human (BBC, 2015)

Intelligence exhibited by machines that enable them to perceive their environment and use learning and intelligence to take actions.

AI can be divided into strong and weak AI.

### Definitions
Weak AI focuses on specific tasks and is limited on specific tasks. It exists today, and can be applied to various settings.

Strong AI is broader, general-purpose, self-aware, with an ability to learn like a human. *This is purely theoretical* - at least for now.


### Milestones
Turing introduced the Turing Test that has influenced AI in 1943. The birth of AI as a term was in 1956.

Top-down approach: pre-processes to do things, getting knowledge from real world into a program which we then use to solve a problem.

Bottom-up approach: no hard-wired instructions, we use models to learn from a set of data and learns new behaviours and knowledge

Knowledge is required to establish context. A translation should not be a literal one but a free/idiomatic one, which can only be achieved with understanding.

In the 1970s, we used single neurones connected into a network (an ANN) which could not implement basic functions - and as a result, there was an AI winter for around 15 years.

Then, in 1997, Deep Blue beat a world champion at Chess. 
In 2011, IBM Watson was released that won the US quiz show Jeopardy, and the Turing Test was passed in 2014.
AlphaGo conquered all open board game in 2016.
In 2022 November, perhaps “strong AI” ChatGPT was released and since, many LLMs.

### The Turing Test
Made in 1950: philosophical paper on machine intelligence: the Turing Test

A person asks 2 terminals various questions, and if the machine system is picked by the person 30% of the time then it is considered intelligent. **This is an operational definition of intelligence.** 


### Chinese Room Experiment
There is a simple rule processing system which is intelligent but has no understanding of Chinese. The system overall acts at it understands Chinese. This is a behavioural definition of intelligence.


Lectures: 18hrs
Computer Sessions: 14hrs
- Exercise materials release on Tuesday
Coursework: 25hrs
Revision: 30hrs
Study: 20hrs

Assessment: 75% exam/75 marks with Examsys, all lecture content. 
Coursework: 25%, 25marks

## Schedule
Part I: Fundamental issues
Part II: Machine learning (ANNs), techniques including regression


# Machine Learning I
There are lots of challenges with unsupervised learning so we will be focusing on supervised learning.

> A computer program is said to learn from experience (E) with respect to some class of tasks (T) and performance measure (P) if its performance at tasks in T as measured by P improve with experience E.

The top-down/classic approach models all the different functions and wires all these tohgether. We manually write hardcode programming langauge instructions to solve the (specific) task - which is difficult if e.g. new conftion emerges, etc.

A bottom-up approach just gives the system a lot of data so it can “discover concepts by itself in the world” - and see new patterns that do not have to be hardcoded or even foreseen by humans.


1. Analyse and understand the task
2. select appropriate models
3. train (pretraining) and test the model on new data
4. use this model to automatically solve unseen tasks
	- AI models do not need to be re-trained to solve new questions that people ask ChatGPT 

### 3 pillars
1. Models and algorithms:
Models just need data: this reduces the knowledge bottleneck from engineers/doctors to find all the functions and connect them together. 


2. Powerful and cheaper computation


3. Data warehouses
Bug jump in accuracy with huge amounts of data, i.e. it scales well


### Machine Learning vs. Traditional programs
In traditional proframs, we send data and the program to a computer to get an output.

In machine learning, we send data and the output into the computer and get out a model. This model is then used to take in new data and generate an output.

> Data mining is the exploration and analysis of large quantities of data to discover valid, novel, useful and ultimately understandable patterns of data.

Valid: result holds on new data with some certainty
Novel: non-obvious to the system
Useful: should be possible to act on it


Machine learning is broader. It is a branch of artificial intelligence, with neural networks (and regression, decision tree, etc.) a subset of ML, and then deep learning being a subset of neural networks.



Visualisation: Matplotlib
Manipulation: NumPy (data handling) and Pandas (processes data structure)
Machine learning: Scikit-learn
Deep learning: TensorFlow, Karas, PyTorch

# Machine Learning II
Processing & Data Processing, Unsupervised Learning

No matter the technique, the statement “garbage in, garbage out” still holds.

Top-down: follow a formula to find out something in real life. This is deduction - formulas, rules, instructions that tell us how to solve a problem. There is a theory, hypothesis, observation and conclusion.

We can also use the induction method: There is a pattern, which can be analysed with machine learning models, 


In supervised learning, we have labelled training data, with each sample/instance/data point consisting of a data point and a desired output. Its goal is to find/train a model to match an input to an output. Examples of supervised learning include linear regression, decision tree (these are very good), and ANNs (artificial neural network - basis for many deep learning models).

With unsupervised learning, we simply have the data points, and we do not know what they are or match to - there are no labels. The goal is task-dependent, depending on what we want to do. Examples of this include K-means and the Apriori algorithm. We can group data or identify trends with this model.

Reinforcement learning: there is an environment (the problem need to solve), and an agent takes in feedback from the environment along with a description of the current state and gets rewarded based on the action taken in the previous step. We do this repeatedly, via trial-and-error, and a policy is gradually learnt to make decisions.


The three pillars of machine learning are:
- Models
- Computation
	- Was a bottleneck; papers and research published in 1980s did not have the resources to make the model due to lack of compute
- Data
	- There was a breakthrough in 2013 where we finally had more data generated than during the rest of human history 

### Data preprocessing
Firstly, partition the data into two subsets: 70% training and 30% testing

E.g. in an excel table, columns are features/attributes and rows that contain the information is the sample/observation/instance. There may be a label/target column included too, with e.g. good/bad used in a labelled manner.

Data cleaning includes imputation - handling missing data. We can `df.isnull()`, `df.dropall()` - we do not want to do this as data is very expensive - `df.replace()` - replace data with missing.

Visualisation can be done with `matplotlib.pyplot as plt`, which can take in 2 DataFrames and out a nice graph.

#### Pandas
```python
import pandas as pd

df = pd.read_csv(“my_csv.csv”) # this transfers the excel/CSV into a format that pandas and models can be trained on. 
df(“Age”).mean() # simply get the mean age.
```

## Unsupervised Learning
There is much more unlabelled than labelled data. However, there is no **relation method** that can be used to allow for accurate evaluation. Lots of real world applications can make use of this - e.g. marketing, customer segmentation, document clustering in research, etc. An example of this is grouping amazon shoppers into larger groups, and then recommending an item based on everyone else in this group. In finance, outliers can be identified for fraud detection.
### K-means clustering
1. Choose the number of clusters K
2. Initialise K cluster centroids randomly
3. Repeat until a maximum number of iterations:
	- Assign each data point to the nearest centroid based on distance
	- Update the centroids by computing the mean of all their data points assigned
4. Out the final cluster of assignments and centroids

Applications of clustering include analysing company structure, social network connections, etc. It can measure many features and many different things].

In clustering, association rules are correlations between any two or more variables.
- Given a set of records containing items, produce dependency rules, to predict occurrence of variable X with variable(s) Y.
- Another example of this is supermarket lists; if many people buy X then likely going to buy Y.

However, a discovered correlation between data may not be causation. 


#### Exmaples of unsupervised training
1. Prepare the training. 
	-  Read in the dataset iris with datasets.load_iris()
	- Create a dataframe 


2. x = data/values
3. kmeans = KMeans(n_clusters=3, max_iter=100, random_state=0)
4. ykmeans = kmeans.fit_predict(x)
we can then show the centroids with:
1. kmeans.show_centroids_
or show the results:
![[Pasted image 20250206103955.png]]



y = df[“risk”]
x = 

Examples of supervised learning includes healthcare (disease diagnosis, drug discovery), retail (predicting product demand), natural language processing (translation, sentiment analysis), finance (credit scoring)

In supervised learning, we have more to play with.
WE partition the total training dataset into training and testing subsets

from sklearn
x_train, x_test, y_train, y_test = train_test_split(X, y, test_size = 0.3)



### More Supervised Learning
If the labels are categories, then we can classify (use classification on) them - e.g. good/bad.
If the labels are continuous data, then we use regression on them - such as integers and probabilities.

`Training Set -> Decision Tree -> Model <- Test Set` (how does the model generalise on the data?)

#### Regression
Regression is a model to find the relationship between variables X and Y. Training data essentially says, “based on the given data, predict what another data point will be”
Or: “find the function b1 and b2 that minimised its mean squared error to fit the samples, given the input data”:
- `G(x) = b0 + b1 * x`

Polynomial linear regression: `G(x) = b0 + b1 * x + b2 * x^2^`

Underfitting often occurs with simple linear regression - just one line that does not fully represent the data. Overfitted models often overrepresent the data, reflecting more randomness and granularity in the original data.

Regression training is very fast, whereas others (ANNs) may take several seconds. It’s easy to interpret and implement, but cannot handle complicated relationships and is very sensitive to nose and outliers with the risk of overfitting. 

#### Decision Tree
Trees are a widely used data structure. Decision trees are these structures with various decisions (e.g. cloud cover, temperature, etc.).

At the root node with a decision variable (feature), we compare it if it is e.g. greater than another variable and less than, then it goes to the left/right branch depending on their values for a particular feature. This process of continually adding layers to the decision tree repeats recursively until all possible values are grouped - or not (depending on overfitting).

Decision tree have reasonable learning times with even large numbers of features. They are easy to implement and intepret/explain - though simple sets of rules.
However, it struggles more with complex decision boundaries and having missing/incomplete data, or complex relationships. There is also the heightened risk of making the decision tree over-complex


confusion_matrix: can reveal information to do analysis. Given an output, putting test instances into a martix, with the actual and predicted output compared — revealing false positives/negatives (which we aim to be zero) and then also the correct & real predictions.

# Machine Learning IV

ANN
 - Is a black box - very hard/impossible to visualise: don’t know exactly what’s going on vs other models like linear regression.






