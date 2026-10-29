

1. Text preprocessing
2. Text representation
3. Text classification
4. Natural language generation
5. Evaluating AI systems



## Why evaluate?

"Doing things in a principled and disciplined way is not much different from messing about."

AI systems are complex and often non-deterministic. Evaluation may happen in terms of the system (components) or how users evaluate it. 

## 1. System-centred evaluation

Evaluating a classifier allows us to investigate performance metrics: **precision** of the classifier (how many true positives) and **recall**. **Accuracy** and **F1-score** give a much wider evaluation particularly when classes are not uniformly distributed.

### **Experiment design**
#### Train/test paradigm
There is a train/test paradigm: holding out data to simulate "new" data: training and validation sets are used to tune hyperparameters, and the testing dataset is used for the final evaluation. The problem is how to select the best hyperparameters: splitting the set further with train/validation/testing is an easy way of doing this: 

![](../../../Images/Pasted%20image%2020261028091513.png)

#### Cross-validation
This involves training with rotation: the training/testing split is split into a number of partitions. For example, a dataset of 1,000 documents can have an 80/20 train/test split, and the 800 documents could be split into 4x200 partitions.

This allows us to see not just performance on one model, but overall across the entire dataset.

Nested cross-validation uses data more efficiently: this estimates performance more reliably by giving the average of all the folds and validation steps. It allows us to see model robustness (variance) between different runs. However, it is more time consuming. 

![](../../../Images/Pasted%20image%2020261028092248.png)


When evaluating a QA system where one question has one answer, the typical system returns a list of answers by decreasing amount of relevanece. Therefore, we can measure: **if the first answer is the correct one**, and **how far the correct answer is from the top**.

![](../../../Images/Pasted%20image%2020261028092401.png)


### Evaluating NLG systems

This is generally harder. There is intrinsic evaluation (properties of the text) with automated evaluations, fariness and biases.

Extrinsic evaluation refers to the impact on downstream tasks - for example, user-focused studies and evaluations.

#### Automated methods

Automated methods
- BLEU score (precision-oriented): how much of the translated text is in the reference translations
- ROUGE score (recall-oriented): how much of the reference summarises are in the summarise text 

Modern methods:
- BERTScore: compares generated answer and expected; can account for semantic variaions
- LLM-as-a-judge: controversial. Have generated text, reference text with the largest language model to rate the NLG output on terms like fluency. 

#### Drawbacks

System-centred evaluation focuses on there being a ground truth during the comparison, so there must be a single "gold standard" label. However, there are:
- semantic equivalence: there may be multiple ~equivalent outputs that are not captured: different ways of saying the same thing where only one way is in the data, thereby penalising other ways of saying things.
- subjectivity: truth is contextual and can vary, for example emotions in different cultures may be considerably different. 


**Other forms of system evaluation:**
- Bias probing: use template sentence to probe for stereotypes, such as filling in the blank. 
- Robustness testing: measure performance against small changes in input, perturbing inputs with typos, paraphrasing and filler words that should not change the answer.
- Adversarial testing: measures system performance against inputs designed to break the model, measuring the "worst cases". This could be adding many filler sentences into an emotion classifier to misunderstand it 



## 2. User evaluations

Task-based evaluations measure impact on end users. 

**General steps:**
1. Determine target audience
2. Understand user needs
3. Identify relevant work
4. Determine goals and expectations
5. Check validity of setup
6. Select sensible subset for evaluation
7. Get ethics approval
8. Keep a log
9. Be explicit about materials and methods
10. Describe ALL relevant (and unintended!) results.