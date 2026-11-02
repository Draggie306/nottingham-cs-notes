


## AI model


Discrete Diffusion Models: A Unified Framework from Tokenization to Generation - https://arxiv.org/abs/2607.13431
- Paper suggests that autoregressive (AR) models perform an irrevocable, single-pass left-to-right decoding. This limits models' ability to perform global planning, escape local optima or restraints, or refine earlier decisions based on later structure - inherently limiting the ability for infilling (fill in the blank given prior and forward context), controllable generation or long-context reading
- Each step in the generation process allows the diffusion model generation to access to the entire state of the model and perform global, bidirectional generation. This allows it to "plan holistically, correcting early mistakes, coordinating long-range dependencies, ans satisfying constraints that span the entire output". This ability also helps with infilling: corrupting some parts of the 

Next Semantic Scale Prediction via Hierarchical Diffusion Language Models - https://arxiv.org/pdf/2510.08632
- 