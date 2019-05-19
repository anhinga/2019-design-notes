# Past thoughts summary

Here I am trying to record the evolution of my thinking about DMM synthesis.

## Before 2016 - not thinking about them as neural nets (only thinking about them as continuously deformable programs)

Programs are genes. (Or existence of a link in a network is a gene.)

Coefficients in the linear combinations of programs (or weights on links) are expressions of those genes.

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

DMMS had effectively became examples of that architecture, with activations functions playing the role of inflexible components in the flexible tissue.

Our slide deck from that October 2015 conference had a slide saying

 * Looking for new methods to synthesize programs as matrices.
 
 * Looking for new idioms of higher-order programming expressed interms of changing the matrix elements.
 
 * It is not difficult to have rich sets of template operations.
 
 * Continuous program transformations and continuous trajectories inlarge spaces of programs are therefore available.
 
 * One can evolve programs in continuous fashion.
 
 * One can sample continuous trajectories in a space of programs.
 
(slide 43 of https://www.cs.brandeis.edu/~bukatin/LinearModelsGCAIOct2015.pdf)


## Starting from 2016 - keeping in mind that DMMs are generalized neural nets

## Starting from 2019 - first experiments with training the sparse networks
