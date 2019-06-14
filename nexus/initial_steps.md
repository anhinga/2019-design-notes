### Initial steps in Nexus design.

We start with the flat version first, then add nested indices side of things later.

Per `jsa-aerial` remark, while we aim for our matrices and vectors to be sparse, we can use ordinary matrices and vectors 
in the first implementation, and just keep them _de facto_ sparse.

The two natural versions for the flat version seem to be: 
  * vectors are really one-dimensional, matrices and images are embedded into them as needed via reshaping of indices, and _matrix multiplication_ is used "as is" (the overall set of neuron outputs (inputs of **W**) is a vector of vectors, i.e. a matrix);
  * vectors are matrices, in the spirit of "extended pure lightweight dmms", where matrices in the streams are allowed to be larger than 
    the network matrices (which, let's say, are "kept in an upper left corners of matrices in the streams"), and _tensor contraction_ is used as matrix multiplciation (the overall set of neurons outputs (inputs of **W**) is a vector of matrices, i.e. a 3D tensor).
    
