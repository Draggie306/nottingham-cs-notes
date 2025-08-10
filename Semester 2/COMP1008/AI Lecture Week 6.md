## Natural Language Processing (NLP)
Is the technique to help human communication with the machine. There is no format to “talk” with the machine - different languages, different meanings, etc.

It is a branch of AI which allows machines to ”understand” and generate human language text. 



### Approaches 
#### Symbolic 
Relies on **rules and logic** to represent and process languages. It can be based on a set of instructions, based on grammar (how words are used in sentences), lexical databases (storing definitions of words and their relationships in context)

#### Statistical
Probabilistic models to analyse language patterns to predict words (using Bayes’ rule). 


#### ANN-based
Handled sequential data with memory (the result of the previous output)


### NLP Pipeline
The NLP pipeline is a series of steps to transform new text into a format suitable for further analysis and extracting meaningful information.

- Text Preprocessing - very common and almost the same in all NLP systems. Involves:
	- Normalisation (converting text to a standard form like lowercase)
	- Tokenisation (breaking down the text into sub-words, words or phrases or sentences)
	- Stopword removal (filtering out common words that do not give more context “a”, “the”)
	- Stemming (reducing words to their root form, e.g. running -> run, to improve consistency)
	This allows the models to process information in use for later steps (and is not NLP itself)
- Feature Engineering - dependent on the AI application and includes:
	- Part-of-Speech (POS) Tagging: each word is tagged/assigned its function, e.g. noun, verb, adjective, adverb, etc.
	- Named Entity Recognition (NER) identifies named entities further such as person, number, organisation, location or object to further build context.

In traditional, symbolic-based NLP models, it would rely on if the first letter is uppercase, then if followed by Inc., then assign it as a named entity.

Statistical models (Bayes’) calculate the probability of tags or weights of features

ANN-based NLP deep learning techniques like Transformers captures the semantics and relationships in word sequences.

### Applications
Eugene Goostman was released in 2014 and may be considered to be the first program to have passed the Turing test. It used a rule-based system with predetermined responses and actions to inputted prompts, with a knowledge-based database of pre-written responses and conversational templates. It had some deceptive techniques built-in, such as pretending to be a child.

IBM’s Watson in 2011 used POS Tagging and NER
Unsupervised learning was used as labelling data is very expensive

Google Translate until 2016 used statistical models. Since, pretty much all translations use Neural Machine Translation as an ANNs. 
- Encoder: analyses and transfer words to a useful representation to apply NLP methods.
- Decoder: after calculating probabilities, output words based on context
- Attention mechanism: focusing on the specific parts of the sentence and input sequence
- Doesn’t disclose all specific algorithms.


## Large Language Models
Generative AI is based on lots on previous information to create entirely new content. 

All LLMs start from Deep Learning.
- Convolutional Neural Networks are successful on image applications due to their layer-by-layer, hierarchical structure and local features and 
- Recurrent Neural Networks (RNN) are successful on text due to inherent sequential structure.


Transformers are a specific ANN architecture effective for capturing long range dependencies in text. It completely revolutionised NLP. All LLMs today are built using transformers.
- The attention mechanism focuses on the most relevant input text assigns weight/importance of different words in a sequence based on context.

LLMs have a large amount of parameters (weights trained) that capture/formulate the relationship between input and output. To have high-quality outputs, it is trained on basically the entirety of human knowledge and history.
- web pages, books, articles, code, wikipedia, either licensed or “borrowed”;
- data cleaning, reducing duplicates and irrelevant & biased information
- text preprocessing: normalisation, tokenisation, stopwords etc.
The output is the most likely word/token based on probabilities — but this can include hallucinations as it does not “understand” anything in a given scenario.

The process involves:
- unsupervised pretraining: learning patterns on large text data, with exponential data and resources.
- supervised fine tuning: on specific tasks, updating parameters for specialised classification, sentiment analysis and translation
- reinforcement learning: rewards used to optimise the output 
- 
Temperature controls the randomness at the final output layer - higher temperature adds more randomness, so some words have a higher chance of being other words (not just the most likely output) and leads to a more creative output.



Improving AI requires algorithms, models and data.