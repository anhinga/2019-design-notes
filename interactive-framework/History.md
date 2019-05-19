# Historical notes

The field of visual dataflow programming goes decades back and includes such well-known examples as Pure Data, LabVIEW and more; visual programming in general is even larger:

https://en.wikipedia.org/wiki/Visual_programming_language

Our own relevant prototypes for neuromorphic dataflow systems with vector-like flows (or their pieces) in recent years include

## Project Fluid, in https://github.com/anhinga/fluid 

Programming language: Processing (a simplified Java with awesome visual facilities, popular in the digital artistic community).

### Pre-DMM

May 2015 and June 2015 experiments in Project Fluid with the software architecture described in https://arxiv.org/abs/1601.00713

Here we have a system for artistic synthesis of visual animations via a programmable dataflow system, which admits interactive controllers to manipulate the parameters of the nodes.

The architecture of June 2015 experiments also allows to programmatically edit the dataflow program itself while it is running and enables visualization of the changing dataflow graph.

What is missing is an interactive controller which would allow to edit the dataflow program interactively, and not just programmatically.

The archictecture allows to grow the network by making copies of subgraphs. Another useful operation there is "S-insert".

June 2018 in `atparty-2018/surreal_webcam` directory of Project Fluid - feed webcam or external movie into May 2015 archicture.

### Early DMMs

August 2015 in Project Fluid - continuous cellular automata

### Lightweight pure DMMs editing their own network matrices (controlling connectivity and weights) while the network is running

In these cases, the dataflow program modifies itself by changing its own network matrix.

August 2016 in `Lightweight_Pure_DMMs` directory of Project Fluid - first self-modifying Lightweight pure DMMs.

June 2018 in `atparty-2018/game_of_afterlife` directory of Project Fluid - self-modifying Lightweight pure DMMs producing interesting emerging phenomena. The last of experiments in this series also drives audio output.

June-September 2018 in `Lightweight_Evolutionary` directory of Project Fluid - first experiments with interactive evolution of a small population of Lightweight pure DMMs.

September 2018 in https://github.com/anhinga/fluid_drafts - external movies are fed into Lightweight pure DMMs.

## DMM project, in https://github.com/jsa-aerial/DMM

Programming language: Clojure (an ultramodern JVM-based Lisp, a very nice language friendly towards programming with immitable structures)

Dataflow matrix machines based on streams of V-values, as described in our paper, "Dataflow Matrix Machines and V-values: a Bridge between Programs and Neural Nets", https://arxiv.org/abs/1712.07447

This is our main "professional" DMM engine (although it is very experimental).

Visual experiments were using Quil, a Clojure wrapper around Processing.

July 2017 - first visual experiments with a neuron emitting mouse position and a neuron accumulating a list of mouse clicks: https://github.com/jsa-aerial/DMM/tree/master/examples/dmm/quil-controlled

January-April 2018 - first experiments enabling interactive changes of the running neural network (including the topology of its graph) via text commands (sent from Quil window or from a Seasaw-based editor ("Seesaw turns the Horror of Swing into a friendly, well-documented, Clojure library")). The changes are eventually sent to a dedicated neuron, which listens on a core.async channel. This dedicated neuron produces updates for the network matrix (the matrix encoding network connectivity and weight) or for other elements of the network: https://github.com/jsa-aerial/DMM/blob/master/examples/dmm/quil-controlled/interactive and Section 1.1 of https://github.com/jsa-aerial/DMM/tree/master/technical-report-2018




## Python code snippers, in https://github.com/anhinga/2019-python-drafts

My current thinking is that the next version of the DMM engine should probably be in Python, in order to gain access to various well-developed machine learning frameworks (all the best ones seem to be Python-centered, with other languages coming as an afterthought at most), and in order to make it possible for more people to easily work with DMMs.

Some preliminary experiments were done in April 2019, most importantly in interactively editing a directed graph in Dash Cytoscape.

We also made sure that Trio-based websockets work for us (websockets are important when one does not want to implement the whole system as a single monolithic process; they also make it relatively easy to implement interactions between different programming languages). We started preliminary work with VisPy, which is the state-of-the-art OpenGL wrapper in Python (trying to overcome our dependency on Processing).


