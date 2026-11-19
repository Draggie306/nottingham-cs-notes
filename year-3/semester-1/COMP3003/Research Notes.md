

## Overview



## AI model


Discrete Diffusion Models: A Unified Framework from Tokenization to Generation - https://arxiv.org/abs/2607.13431
- Paper suggests that autoregressive (AR) models perform an irrevocable, single-pass left-to-right decoding. This limits models' ability to perform global planning, escape local optima or restraints, or refine earlier decisions based on later structure - inherently limiting the ability for infilling (fill in the blank given prior and forward context), controllable generation or long-context reading
- Each step in the generation process allows the diffusion model generation to access to the entire state of the model and perform global, bidirectional generation. This allows it to "plan holistically, correcting early mistakes, coordinating long-range dependencies, ans satisfying constraints that span the entire output". This ability also helps with infilling: corrupting some parts of the 

Next Semantic Scale Prediction via Hierarchical Diffusion Language Models - https://arxiv.org/pdf/2510.08632
- Builds a more generalised/coarse structure: lower-level tokens with detailed semantics are mapped to higher level tokens with less detailed semantics. 
- Basic masking as used with discrete diffusion models are binary with no semantics between the layers, whereas intermediate steps 
- Not too sure how this could link to the current idea? 


Structured denoising diffusion models in discrete state-spaces: https://arxiv.org/pdf/2107.03006, implemented in https://github.com/cloneofsimo/d3pm .
- Implements the ideas from: https://github.com/uclaml/DNDM/tree/main/discrete_diffusion/discrete_diffusions

Research findings:
- The D3PM model supports conditional embedding, used to influence the model.
	- This could change based on difficulty or - more interestingly - focus or other derived brain data. 
- Training example remains hard
- Game space itself is modified by how players experience it.
- Inpainting; repairing or modifying an existing state, can be done by 

- Hierarchical model stages.


Question: not clear how brain data feeds into this. Might be worth diagram/explaining how brain data. Comment: what does game layouts mean and why game layouts - are you making it more difficult which sets up requirements about comparability vs different. 

- Warrants further development: can be contrived: barriers to exploration, what actually has an effect on the player's brain. Don't just come at this from a technical POV; what will users experience that is fun that has an effect on their cognitive state/brain activity.
- Literature on "what actually makes a game": game flow; constant task feedback; not easy but appropriate for the layer.
- Tracy Fullaton (?): players, goals and objectives; procedures Jesse Schell Art of Game Design: do not forget the **what** and build understanding of how the model makes game good. 

2 different systems: may be a disconnect. May be best to focus on diffusion generation: what does it mean to generate level depending on focus level. 

L brain activity/right: regression or some sort of analysis; script to analyse the data to inform: different features including dips and normalised levels can be used to define what should manifest in the game.

Look at brain data end; look at game end; do some prototyping of both.

Interim report: detailed sections/headings

Could be better to start with another game example e.g. the Mario paper; may be more difficult task to create a game;