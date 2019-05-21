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

   So the motive of "learning to learn" is very prominent - training the network to train itself better (or to train other networks better).

 * DMMs comfortably host populations of "smaller" DMMs within themselves.

   So this is a nice setup for artificial evolution and for self-modifying evolutionary schemes (note that neuroevolution and the "learning/evolving to evolve better" are becoming popular topics in the field lately). 


## Past thoughts summary

Overviewing the evolution of my thinking about DMM synthesis: [past-thoughts.md](past-thoughts.md)

## Flattening and reshaping of V-values

Flattening and reshaping of V-values for the purpose of being able to apply standard machine learning software tools, and also for the purpose of being able to construct flattened visualizations: [flattening-of-v-values.md](flattening-of-v-values.md)
