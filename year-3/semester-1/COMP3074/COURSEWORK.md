

Build, design and evaluate a chatbot. 


Lab is designed to frontload work, and also to help with the exam.

The coursework has 3 deliverables:
 - NLP-based chatbot: 30%
 - Report, up to a maximum of 2,000 words (10% margin) without citations, describing the architecture and evaluation: 50%
 - A short narrated video of no more than 5 minutes, explaining the implemented features and conversational design principles: 20%

Demonstrate mastery of the criteria across the whole set of criteria. If one part of the criteria gets a low mark whilst the other parts are excellent, the overall band will be the low mark. 


## Notes

Further created an "unseen" dataset, similar to the `extra_data` corpus for each intent. This was used when evaluating the classification recognition. 

\[Screenshot of some graph here\]

When adding extra capabilities beyond the initial dataset's intents - such as identity management - this did not cause any major issues. After the "identity_mgmt_input", "identity_mgmt_retrieve" and "action" classifications were added, there was only 1 test case that no longer was correctly routed. However, when adding the "knowledge_question" to the dataset, this caused many more significant regressions. For example, the input "What is my name" began to be classified and routed to the knowledge retrieval portion instead of the identity management routine.

https://legacy-docs-oss.rasa.com/docs/rasa/reference/rasa/core/policies/two_stage_fallback/ defines an ambiguity threshold between the two top values.

By using this dynamic value determined between weightings, this was significantly more reliable and less prone to errors compared to my initial naive thresholding - which required modification with every dataset change. 

Before adding pretraining data:
```
[[202   0   0   1   2   0   2   5]
 [  0 170   4   0   0   2   0   1]
 [  1  10 201   0   0   0   3   5]
 [  0   0   0 174   0   1   1   2]
 [  2   2   0   0 189   0   0   4]
 [  0   0   0   0   0 249   0   0]
 [  2   0   2   0   0   2 205   1]
 [  9   6   3   3   4   3   0 165]]
```
`Average accuracy across 15 iters: 0.9421143671143672`

"How are you":
```[IntentClassifier/predictions]  Intent: affirmation | Probability: 0.0081
[IntentClassifier/predictions]  Intent: capability | Probability: 0.0427
[IntentClassifier/predictions]  Intent: clarification | Probability: 0.0206
[IntentClassifier/predictions]  Intent: farewell | Probability: 0.0085
[IntentClassifier/predictions]  Intent: greeting | Probability: 0.4168
[IntentClassifier/predictions]  Intent: knowledge_question | Probability: 0.0364
[IntentClassifier/predictions]  Intent: negation | Probability: 0.0061
[IntentClassifier/predictions]  Intent: smalltalk | Probability: 0.4608
Result likelihood is 0.043963556784508806
[debugger] classifier is unsure what to decide; values are 0.46078469764499075 vs 0.41682114086048194
[Claudia] I didn't recognise that. Could you please rephrase or ask something else? 
```


With pretraining:
```
[[  3   0   0   1   0   0   0   0   0   0   0]
 [  0 203   0   0   1   1   0   0   6   1   4]
 [  0   0 170   5   0   0   0   0   2   0   2]
 [  0   0  13 195   0   0   0   0   2   7   5]
 [  0   0   0   0 176   0   0   0   2   1   2]
 [  0   0   0   0   1 194   0   0   0   0   4]
 [  0   0   0   0   0   0   2   0   1   0   0]
 [  0   0   0   0   0   0   1   0   1   0   0]
 [  0   0   0   0   0   0   0   0 249   0   0]
 [  0   3   1   5   0   0   0   0   4 200   2]
 [  0   7   8   1   0   7   0   0   6   0 166]]
```
`[IntentClassifier] Trained intent classification model has accuracy: 0.9357357357357358`
`[IntentClassifier] Average accuracy across 15 iters: 0.9325021280857244`


"How are you":
```
[IntentClassifier/predictions]  Intent: action | Probability: 0.0047
[IntentClassifier/predictions]  Intent: affirmation | Probability: 0.0091
[IntentClassifier/predictions]  Intent: capability | Probability: 0.0442
[IntentClassifier/predictions]  Intent: clarification | Probability: 0.0214
[IntentClassifier/predictions]  Intent: farewell | Probability: 0.0094
[IntentClassifier/predictions]  Intent: greeting | Probability: 0.5230
[IntentClassifier/predictions]  Intent: identity_mgmt_input | Probability: 0.0063
[IntentClassifier/predictions]  Intent: identity_mgmt_retrieve | Probability: 0.0036
[IntentClassifier/predictions]  Intent: knowledge_question | Probability: 0.0403
[IntentClassifier/predictions]  Intent: negation | Probability: 0.0067
[IntentClassifier/predictions]  Intent: smalltalk | Probability: 0.3313
Result likelihood is 0.19174695333023395
[debugger] Input was classified as: greeting
[Claudia] Hello! I'm Claudia, your home assistant. How about you? What's your name? You can let me know by saying "my name is Wendy", for example.
```






