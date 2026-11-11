

## Reminder: Checkpoint Info

There are 6 things to get the overall "check":

- Demo the chatbot running in the CLI (same as the final)
- Demo this to a TA/Convener in the next lab
- Show the code - checking the Q&A is not hard coded and similarity-based matching is used.
- Implement similarity-based intent matching or a classifier for intent matching to route control flow of the chatbot to the correct function that handles the intent
- Produce a coherent response in response to a given intent
- Identity management: ask the user's name, store it, use it

![](Images/Pasted%20image%2020261110100634.png)

Used to give out bonus marks for this, but not any more.


## Branching

### Constrained responses
Designing a prompt (what the chatbot says) in such a way that the person responding to it will include a certain keyword. For example, saying "What city are you travelling to", not "Where are you going; or "What song would you like to hear". one such strategy is using *N-based lists*: containing the N likely matches to fund the correct result, iterating over the list until the user confirms. 

### Open Speech
This allows for flow when the response doesn't need to be processed. This involves a generic reply, similar to the "generic confirmation" strategy. This can be done by e.g. a virtual nurse saying "Tell me more about the headaches you have been experiencing", the user replies with whatever, the the nurse replies: "Thank you. I will share this with your doctor".

### Input categorisation
This also includes sentiment analysis - categorise user input based on e.g. emotions and branch based on this.

### Wildcards and logical expressions
WIldcards allow for certain words to be repeated without having to explicitly specify them: "My computer is really slow" is the same as "My computer is slow" and also "My computer is really really slow". 

Logical expressions, such as: "my computer is **not** working" is very important, alongside `forgot AND password`: "my dad forgot his password again" - processing needs to understand that if these statements occur together, branch to an action. 

### Disambiguation
When there is not enough information, or too much information: such as the right city for weather, or if the intent is unclear "i need help with something".

When there is more than one piece of information, such as the user's response being ambiguous "I have a fever and a cough" - then ask the user to pick the more important one, or one of the options "shall I call the mobile or work phone?".


### Dialog Management
A strategy that combines all principles: error handling, confirmation, context capture. 

![](../../../Images/Pasted%20image%2020261110102848.png)


### Capturing intent and objects
THe object and intent both need to be captured: what the user wants to do with the object. Intent typically corresponds to verbs, while object are intuitively nouns. For example: "Show me my calendar" or "Delete my meeting from my calendar". Intents and objects are also combined in the concept of *utterances*: a statement that allows you to map different ways the user might want to express themselves: asking different ways of saying the same thing, but matching to the same answer.

### Negation handling
Negative responses are very important. "No", "not", "don't" and "neither", "except", "dislike" all have negative connotations to allow users to express what they don't want. If this is wrong, the response will be the inverse to what is wanted. This can be handled with logical expressions or within the sentiment classifier.


### Sentiment Analysis

![](../../../Images/Pasted%20image%2020261110103544.png)

If building a voice model, we can combine e.g. loudness and other data in the auditory channel that is not present when doing text analysis.

### Speaker verification

Also known as voice biometric authentication, this uses the voice ID to verify the speaker to avoid triggering wakewords on some assistants. Another use case is transcribing meeting/mult-party conversations, allocating each transcribed phrase to the correct speaker.

### Context
Taking advantage of the basic context the interface seem smarter and save users' time. It can track the stages required to complete the transaction - giving more flexible messages to users - and coreference resolution including pronouns and indexicals to track turn-by-turn concepts, e.g. "how old was he when he died".

### Personalisation
![](../../../Images/Pasted%20image%2020261110104254.png)


### Conclusion

VUI and CUI is not a solved problem; there are huge challenges around the gap between ASR and NLU capabilities and how people really talk. Designers can make many changes to make VUI and CUI more effective, despite the associated limitations.