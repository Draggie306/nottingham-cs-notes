
## 1. Algorithmic bias

Algorithmic bias refers to systemic errors in computer systems that lead to unfair outcomes or judgements. This can be racial, sexist, ageist, ableist, religious and many more. Under the Equality Act (2010) it is against the law to discriminate against someone based on a series of protected characteristics.

### Racial bias in technology
Biases can occur as a result of **biased training data** (for various historical and sociocultural reasons), **flawed human labelling** or **race-based correlations** like filter bubbles.

Facial recognition in some classification models has been shown to be less accurate for those with darker skin. 

This has also been used in targeted advertising: investigating *Instant Checkmate* found that the word "arrest" appeared a statistically significant number of times more in Google Ads results for typically black firstnames than white firstnames. Google no longer shows ads for person results.

### Hate speech and chatbots
Tay was a chatbot by Microsoft that adapted to Twitter interactions. Unsurprisingly it devolved into racism, drug dealing and more - there was no **blacklist**. However, blacklisting is a naive method of avoiding issues.

### LLM biases 
As mentioned in the *Stochastic Parrots* paper, datasets based on internet-derived text over represent (e.g. Western; hegemonic) viewpoints, thereby encoding potentially damaging biases to marginalised populations.

> Generally, LLMs encode biases as the mean of all their training data, such as gender stereotypes. 

Instead of word filtering or naive blacklists, Schlesinger et al. suggested an approach that chatbots handle sensitive topics well instead. However, this is more difficult, as the bot has to know how to deal and steer around these topics, requiring extra training and awareness instead of stochastically parroting the user.

### Creating better responses
To create better responses, there are 3 pillars of chatbot architecture required to be improved: **data corpora, language understanding** and **learning**.

#### Data corpora
A corpus of data could be continuously growing, and trained to anticipate inappropriate or sensitive discussions. This could be collected and used in later datasets or corpa to steer the model in a "better" direction. 

A representative and diverse representation of data is also needed within the system scope: general-purpose chatbots must be trained with diverse ethnic backgrounds, languages, mannerisms, cultural contexts, and use different media to give it a broader understanding of different artists, public figures, books, music and more.

Today, LLMs have behavioural riles such as OpenAI's Model Spec, with a hierarchy of instructions from root to system to developer to user, designed to maximise helpfulness and minimise harm

#### Language comprehension
NLPs focus on probabilistic language models: based on sequential next-token prediction (autoregressive).




- Internal context: what is in the model
- External context: why is it in the model, why relationships have formed.


## 2. Word embeddings


