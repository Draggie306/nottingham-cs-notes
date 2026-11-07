
There are many parts of the data system for AI:

**People**, who both **collect** and **use** the data. 
- There are labellers/crowdworkers who collect and generate the data.
- Researchers
- People who use the data - advertisers (to target products towards a target audience), researchers (to write papers and publish research), industry (to build better products), governments (to discover what is going on in their country), law enforcement...

**The data itself**.
- How representative the data is - how far the data represents the population it was intended to.
- Coverage - black spots if the data was unable to cover a certain area
- Validity - if the data actually represents reality, and is not made up "faked"
	- Crowdworkers may be trying to get through their labelling quickly,
- Sources - data does not tell you where it was collected; as a result it can distort the outcome
	- e.g. if users have athsma then more likely to survive - all data was selected from a hospital where decisions could be made more quickly
- Reliability
- Pre-processing 

**Systems** and algorithms the data runs on
- The techniques are used
- The training data it is based on, e.g. classification
- The purpose the algorithms are deployed for

## Dealing with biased data

- Collecting a diverse data set from multiple sources
- Being aware of the biases for weighting strategies

**Ecological validity**: the extent to which study and data findings generalise to real-world settings.

[A paper](http://d-scholarship.pitt.edu/23198/1/SIGdial23.pdf) used real callers versus simulated callers, and found that recruited participants talk more and speak faster, whereas real users ask for more help and interrupt the system more. 


### Data sheets
Data sheets are an approach to provide metadata about the data source for transparency.

They typically include motivations, composition, the collection process, 


An example data sheet includes the Hate Speech Twitter Dataset. This was created to study the automatic detection of hate speech, and uses most varieties of English using the BCP-47 tag.

The **speaker demographic** of this data were a range of >1,500 anonymous Twitter accounts that could not be asked for demographic data. The **annotator demographic** included 1,065 crowdworkers, mostly women, from 20-40 years old. The **speech situation** is informal, online commentary in an environment more "designed" to foster negative discussion. The tweets were published between April 2013 and December 2015 


## Crowdsourcing


A distributed workforce is used for people who can perform virtual tasks - commonly to obtain labelled data to train AI systems. 


Crowdsourcing practices, inspired by best content analysis practices - a methodoogy in social sciences.
- Are labels from an external dataset, or were some relabelled?
- Are the lebellers experts or crowdworkers? How are they trained?
- Is a training example given in the paper? How is it screened?
- Compensation?

Crowdwork is often done in low-income countries, in precarious working conditions without rights to holidays, health insurances, minimum wage, a union to represent them, or any protection from rogue employers.


## Algorithmic solutions and transparency


### Debiasing word embedding
Word embeddings reflect bias in language, and therefore the vector arithmetic perpetuates the bias. **Hard and soft debiasing** are strategies used against this:

- Hard debiasing removes the gender-pair associations for gender neutral words
- Soft debiasing reduces the differences between the sets while maintaining as much similarity to the original embedding as possible. 

However, debiasing does not resolve the root of the problem: debiasing is considered a "superficial" fix in that they just hide, and do not remove the bias: debiasing also removes the number if appropriate analogies. The gender bias is still reflected in the distances between words in the embeddings and can therefore be recovered.  Even after debiasing, **implicit-gender words** (e.g., receptionist, hairdresser) still group together with other implicit-gender words of the same gender.


### LLMs and bias handling

1. Data: filtered and curated from low-quality and harmful data.
2. Model training (pre-training): learning language and reduce undesirable associations
3. Fine-tuning/alignment: RLHF, preference training (post-training), behavioural rules
4. Evaluation: red-teaming, adversarial prompting, bias and toxicity testing
5. Runtime safeguards: detecting and blocking harmful inputs and outputs
6. Monitoring & iteration: faliure identification for continuous improvement.
