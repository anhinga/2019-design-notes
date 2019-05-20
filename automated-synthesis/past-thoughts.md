# Past thoughts summary

Here I am trying to record the evolution of my thinking about DMM synthesis. Note that while I was doing some conventional machine learning model training (including training of neural nets) in the past, the sketches below are mostly theoretical; the first machine learning experiments which can be said to be somewhat related to DMM specifics were only performed in February 2019.

## Before 2014

Let's try to figure our how to create continuously deformable programs.

If we can do that, it is highly likely that it will be much easier to synthesize them, than discrete programs.

## Before 2016 - not thinking about DMMs as neural nets (only thinking about them as continuously deformable programs)

Programs are genes. (Or existence of a link in a DMM network is a gene.)

Coefficients in the linear combinations of programs (or weights on links) are degrees of "gene expression" of those genes.

So, in the context of artificial evolution, working with linear streams allows to incorporate gene expression into evolutionary programming (Section 1 of our Fall 2015 https://easychair.org/publications/paper/Q4lW). 

Section 5 of the same paper also said: "Instead
of implementing everything in terms of architectures admitting linear combinations of single execution
runs one can use a hybrid approach, mixing these architectures and traditional software. In this context
we might be inspired by hybrid hardware connecting live neural tissue and electronic circuits.
One might decide to use large existing software components and try to automate the process of
connecting them together using flexible probabilistic connectors. Here one should note the progress in
automated generation of test suites for software systems.

Another hybrid approach involves the use of small inflexible components inside the flexible “tissue”
of linear models." 

DMMs had effectively became an example of hybrid architecture, with activations functions playing the role of inflexible components in the flexible tissue.

Our slide deck from that October 2015 conference had a slide saying

 * Looking for new methods to synthesize programs as matrices.
 
 * Looking for new idioms of higher-order programming expressed interms of changing the matrix elements.
 
 * It is not difficult to have rich sets of template operations.
 
 * Continuous program transformations and continuous trajectories in large spaces of programs are therefore available.
 
 * One can evolve programs in continuous fashion.
 
 * One can sample continuous trajectories in a space of programs.
 
(slide 43 of https://www.cs.brandeis.edu/~bukatin/LinearModelsGCAIOct2015.pdf)


## Starting from 2016 - keeping in mind that DMMs are generalized neural nets

Hope to learn readable programs via neural methods (mostly because DMMs can be pretty compact): Secton 4 of https://arxiv.org/abs/1603.09002

Would be nice to have a corpus of programs in a DMM-oriented language for training: Section 4 of https://arxiv.org/abs/1605.05296

'We envision having a sufficient collection of types of neurons capable of editing the (network matrix) to easily express the edits doable via the interactive high-level language mentioned above. We think about this informally as “self-referential completeness of the DMM signature relative to the language available to describe and edit the DMMs"': Section 1.6 of https://arxiv.org/abs/1605.05296 (this is important, if one wants to teach the network to edit itself meaningfully)

Explore training the nets with piecewise bilinear neurons based on ReLU (this is the activation function: g(x, y) = max(0, x)∗max(0, y) ): Section 1.3.2 of https://arxiv.org/abs/1606.09470

DMM-based program synthesis is similar to finding neural net architecture while assembling the network from layers and modules:
Section 4 of https://arxiv.org/abs/1706.00648 (Section 4 in this preprint is generally useful for learning, as well as not too different Section 10 of https://arxiv.org/abs/1712.07447 )

### Tension between flexibility and efficiency, and also between derivative-free methods and gradient-based methods. 

DMMs with V-values are very flexible. But this comes with a price: the parallelization is not-trivial, especially if one is looking forward towards using GPUs and such. Also standard autograd packages usually don't work well with this level of flexibility in tensors (they typically want tensors of fixed rank, and they've only recently started to work reasonably well with sparse tensors at all).

So, until one makes better progress towards parallelization and autograd for most flexible DMMs schemas involving V-values (vectors with tree-shaped structure of indices), using them comes with efficienct costs and also pushes one towards derivative-free methods (e.g. the flavor of "evolution strategies" introduced by OpenAI a couple of years ago: https://openai.com/blog/evolution-strategies/ or the schema we were sketching on paper in the last couple of years: https://github.com/jsa-aerial/DMM/blob/master/design-notes/Early-2017/population-coordinate-descent.md and Section 4 of https://github.com/jsa-aerial/DMM/tree/master/technical-report-2018 )

However, with the progress of autograd and GPU methods for sparse matrices, a compromise became possible: one can reshape indexes into appropriate one and two-dimensional structures and back, and the main irregularity one still needs to deal with is sparseness of vectors and matrices in question, which is much more feasible to deal with using available tools in some of the existing machine learning frameworks.


## Starting from 2019 - first experiments with training the sparse networks

I conducted this series of experiments in February-March 2019:

https://github.com/anhinga/synapses/blob/master/regularization.md

Normally, one does all kinds of strange tricks to achieve sparseness of resulting neural nets while dealing with dense nets during training (L_1 regularization is the most well known way of doing so, but there are other techniques as well).

The simple neuroevolutionary schema invented by Mocanu et al. allows to keep the connectivity pattern sparse at all times and to weed out the non-performing links replacing them with new candidate links.

If one views the links as genes, and the round of conventional training computing weights as figuring out the optimial gene expression, there is interesting interplay with our thoughts in Section 1 of our Fall 2015 https://easychair.org/publications/paper/Q4lW mentioned above. Of course, the fitness criterion is very simple here (if gene expression is low, then this gene is unnecessary), and the production of new genes is very simple minded (any possible new gene is equally likely to be created). The evolving population here is a population of single genes (here, genes = links between neurons), not of the networks.

In any case, this schema by Mocanu et al. is likely to be quite useful for DMM synthesis. That's what's prompted me to study it experimentally in February-March 2019.

