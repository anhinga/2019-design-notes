# Automated synthesis of dataflow systems with vector-like flows.

(DMM-specific machine learning and related topics)

Traditional neural nets are a subclass of DMMs, so the enormous body of machine learning research is applicable.

Here I am trying to record DMM-specific aspects, and also the evolution of my thinking about DMM synthesis.

## Highlights

 * DMMs with very small number of neurons can be quite expressive, because there is no coupling between the number of neurons and the dimensions of vectors (the DMM architecture is friendly even towards infinite-dimensional vectors handled by a single neuron).

   So a lot of meaningful machine learning tasks can have small number of trainable parameters.

 * DMMs are often used in lieu of programs, and as such they tend to have sparse connectivity.

   So the motive of synthesizing models with sparse matrices is quite prominent.

 * DMMs are capable of conveniently editing themselves or other DMMs.

   So the motive of "learning to learn" is very prominent.

 * DMMs comfortably host populations of "smaller" DMMs within themselves.

   So this is a nice setup for artificial evolution and for self-modifying evolutionary schemes.
   
