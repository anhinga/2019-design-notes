# Architecture notes (preliminary introduction)

I don't have a ready final architecture in my mind, which just needs to be written. The [History.md](History.md) gives me some ideas and some warnings about potential problems.

So I'll start just with putting notes about those ideas and those problems here.

## Preliminary snippets

### Graph editor controller for a changing graph

This is an interesting problem. If one edits on the level of network matrix, one can trigger a change without knowing the exact state of the matrix. Even if the change algebraically depends on the moving target, still one can use the current snapshot of that target to get the needed values.

But with explicit graph editing one cannot play it this way: if a graph is changing in front of you, it would not be possible to reasonably manipulate it with a mouse.

So a tentative solution is as follows: if one is dealing with a morphing graph, one makes a copy (which is a frozen in time snapshot of the graph in question), edits it, and sends forward a delta generated by this edit. We expect that any given delta can always be applied to any graph whatsoever (this is certainly true, if one does it on the level of weight-connectivity matrices corresponding to the graphs, one can always add two matrices, and any matrix over appropriate signature of indices has an interpretation as a network graph).

It's all good for small graphs. Navigating and editing large graphs is a separate non-trivial problem (but it should at least be considered for Stage 1).

The exact interplay of graph and matrix representations also requires further thoughts. Do we store both and make sure that they are always in sync? So we have further topic for meditation on graph controllers.

### Various kinds of streamed objects

