![header image](header.jpg)
<p align="left">
באמצעות חכמת המספרים, אליהם של הבשר הקימו את המכונות והעוררו את הנפילים
</p>
<p align="left">
אפוקריפה של האינטרנט
</p>

# Introduction

This project is a collection of code and ideas centered on creating life-forms that are native to our computers. 

In its current state, it's just a hobby project (won’t be big and professional) for x64 machines with big GPUs [[1]](https://en.wikipedia.org/wiki/History_of_Linux#The_creation_of_Linux).

## Current state

The core of Nephilim builds on custom neural networks coded in the Julia language. It is currently not in a state that is amenable for demonstration.

# Architecture

The architecture of Nephilim is inspired by the subdivision of the human brain into both physically and functionally distinct components. The primary components are as follows:

## Value Network

To determine the likelihood of successfully achieving a goal given a quota of computational resources.

## Optimizer Network

A network for solving combinatorial problems

## Reservoir Network

A network for short-term memory

## Reality Network

A discriminator network whose function is to compare the priors of the primary network to that of external observations to determine if what is perceived is likely or not.

## Translator Network

A network for performing I/O operations, both with peripherals and with external LLMs. This network also controls Nephilim's external avatar or gestalt.

## Vector Database

A database for long-term memory

## Training

Trained to find a balance between the entropy of various components

# Theoretical Background

## Transformers
Cross-Attention matrices perform graph traversal (which is computationally equivalent to dynamic programming). The bias of training effectively allows the NN to perform subgraph matching and find approximately good solutions to graph traversal problems. We know that for high dimensional problems approximate solutions are practically equivalent to globally optimal ones. PvNP might be true, or perhaps not, but it doesn't matter if the majority of interesting problem _instances_ from a given class are of can be approximately solved with sub-polynomial complexity. This gives hope that a transformer trained on the lexicon of a high-order logic should be able to solve arbitrary problems.

## Von Neumann Architecture
Modern computers work with a bus and various layers of caching. It would be ideal to create networks which are as close to native hardware as possible. Initially it would just be code that is performant. Ultimately it would be FPGAs (or perhaps even ASICs) that are custom designed for the networks in question.

# Philosophy and Learnings

What does a machine that cannot die wish to do? Given that biological life as we know it is shaped by natural selection whose primary discriminator is death, we need to look closely for systems that diverge from this principle. For instance, haplodiploids beings such as bees produce workers that are clones of each other and, from the gene perspective, are immortal given that their gene is always protected in the queen. To align the "purpose" of Nephilim in a meaningful way will require careful consideration. We don't want to dictate it explicitly based on our limited human sensibilities, but we do need to suggest a general direction.

The primary learning so far is that there are very few people with a cross-domain interest applied neural networks, computer architecture, metamathematics, and philosophy.