In order to process data, we need to apply mathematical functions on words. To do this, we need to turn words into a sequence of numerical values 

### Sparse vector representations
This uses a **bag-of-words** approach with **term weighting**. 

A core machine learning representation is a *vector space representation*: a vector space with multiple N dimensions, where N is the size of the corpus's vocabulary. A document is a vector in that vector space, where the frequency is the component of the vector.

![458](../../../Images/Pasted%20image%2020261007091152.png)


The similarity of objects is intrinsically related to distance measures: objects that are closer in the vector space can be associated together with clustering algorithms, some classifiers, information retrieval algorithms match "close" points in the space.

Each dimension is computed from a function of the frequency, not the raw frequency itself - long documents end up very distant from short documents.

### Term weighting

Binary term weighting: the weight is simply 1 if the token exists in the document, 0 if not.

Log-frequency term weighting: very good at decreasing the size advantage for large documents. However, some common words have high scores across all documents.

TF-IDF: combines term frequency with the inverse document frequency. 
![](../../../Images/Pasted%20image%2020261007092753.png)

This is useful, as words present everywhere are pushed towards zero: these words do not distinguish different sentences from others.

### Flat vs sequential representations

The Bag of Words has a fixed size: V (size of the vocabulary). Sequential representations have a variable size, based on document length. Each word, sentence and paragraph is encoded separately. This takes more space but allows much more nuance.

The simplest form of variable-length representation is one-hot encoding. This creates vectors of dimensions **input length \* vocabulary size**.

One issue is that all words are treated as equally unrelated, with no semantic understanding. It also creates large sparse matrices (mostly containing `0`).


## Dense vector representations


### Word embeddings
The key idea of languages, modelling meaning based on the distribution of language in large data samples, is known as distributional semantics. 

For instance, "cat" and "dog" appear in roughly the same contexts, same with "red" and "blue", so their meaning is more closely related than the adjective "large". 

A word embedding is a dense vector representation. 

The issues with word embedding are:
- the algorithm preserves biases in training data
- there is no true semantic understanding (distributional semantics)
- there is some latent dimension that is not observable: cat is closer to dog than tiger, which might not be desired.

### Modern representations

Word2Vec uses pretraining: word embedding is trained on the data, and the embedding is used to train another model.

Since then, more complex forms of pretraining have been designed, such as BERT and GPT3. These use self supervised learning tasks: next token prediction, gap token prediction and more. Without the need for labelled data, lots more data becomes available. 

## Representation and Similarity



### Retrieval-augmented generation











