# Flattening and reshaping of V-values

This continues the line of thought from https://github.com/jsa-aerial/DMM/blob/master/design-notes/Mid-2017/numerical-keys.md

In order to apply standard tools from machine learning frameworks, one should have flat sparse vectors and flat sparse matrices.

A vector of sparse vectors is a sparse matrix, so applying a sparse matrix to a vector of sparse vectors is simply a sparse matrix multiplication.

In this paradigm, various standard autograd tools and compilation to GPU/TPU are expected to more or less work now (although until quite recently doing this well for the sparse case was a problem; but the situation is improving in this sense).

## Plain V-values

The leaves are now not real numbers, but indices into one-dimensional array of numbers (or, when necessary, row and column indices of a matrix).

One only needs to maintain a single tree providing translations from tree paths to indices of a one-dimensional array. One would also like to have a one-dimensional array of tree paths providing the inverse translation.

Also a similar bidirectional translation for matrix rows and another one for matrix columns.

One needs to think about reshaping bidirectional translations (or extending the sizes of relevant arrays/matrices). In the initial versions, we'll just reserve sufficient space to avoid this issue.

We will need to provide custom reshaping maps from 1D-arrays to 2D-matrices (since among our 1D arrays we would have data which we'll need to use as network matrices).

(Note: implementation-wise the natural framework here is sparse matrices and sparse arrays; however `jsa-aerial` noted that one can just start with ordinary matrices and arrays storing all those zeros for initial experiments, and transition to sparse matrices later on.)

## Extended V-values

For V-values with extended leaf structure (Section 5.3 of https://arxiv.org/abs/1712.07447 ), one should probably consider the structure containing the arrays with elements taylored for each kind of linear streams involved in the particular construction (See Section 5.3 of that paper for details: so, instead of keeping one tree with combined leaves, we make separate trees, one tree for each kind of leaves, and then flatten those).

---

This seems to be the right direction, in terms of starting to do machine learning applications.

---

**Note (Dec 15, 2020):** See https://github.com/scikit-hep/awkward-1.0 "Manipulate JSON-like data with NumPy-like idioms".

This might be another possible solution to this problem instead of flattening.

(Of course, another way is simply to use Julia Flux and Zygote and avoid flattening.)

---

See also **pytree** protocol of JAX:

https://jax.readthedocs.io/en/latest/pytrees.html

https://jax.readthedocs.io/en/latest/jax.tree_util.html

---

**Note (Dec 21, 2020):** Adding missing info on search for _python dynamic perfect hashing_ and related things (from Feb 24, 2019):

https://en.wikipedia.org/wiki/Perfect_hash_function (with or without order preservation)

https://github.com/eddieantonio/perfection

and the associated very long "mini-book" 1997 Theor.Comp.Sci. open access article by Czech et al, "Perfect Hashing":

https://www.sciencedirect.com/science/article/pii/S0304397596001466

One should pay attention to ref [33] or [31] and pages 58, 67, 99, and immediately following those in that "mini-book".

In particular this Python program looks good (we should benchmark it vs. naive ways):

https://github.com/eddieantonio/perfection/blob/master/perfection/czech.py

"Use the Czech et al. method for generating **minimal perfect hashes for strings**" ("A minimal perfect hash function is a perfect hash function that maps n keys to n consecutive integers – usually the numbers from 0 to n − 1 or from 1 to n")
