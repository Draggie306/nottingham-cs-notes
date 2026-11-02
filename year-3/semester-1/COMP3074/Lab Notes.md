
## Lab 2

### Sklearn methods

`.fit(X)`
- learns something, e.g. what words occur, from the supplied data X

`.transform(X)`
- applies something previously learned, to data

`.fit_transform(X)`
- Learns from the data and immediately transforms (applies) it

`.predict(X)`
- Uses a trained classifier to predict a label (e.g. positive/negative review)

`.fit(X, y)`
- trains a model using features and labels (e.g. words that are associated with positive reviews)

#### Classes

`CountVectorizer`: creates a new vocabulary of words, and convers documents into a matrix of word counts. 

Given an array `fit_transform()` discovers the vocabulary and assigns a column to every valid word, then the `transform` counts the occurrences of the word within every document. 


## Lab 1

### Term weighting

When comparing different corpa, some docs may be larger/smaller than others. As such as weighting is needed to even out this and ensure that everything can be compared relatively and equally:

Binary weighting
- weight of the term $T$ in document $D$ is 1 if $t ∈ d$ else 0.
- achieves evenness across documents but does not distinguish "local" importance of terms

Log-frequency weighting
- weight of the term $T$ is scaled by a function of the raw frequency in document $d$. (Traditional log weighting means that common terms do not have significantly higher values than less frequent ones)

TF-IDF:
- Amplifies traditional log-scaled weighting by adding a function of documents in the entire corpus over the documents that contain a specific term $n$
- This penalises terms that are present in the majority of documents and promotes terms that are present in fewer terms