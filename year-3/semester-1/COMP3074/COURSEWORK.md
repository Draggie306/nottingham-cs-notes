

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

