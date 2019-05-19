# Historical notes

The field of visual dataflow programming goes decades back and includes such well-known examples as Pure Data, LabVIEW and more; visual programming in general is even larger:

https://en.wikipedia.org/wiki/Visual_programming_language

Our own relevant prototypes for neuromorphic dataflow systems with vector-like flows or their pieces in recent years include

## Project Fluid, in https://github.com/anhinga/fluid 

Programming language: Processing (a simplified Java with awesome visual facilities, populated in the digital artistic community).

### Pre-DMM

May 2015 and June 2015 experiments in https://github.com/anhinga/fluid with the software architecture described in https://arxiv.org/abs/1601.00713

Here we have a system for artistic synthesis of visual animations via a programmable dataflow system, which admits interactive controllers to manipulate the parameters of the nodes.

The architecture of June 2015 experiments also allows to programmatically edit the dataflow program itself while it is running and enables visualization of the changing dataflow graph.

What is missing is an interactive controller which would allow to edit the dataflow program interactively, and not just programmatically.

The archictecture allows to grow the network by making copies of subgraphs. Another useful operation there is "S-insert".

### Early DMMs

August 2015 - continuous cellular automata

### Lightweight pure DMMs 
