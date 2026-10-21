
## Meta

![](../../../Images/Pasted%20image%2020261021090459.png)

Lab is designed to frontload work, and also to help with the exam.

The coursework has 3 deliverables:
 - Chatbot: 30%
 - Report: 50%
 - A short narrated video: 20%

## About NLG

In the chatbot cycle, the result perparation appears after all the preprocessing, representation, classification. Now we have a good understanding of the  user's intent - so can generate the answer that will be fed back to the user.

NLG is the other component of NLP (NLP is understanding AND generation). It can be defined as a subfield of AI and computational linguistics that focuses on computer systems that can produce understandable texts in human languages. **Be understandable and meet communicative goals.**

NLG is used in:
- informational reports (e.g. weather reports and medical summaries)
- entertainment: story generation, AI roleplaying
- interaction: "human APIs", website text interfaces
- assistive: assistive aids with SEN
- bot journalism: news stories generation
- bot propaganda: news stories generation

### Methods
There are 2 categories of NLG:

Template-based:
- gap-filling
	- Very simple, no-to-low error rate
- rule-based systems
	- expanded gap-filling systems
	- more complex rules
- grammatical functions
	- manipulate the sentence themselves with its grammar
	- low novelty, ~medium error rate

Dynamic:
- abstract representation of knowledge, no fixed templates, pure dynamic generation of text

Template-based models start from fixed templates, may be very repetitive with fixed structures but low variability: templates are usually gramaticlly coherent.

Dynamic models use generative algorithms to build sentence. This is very high noise because there is lots of error potential, but there is a high potential for novel sentences. 


### Understanding and Generation

![](../../../Images/Pasted%20image%2020261021092149.png)

The system discovered that the dates are the same, calculating a comparative change in status (colder vs hotter), and it has encoded somewhere that "cold" means to be 14C which can be done by threshold values etc.

![](../../../Images/Pasted%20image%2020261021092317.png)


### Stages of template-based NLG

- Firstly, **content needs to be determined**. A key thing often forgotten is placing the surprise or importance of the information at the start of the sentence. 
	- Depends on communicative goal, size/level of precision and prioritisation over the status quo.
- **Document structuring**: order of information, and grouping the sentences: "paragraph 1 about X, 2 about Y and 3 about Z".
	- Choose an order: "I went to the store, and I bought some fruit" makes more sense than "I bought some fruit, and I went to the store."
- **Lexical choice**: content of the words that depend on genre, context, perception and specificities: medical terminology is different to a weather system.
	- Relation with the outside world.
- **Referring expression generation**: in languages we do not say the same word twice: "**Paul** went to the cafe. **He** was hungry" and not using "Paul" twice.
	- Must make sense spatially and temportally, but referring expressions need to be unambiguous, easy to understand, easy to compute and gramatically correct. 
- **Aggregation**: merging syntactic or conceptual constituents.
	- Paris is warm. London is warm -> Paris and London are warm. (Syntactic)
	- Saturday will be cold. Sunday will be cold -> THe weekend will be cold (conceptualisation)
- Realisation: building the actual output:
	- syntactic realisation: word ordering
	- morphological realisation: plurals
	- orthographic realisation: capitalisation


### Generative models

Instead of having complex intent-based classification models like a decision tree, only having one model generating text following from the input can be created.

![](../../../Images/Pasted%20image%2020261021093437.png)
This is not applicable in reality - with 400 words there is a 0% chance of the probability being true.

![](../../../Images/Pasted%20image%2020261021093527.png)
This becomes much easier.

A language model is simply a probability distribution over tokens: 
1. Write a sampling rule, such as "pick highest probability token"
2. Select a starting seed token
3. Apply sampling rule on a seed token (or sequence of words, i.e. prompt) to generate the next token
4. Generated token becomes the seed token
5. Repeat from 3 until generated token is an end of turn/sentence token. 

The sampling rule can be non-determininstic to create variety: i.e. one in the top 5 words.

### Neural language models

Neural networks are universal approximators: we can move from counting to computing.

Approaches for dynamic NLG includes recurrent neural networks, and transformers. 