We were always able to stick to one kind of streamed objects in our experiments. First, these were fixed-resolution images (in the pre-DMM experiments), then numbers (in early DMMs), then network-sized matrices (in Lightweight pure DMMs), then finally V-values (and V-values are universal enough to allow to embed any reasonable streams of objects into streams of appropriately crafted V-values (Section 5.3 of https://arxiv.org/abs/1712.07447 )).

However, in principle, nothing precludes having different kinds of streams in a DMM (Section 3 of https://arxiv.org/abs/1605.05296 ). And I really want to avoid making a decision to stick to a particular kind of streams at this point, even if that kind is sufficiently universal.

So, if we are just talking about stream-based programming (forgetting about the requirement of being able to take linear combinations for a bit), we might want to say that an element of the stream is to belong to a specific Class. We might also say that there is an Empty element (belonging to a specific subclass of that Class), that a receiver which does not know what to do with an element of a particular kind always has the right to cast it to Empty (type mismatch errors are not allowed, a warning signal can be emitted, but the network must be able to run indefinitely long without stopping no matter what ("it's a brain, and a brain should not segfault or throw exception")). And when there is a need to take a linear combination, it is always OK to interpret Empty as Zero. So an input node of a neuron is responsible for performing a linear combination one way or another regardless of what kind of objects it got.

This is obviously too flexible for taking nice derivatives or for GPU execution. We had some ideas of inter-rewrite (reshape) between plain V-values and sparse one-dimensional vectors and sparse two-dimensional matrices as necessary, but plain V-values are more structured than this "anything goes, just make it a subclass" way. If one introduces "sufficiently interesting leaves" into V-values (per Section 5.3 of https://arxiv.org/abs/1712.07447 ) then one might lose the ability to take nice derivatives or to execute on GPU as well.

---

(**Note**: We now have a nice schema for flattening extended V-values as well: https://github.com/anhinga/2019-design-notes/blob/master/automated-synthesis/flattening-of-v-values.md

This is certainly a strong argument for structuring this around V-values, and not around a class of things.

And then all standard arguments apply: classes are not language-agnostic, and that's bad (we don't want to be tied to a particular language). V-values provide JSON-like syntax (essentially, nested dictionary-based variant of Lisp syntax), and that is very expressive and allows for all kinds of interesting experiments with software architecture.)

---

So we might have to say that gradient-based methods and GPU-capable runs would only happen for certain types of networks or subnetworks, and that the completely general runs must stick to derivative-free optimization methods and to CPU not-too-optimized execution, at least for the time being.

This is not set in stone - the introduction of Class of legal streamable objects does not preclude us from imposing further discipline, if we feel like it. In particular, here the demand to be able to do Stage 2 without drastic breaking changes comes into play. We'll need to consider what's compatible with a nice Stage 2 implementation (in particular, our decisions here must be compatible with the ability to interface with sparse matrix-based models from something like PyTorch and to use those models for learning this kind of machines).

In any case, it is the system responsibility to represent a task which it wants something like **pytorch-sparse** with its autograd and GPU-capability to handle in the appropriate shape. So the system would need to be aware of the subclass of problems which can be so represented. (For a more general solution, if one is not too concerned about speed, e.g. when a paticular problem is small, a hand-crafted module for **evolution strategies without parallelization (ouch, that is really slow)** is always feasible to implement.)

### Two-stroke engine

The two-stroke engine remains as before. As noted in Section 6.4 of https://arxiv.org/abs/1712.07447 pre-DMM experiments involve a shift stage following the application of activation function stage on each engine cycle, and this pattern (typical for programs written in the dataflow formalism manually) corresponds to taking a linear combination with one non-zero summand with coefficient 1. The shift stage happens anyway, so it is convenient when it is always understood as a linear combination (regardless of implementation details, which might vary).

### Copying subgraphs

The idea of typically building a program by mostly copying the template subgraphs, creating new, more compicated templates, and slightly tweaking the resulting graph and its connections is cool (see Section 4 of https://arxiv.org/abs/1601.00713 ).

In some sense, there is a lot of good material in pre-DMM formalism ( https://arxiv.org/abs/1601.00713 and May-June 2015 experiments), which we did not have a chance to put in practice (although we have the formulas for copying subgraph in the DMM-based matrix formalism, see Section 4 of https://arxiv.org/abs/1606.09470 ; but we don't have any of this in DMM software produced in 2016-2018).

One of the purposes of the next implementation is to assemble all those good pieces together, including ones from the pre-DMM epoch.

### Internalization

The key principle we are trying to follow is that the edits should be done by triggering appropriate neurons.

We actually want to extend this principle further and think about controllers as neurons or subgraphs. It requires some extra thinking to do it this way, but it's really helpful in many respects. The most important difference between DMMs and neural nets is that one can really program in DMMs, and it is not difficult to express handcrafted controllers as DMMs (subnetworks), or at least to wrap activation functions around them. 

If we can build "graph edit controller" and "graph visualizer" in this fashion, then we should be able to build other controllers which tend to be much simpler than "graph-related controllers".

### Second thoughts about internalization

Looking back at our practices at various projects in 2015-2018, I think it is better at this stage to achieve a more clean separation between model (DMM), views into that model, and controllers, allowing to influence the model. As usual, controllers are often based on pieces of views, and there will be DMM neurons responsible for handling V-values received from "local software" interfacing with controller software (our experience is that this usually ends up being a two-stager - controller implementation is using some external framework, and this framework dictates how the event information should be locally received, and then the local software sends an async V-value into a listening neuron).

So, I think, we are leaning towards adapting the ways this is currently handled in our Clojure experiments, e.g. https://github.com/jsa-aerial/DMM/blob/master/examples/dmm/quil-controlled/jul_13_2017_experiment.clj

Moreover, I can easily see splitting the viewers and controllers to separate processes connected via something like Websockets (we were leaning towards this recently in the context of https://github.com/jsa-aerial/DMM/tree/master/examples/dmm/quil-controlled/interactive although we never implemented it that way).

(Note: so, at least at first, I consider internalization to be limited to the following requirement: editing updates (or suggestions for those updates) are effected by triggering specially crafted **update neurons**; this is still a must. But the editing system does not have to be represented as a DMM (and we only expect editing systems represented by a DMM to appear at later stages).)

## Let's assume (without commitment) that this is a model-view-controller architecture

 * The model part will be guided by this thinking: https://github.com/anhinga/2019-design-notes/blob/master/automated-synthesis/flattening-of-v-values.md
 
 * There can be multiple viewers and controllers, and some of them can be pretty ad hoc (in the style of https://github.com/jsa-aerial/DMM/tree/master/examples/dmm/quil-controlled/interactive experiments in 2018), but we would like to also design something more systematic (that's where our thoughts about "graph editor controller" fit, and here one would also want/need to control what one sees, and how one sees it)
 
 * So far we were using ad hoc practice of controlling the model (the DMM) by the graphical framework frame rate. This was convenient in many respects, but it does interfere with model-viewer separation. This is something to ponder.
 