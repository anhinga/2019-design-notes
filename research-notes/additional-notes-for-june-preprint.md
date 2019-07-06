#### The case of comparable sizes for **W** and **Y** might be particularly interesting.

For example, _DxN_ and _NxD_ (where _N=D_ is an important case).

#### For this situation shader-style experiments are attractive, even without learning.

E.g. If _N=D_, we have 3 square matrices, **X**, **Y**, and **W**, and we can draw them separately in monochrome and jointly in, e.g., RGB.

And the simple starting point for a possible series of experiments is when the loop is not even closed.
That is, take 2 monochrome shaders, take the matrix product of their pictures, and leave the loop open
(so both monochrome outputs, **W** and **Y**, are external input flows not depending on **X**)...

#### Even for non-comparable sizes, one can always splice **Y** into **W**, or **W** into **Y**.

And then one obtains **A(A<sup>T</sup>)** matrix product as a part of **WY** overall product.

#### Another interesting thing in connection with all this is sparsity experiments. 

(A note to myself: look at **A(A<sup>T</sup>)** matrix product for a random sparse matrix **A** (square or rectangular).)
