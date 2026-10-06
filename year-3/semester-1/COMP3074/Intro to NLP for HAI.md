## Conversational Interaction

Tools have become extremely widespread: natural language engines (Siri, Google Assistant, Alexa), speech recognition engines to interact with it, photo and image recognition, machine translation tools. These AIs work with language. LLMs have become synonymous with AI today. 

Language is a tool for interaction: between people (spoken/sign languages), with machines (CLIs), between machines (network protocols), 

### Natural language understanding
NLU systems are systems designed to analyse natural language. From analysing text data, we can perform sentiment analysis on a movie, understand what topics people are discussing, how to translate sentences and more.

### Natural language generation
NLG systems are designed to generate natural language. This can be done from other natural language (chatbots),  from other structured data (weather prediction) or from media (image captioning).

### Rule-based systems
Rule-based systems are very reliable (deterministic), easy to understand and require no data. They are capably of extracting elements from text through regular expressions, classify text based on lexicons, and build reports to send users (e.g. in the stock market).

### Machine learning
More computer power and more data led to the classical machine learning era, with a good tradeoff between performance and build times. ML brought about benchmarking, with benchmark optimisation and focus on building models to be good - bad for novel models that may not result in good scores.

~2012 brought about convolutional networks with images, and recurrent neural networks with text. 

NLP tasks involve (and will include in the labs):
- opinion mining
- sentiment analysis
- stance detection
- textual entailment
- summarisation
- question answering
- information retrieval

For HAI, the steps involved in this are preprocessing, text representation, text classification, and natual language generation. Conversational AI architectures & LLMs 


## Natural language processing

Each unit of interest can is a document: a book, a chapter, a paragraph, tweet. A collection of documents of interest is a corpus: libraries of documents, subsets themselves of a corpus.

Punctuation is important: a full stop must be handled independently to the words. Some words have the same spelling but mean different things: *to house* vs *a house*. Words can also gave different inflections and syntactic sugar depending on the language: programs must understand that *cat* and *cats* mean the same thing.

### Tokensiation
This is when documents are broken down into sub-parts. A document is made of tokens. These can be of arbitrary length: phrases, words, syllables, characters. Sometimes, characters are what matter with spelling, and sometimes syllables are what matter with speech recognition. However, usually, words are what is focused on. 

### Annotation
Each word/token is given its role in speech. Nouns, verbs, adjectives etc. are all parts of speech (POS) and tagged as such. This helps separate meaning using the grammatical context. "The dogged sailor dogs the hatch"  

### Standardisation: lemmatisation/spelling
Words are inflected during usage to express different grammatical categories such as tense, voice, tone, person, and mood (**conjugation**). Cutting inflections on words to isolate meaning: *cat* and *cats* both refer to the animal.

The goal of lemmatisation is to reduce words to their dictionary form, producing a consistent output. Stemming reduces words to the word stem very quickly; however, as essentially runs several *transformations* on strings versus dictionary deduction, it often produces words that do not exist.

### Stopword filtering
When tokens are ignored that do not have a meaning on the overall conversation. Categories such as determinants and quantifiers are "noise", so can be removed from the overall vocabulary - resulting in easier predictions and less intensive processing.




