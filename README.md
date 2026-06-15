# Concept-Vector

The following is the prompt used to initialize work on this project (see [prompts/intro.md](https://github.com/truehumanexe/concept_vector/blob/main/prompts/intro.md)), and it serves as a good summary of the project as well as a good source for LLM evaluated critical feedback for the curious.

**BEGIN**

This is a project called "concept-vectors." It replaces the arbitrary latent dimensions of traditional word embeddings (e.g. Word2Vec, LLM embedding layers) with deterministic, human-defined semantic components that have been distilled from an LLM using a pre-defined scoring method. A need for restructuring of the model's tokenization or vocabulary alignment layers to accommodate this framework is understood and is explicitly outside the scope of this task.

This project has the following objectives:
1. **Computational Efficiency & Memory Reduction:** Restricting the core vector space density to a highly compressed footprint (< 1000).
2. **Deterministic Controllability:** Embedding explicit, isolated semantic components for areas of governance (e.g., Formality, Insult, Hedonics) to allow for predictable post-hoc filtering or scalar logit masking at the decoder layer.
3. **Structural Explainability:** Allowing for easier evaluation of how context shifts semantic baselines during attention execution.
    - Given the following vectors: [ Static ]; [ Dynamic || Trainable ] 
    - The static component is predefined during the distillation process, locked, and treated as a reference
    - The dynamic component is a copy of the static component that is combined with the trainable/undefined components and passed through attention/transformer layers
    - The trainable components allow an LLM to generate meaning that goes beyond the scope of concept-vectors
    - Changes between the static vector and dynamic vector components are measurable

**END**

## Demo

For a demonstration of semantic searching of concept vectors see [notebooks/scratch.ipynb](https://github.com/truehumanexe/concept_vector/blob/main/notebooks/scratch.ipynb)

For a human readable list of concepts, see [docs/concept_descriptions.md](https://github.com/truehumanexe/concept_vector/blob/main/docs/concept_descriptions.md)


## Design

**Method:** This project was made in tandem with Gemini for ideation, feedback, and iteration, as well as meta-llama-3.1-8b-instruct for the distillation process.

**Distillation:** A model is requested to use a 5-point scale [ 0-4 ] to rank the relationship between a given word and a predefined set of concepts. 
- This scale was chosen to allow a model to easily provide a numerical score for a given word such as "boy" and a given concept such as "gender" which doesn't have numerical significance. Or to allow objects on massively different scales to be mapped without having to take account of differing physical units or absurd number scales. E.g. the word "universe" vs. the word "atom" when evaluated under the concept of "scale". 
- The five point numerical scales mapes to five ordinal relevance categories: irrelevant (0), minor (1), moderate (2), major (3), and extreme (4)
- During ranking, each word is passed statelessly with a system prompt defined by templates built from files within prompt directory to avoid context drift. See the function distill() from distill.py

**Normalization:** No normalization has been applied to the vector database, but tanh or sigmoid is the end target. *Note: Cosine similarity does not work on these vectors.*

**Concerns**
- Concept-vectors lose the clean vector math associated with systems like word2vec and the implications of this are unclear.
- Generating a large vector vocabulary via distillation requires significant resources, so this repo only serves as a small demonstration of the idea.
- vector dot product, while functional, may not be the best vector search method. There is a need for exploration of optimal searching.

## Misc.

For future work direction and speculative use cases, see [/notes](https://github.com/truehumanexe/concept_vector/tree/main/notes)





