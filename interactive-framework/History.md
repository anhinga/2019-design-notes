# Historical notes

The field of visual dataflow programming goes decades back and includes such well-known examples as Pure Data, LabVIEW and more; visual programming in general is even larger:

https://en.wikipedia.org/wiki/Visual_programming_language

Our own relevant prototypes for neuromorphic dataflow systems with vector-like flows or their pieces in recent years include

## Project Fluid, in https://github.com/anhinga/fluid 

Programming language: Processing (a simplified Java with awesome visual facilities, populated in the digital artistic community).

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

June 2018 in `atparty-2018/game_of_afterlife` directory of Project Fluid - self-modifying Lightweight pure DMMs producing interesting emerging phenomena. The last of experiments in this series also drived audio output.

June-September 2018 in `Lightweight_Evolutionary` directory of Project Fluid - first experiments with interactive evolution of a small population of Lightweight pure DMMs.

September 2018 in https://github.com/anhinga/fluid_drafts - external movies are fed into Lightweight pure DMMs.

## DMM project, in https://github.com/jsa-aerial/DMM

## Python code snippers, in https://github.com/anhinga/2019-python-drafts


