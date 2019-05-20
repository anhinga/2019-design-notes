# Interactive framework for developing, editing, and experimenting with neuromorphic systems with vector-like flows

In recent years our group created a number of prototypes in this general direction under

https://github.com/anhinga/fluid

and 

https://github.com/jsa-aerial/DMM

Also I started to conduct some relevant experiments under

https://github.com/anhinga/2019-python-drafts

Here we'll try to sketch how the overall framework of this kind should look (from the user viewpoint and from the viewpoint of software architecture).

## History

[History.md](History.md) describes own relevant prototypes for neuromorphic dataflow systems with vector-like flows (or their pieces) in recent years. 

## Core (stage 1)

The requirement for the **core** of the interactive system is the ability to fluently perform various experiments (e.g. in the style of visiual synthesis demonstrated in May and June 2015) by using visual programming and, more specifically, **interactive visual livecoding**. In particular, one should be able to visualize the changing network topology as a graph, and to edit the network both via a **"graph editor controller"**, and by sending textual commands. It should be possible to control numbers by sliders. There should be some further bare-bones infrastructure (including the ability to interactively adjust the frame rate, or pause/resume).

Core design and implementation should be done so as to make the following Stage 2 possible without drastic breaking changes.

For the **Architecture notes (in progress)** see [Core-architecture-notes.md](Core-architecture-notes.md)

## Extensions (stage 2)

The requirements for extensions include the ability to handle various types of input and output sources: images, video, camera feeds, audio, text, EEG streams, etc. In particular, one needs to be able to receive streams of **deltas** for the parameters of the system from machine learning modules. These deltas are to be treated by the system as suggestions for parameter changes, and the actual system might take such a suggestion or a linear combination of one or several such suggestions and apply them, or it might use those suggestions in any other way it sees fit (the experimental setup should allow us to experiment with this).

One should be able to handle a population of DMMs which work simultaneously in the same substrate, and might interact between themselves (or not). One should be able to create and manage checkpoints, so that one can backtrack to certain state and, perhaps, resume evolution in a different direction. Random numbers generation and logging should be made in such a fashion as to make the runs reproducible.

## Optional extensions (stage 3)

These extensions are not a must. It's OK to have an implementation of Stages 1 and 2 not taking this into account at all.

Multimachine setup. Multiuser setup with simultaneously running and possibly interacting experiments by various people. GPU or TPU usage.

We assume that Stage 2 should be capable of exchanging information via Websockets, so a rather constrained and awkward version of rudimentary Stage 3 functionality would be automatically available by the virtue of being able to interact via Websockets.

But doing this well is a problem for another day.




