# Guest Lecture 2 - Language agents, processing and models

## NLP systems
This encodes natural language into representations by the machine (commanding), and then giving this machine understanding back to natural language (result)

Naturally, there are several in-between steps:
- Preprocessing
	- Tokenisation, annotation (with part of speech), limetising stop-word filtering, etc. This tries to remove as much information as it can
- Representation 
	- “Bag of Words” model. 
- Intent prediction
	- Perceptron - inspired by the biological qualities of neurones.
Prepare result


This is all very complicated - with thousands of intents and models. 

## From statistical to neural language models

Voice-powered assistants often deal with ambiguity: “eyes on the price” versus “eyes on the prize”. To work out which is the most likely to have been said, we do a lot of counting of all the information and books available and representing a sequence of tokens, with the 

> Markov assumption (Markovian process): language is a stochastic, memoryless process. 

![](../../../Images/Pasted%20image%2020260428162325.png)

This was good until the year 2000 or so. Probabilities are rigourous, very fast to calculate BUT this was not robust between words and synonyms.

If instead of counting things, we used neural networks to estimate probabilities of word sequences. Neural language models are autoregressive: they compute the next token at a time. 9 tokens creates the next one, which then is fed back to be 10 tokens to create the next one. 

By scaling the neural network to become very large, we can solve many issues - but not all of them. Long term dependencies are particularly bad: words at the end of a sentence that depend on the start of the sentence. Although they can be scaled ad infinitum, they require lots of data and memory. In 2006, the largest model was 20 million. In 2026, it is over 1 trillion parameters. 

## Large language models

To turn neural models into large language models to solve the entire problem in one go. We should be using models that make better use of data: **recurrent neural networks** model dependencies, which was added into long-term memory networks (solving the long-term dependencies in the architecture).

The transformer breaks the dependency of linear processing.

The second trick was changing the training process. Instead of using all the data all the time, we have phases. 
- In the pretraining phase, the model just predicts basic text over trillions of documents until it calculates the next phase perfectly. 
- Supervised fine tuning: where you start specialising into translating, answering questions, labelling images. This creates a good completion engine/autocomplete but 
- Reinforcement learning: focuses on behaviour. If the model can generate 10 answers, which is the best one that humans want to see?

The third trick: data. 
- Just steam the data and figure out the rest in court. 

The fourth potential trick: after making models large, people began to realise it is useful to make them small. 
- Find a lower precision of the neural network but don’t use a full floating point number to represent the same representation.

> The smallest representation of bits that represents a language is just 1.

![](../../../Images/Pasted%20image%2020260428164351.png)
## Agentic systems

AI shouldn’t answer questions, it should do stuff. *One that acts and produces and effect*. Something that senses its environment, thinks/plans what to do, and act on the environment.

Computer scientists have not been stopped by text-based interfaces to interact with the world. Terminals, APIs, text messaging, etc.

”Tool calling” gives the LLM a way of interacting with the world.

To do something useful, the agent should be able to remember stuff. This is the core idea between retrieval augmented generation. Instead of generating an answer, it generates a knowledge graph/database/website before feeding it into the LLM (provides a source of grounding) and only then generating. 

Reasoning. Making a plan to solve a problem. LLMs can be made to think harder by forcing it to spend more time generating the answer - known as “inference-time scaling”.
- Self-correction: generate a response, then use the model to correct the response against a series of constraints.
- Process reward models: a separate, specialised model (the verifier) evaluates intermediate steps of a calculation
- ﻿﻿Chain-of-thought expansion: the prompt explicitly instructs the model to articulate intermediate reasoning steps before providing the final answer.


This forces the model to process more ”tokens” before giving a final, longer, but better, answers.  

### Commoditisation of intelligence

Model poisoning: if an extremely large models are made, released for free, but contain one code word that transmits users’ passwords, then everyone uses the model and trusts it, but the (company/lab) who controls this release a word out and then all passwords get revealed.

### Agent meshes and teams


