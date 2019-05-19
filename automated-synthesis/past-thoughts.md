# Past thoughts summary

Here I am trying to record the evolution of my thinking about DMM synthesis.

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

Explore training the nets with piecewise bilinear neurons based on ReLU (this is the activation function: g(x, y) = max(0, x)∗max(0, y) ): Section 1.3.2 of https://arxiv.org/abs/1606.09470

DMM-based program synthesis is similar to finding neural net architecture while assembling the network from layers and modules:
Section 4 of https://arxiv.org/abs/1706.00648 (Section 4 here is generally useful for learning)

### Tension between flexibility and efficiency, and also between gradient-based and derivative-free methods. 



## Starting from 2019 - first experiments with training the sparse networks
