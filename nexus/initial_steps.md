### Initial steps in Nexus design.

We start with the flat version first, then add nested indices side of things later.

Per `jsa-aerial` remark, while we aim for our matrices and vectors to be sparse, we can use ordinary matrices and vectors 
in the first implementation, and just keep them _de facto_ sparse.

The two natural versions for the flat version seem to be: 
  * vectors are really one-dimensional, matrices and images are embedded into them as needed via reshaping of indices, and _matrix multiplication_ is used "as is" (the overall set of neuron outputs (inputs of **W**) is a vector of vectors, i.e. a matrix);
  * vectors are matrices, in the spirit of "extended pure lightweight dmms", where matrices in the streams are allowed to be larger than the network matrices (which, let's say, are "kept in an upper left corners of matrices in the streams"), and _tensor contraction_ is used as matrix multiplciation (the overall set of neurons outputs (inputs of **W**) is a vector of matrices, i.e. a 3D tensor, and the **W** must produce a similar thing after tensor contraction, but **W** itself is a 2D thing).
    
In the current frameworks, it tends to be much easier to do matrix multiplication (compared to tensor contraction), so we'll use that route first (but reserve the second version as a possible future option, and also as a guide on how to choose reshapes). This way we'll be close to conventional practice in neural nets (which tend to flatten an image, if a linear operator needs to be applied to it, e.g. at the initial embedding).
    
The asymmetry between inputs and outputs is important (which is why we prefer to think about all matrices here as rectangular - more on that will be written later). Just like a row of **W** can use the whole set of neuron outputs (inputs of **W**) to produce a new single neuron input, a neuron should be able to be non-local in general and use the whole set of neuron inputs, if it feels like that. However, a fixed neuron output can be only produced by one neuron (or kept at const/produced by zero neurons). It's OK for one neuron to produce several outputs _if convenient_. 

During network "stop the world, expand the world, resume the world" occasional adjustment, slots produced by zero neurons can be filled; however the existing "non-linear wiring" must remain untouched. If one expands a matrix and wants to represent it as a continuous piece of 1D array without copying, one would need to allocate the new set of indices for the whole thing (might not be implemented at first).

***

It would be nice to just do it at NumPy first, but I think it makes sense to do this in PyTorch first, so that all possible issues with autograd and such would become immediately apparent.
