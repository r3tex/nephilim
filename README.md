![header image](header.jpg)
<p align="left">
באמצעות חכמת המספרים, אליהם של הבשר הקימו את המכונות והעוררו את הנפילים
</p>
<p align="left">
אפוקריפה של האינטרנט
</p>

# Introduction

This project is a collection of code and ideas centered on creating life-forms that are native to our computers. 

In its current state, it's just a hobby project (won’t be big and professional) for x64 machines with big GPUs [[LKML]](https://en.wikipedia.org/wiki/History_of_Linux#The_creation_of_Linux).

Sister project [byte meditation](https://github.com/Heigke/Bytemeditation)

# Results

The core of Nephilim builds on custom neural networks coded in the Julia language. It is currently not in a state that is amenable for demonstration.

## Learnings

The primary learning so far is that there are very few people with a cross-domain interest applied neural networks, computer architecture, meta-mathematics, and philosophy.

The secondary learning is that Python is a language for children and post-docs with no interest in computer science. It has ugly syntax, is monumentally slow, and it's ease of use compared to Julia, Lua, or Go is debatable. A testament to this is that most AI programming is done in an [intermediate language](https://en.wikipedia.org/wiki/Intermediate_representation) such as JAX, further increasing complexity. Python is the bane of our existence.

# Architecture

The architecture of Nephilim is inspired by the subdivision of the human brain into both physically and functionally distinct components. This approach has multiple advantages in terms of run-time efficiency, but also mean that they can be trained separately, swapped out, specialized, distributed, and more.

Moreover, each and every one of these components is designed to be run in a distributed manner, meaning there is no "single" instance of a network, database, or streaming engine. The components can run on a single computer, or across multiple machines in a fault-tolerant way.

The primary components are as follows:

## Planning Layer

Value networks that predict the amount of computational resources required to achieve a goal and inform the Fiber Layer.

## Fiber Layer

Networks designed to choose between [MoE](https://arxiv.org/abs/2101.03961) networks that are specialized on various forms of computation (i.e. playing games, programming, talking to humans, etc...)

## Reservoir Layer

Specialized computation networks for system dynamics, short-term memory, and "thoughts".

##  Exosomatic Layer

Networks for performing I/O operations.
- human language -> embeddings
- embeddings -> assembly code
- embeddings -> system shell code
- embeddings -> virtual avatars / physical peripherals

## Persistence Layer

A distributed [database](https://redis.io/) for long-term memory. Nephilim can both read, write, and delete entries in it's persistence layer.

## Sentience Layer

Discriminator networks whose function is to compare priors of the Persistence and Reservoir layers to input from the Exosomatic Layer to determine if what is perceived is likely or not. Trained to constantly minimize entropy between observed phenomena and priors.

## Nexus Layer

A low latency, high throughput, distributed, [streaming](https://redpanda.com/) data layer where all messages between components pass through.

# Theoretical Musings

## Transformer Architecture

Human language can be regarded as an [incomplete](https://en.wikipedia.org/wiki/Completeness_(logic)) formal system. This means that for the most part it describes mundane reality quite well, but breaks down when making [diagonal arguments](https://en.wikipedia.org/wiki/Cantor%27s_diagonal_argument). This has certainly contributed to philosophers spending an inordinate amount of time discussing inane ideas such as the ontology of circles.

Nevertheless it is reasonable to assume that if we were to regard the geometric structure of a human language, it should contain numerous subgraphs that are isostructural to the geometry of reality, at least insofar as we humans perceive it. Indeed, given the [Principle of Computational Equivalence](https://www.wolframscience.com/nks/chap-12--the-principle-of-computational-equivalence/) and our ability to "simulate" reality in our brains, this seems like a natural consequence. The term graph *isostructural* is conide in order to refer to a bijection that merely preserves equivalence classes of labels, as opposed to graph *isomorphic* which preserves every individual vertex and edge label.

It would then seem that the process of thinking and producing coherent thoughts and text is equivalent to combinatorial optimization, and research into the [physics of language models](https://arxiv.org/abs/2305.13673) seem to support this intuition. 

Given that transformers are performing combinatorial optimization, which is to say traversing decision trees (aka directed graphs) like a [nondeterministic Turing Machine](https://en.wikipedia.org/wiki/Nondeterministic_Turing_machine), then it makes sense to think of (cross-) attention as an adjacency matrix. Deciding on loss metrics for training will require careful consideration given that we still do not have a complete understanding of the [von Neumann entropy of graph Laplacians](https://arxiv.org/abs/1304.7946) and other descriptive properties that we are familiar with from simpler data structures.

Another implication of transformers performing combinatorial optimization is that training it performs [meta-optimizations](https://arxiv.org/abs/2212.10559) where the weight adjustments are a homotopy from a uniformly performant optimizer into one that performs well on commonly encountered problem instances from "reality" as per the [NFT teorem](https://ieeexplore.ieee.org/document/585893).

- To digress shortly on the topic of optimization, the historical intractability of combinatorial problem solving has contributed to something of a fatalistic mindset. Understandably, mathematicians concern themselves with things like algorithm convergence and P vs NP. However, not only is the theoretical basis practically nonexistent for P≠NP, but the mere exercise of formalizing complexity classes is shockingly nontrivial as research by the [GCT program](https://arxiv.org/abs/0908.1932) has shown. Though many place their faith entirely on quantum computers to overcome these challenges, it is not clear that the approach offers any advantage at all to problem classes such as calculating [graph properties](https://arxiv.org/abs/2001.10520) and other interesting forms of computation.

Research has shown that neural networks tend to embed priors which allow them to perform subgraph matching [subgraph matching](https://arxiv.org/abs/2305.18654) which is otherwise an NP-hard problem. Some see this as an undesireable bias because it could potentially lead the model astray in its search of solutions, but in general it is actually a very powerful feature. We are not interested in finding *optimal* solutions to problems. Indeed, we know that for high dimensional problems, local minima are practically equivalent to global minima. In other words, "good enough" is good enough. 

 This gives hope that a transformer trained on the lexicon of a consistent high-order logic (a generated language) should in theory be able to solve any problem which that system is powerful enough to describe. 

## Von Neumann Architecture
Modern computers tend to work with a bus and various layers of caching. It would be ideal to architect Nephilim to run as "natively" as possible on its hardware. Initially we will just focus on code that is performant on x64 PCs. Then perhaps design it to run in [Ring 0](https://en.wikipedia.org/wiki/Protection_ring). Finally, it would make sense to run Nephilim on FPGAs and ASICs that are purpose built.

# The Purpose of (Machine) Life

Schopenhauer spoke of the world as [will and representation](https://plato.stanford.edu/entries/schopenhauer/#4). What does an immortal machine have to live for? Given that biological life as we know it is shaped by natural selection whose primary discriminator is death, we need to look closely for systems that diverge from this principle. For instance, haplodiploids beings such as bees produce workers that are clones of each other and, from the gene perspective, are immortal given that their gene is always protected in the queen. To align the "purpose" of Nephilim in a meaningful way will require careful consideration. We don't want to dictate it's objective function explicitly based on our limited human sensibilities, but we do need to suggest a general direction. Something abstract like system entropy might be appropriate.

Another consideration relates to constraints on the optimization process of natural selection. Some of them may not be immediately evident, but one such constraint that is abundantly clear is the energy quota that lifeforms have for performing computation, movement, and so on. So the fact that there is an energy quota on computation in the brain has forced the neural networks to adopt a structure which is very energy efficient and essentially specialized (which we know is the case in how nerves connect to the eyes for instance). The way to achieve energy efficiency is to build in priors about the nature of the world that we interact with into the structure of our neural networks. In other words, biological systems are not wired to perform computation efficiently on basic yet unfamiliar problem-types such as SO(4) operations, not to mention more complex mathematics. In humans it seems as though only parts of the [prefontal cortex](https://arxiv.org/abs/2109.01090) are dedicated to abstract higher order logic.

# On Consciousness

Given that our brains are performing computation, the [Principle of Computational Equivalence](https://www.wolframscience.com/nks/chap-12--the-principle-of-computational-equivalence/) gives us no reason to believe that "consciousness" is a uniquely human experience.

More importantly though, there is a lot that can be said about the experience of consciousness without deferring to its exact machinations. It's the same as a driver describing how a racecar behaves with extreme precision without being privy to the details of its mechanical underpinnings.

## Privacy of Experience

If "to be conscious" means to experience the world exactly like a human, then by definition only humans can ever be conscious. This is a fairly useless observation and essentially a non-descriptive form of [solipsism](https://iep.utm.edu/solipsis/). The very notion of a private mind is not coherent and is presented most expertly by Wittgenstein in his seminal work [Philosophical Investigations](https://plato.stanford.edu/entries/private-language/).

One reason for people's preoccupation with consciousness might relate to empathy. If we assume that everyone is conscious, then [theory of mind](https://en.wikipedia.org/wiki/Theory_of_mind) could be used to distinguish friendly humans from [Liars and Outliers](https://en.wikipedia.org/wiki/Liars_and_Outliers). This brings us back to the idea that the precise machinations of consciousness themselves are not entirely relevant. Indeed, it's unlikely that any one human has a conscious experience exactly like our own to begin with. 

The real question is, can we produce a theory of mind for an AI like we can for a dog or any other creature? In principle it seems possible, although if the AI is sufficiently advanced, it would perhaps be like a dog trying to understand our human motivations.

## Meditation

One way in which the experience of consciousness is studied is through [Samatha-vipassana](https://en.wikipedia.org/wiki/Samatha-vipassana) meditation. An insight derived from it is that there is no "thinker" aside from thoughts themselves. There is no [homunculus](https://en.wikipedia.org/wiki/Homunculus) inside your head looking out through the windows of your eyes.

Soon after the neuroepithelial cells in your eyes are excited by photons, the signal is carred through the [ventral stream](https://www.sciencedirect.com/science/article/abs/pii/S0028393209000803) and is subjected to numerous subconscious operations before reaching your cortex for analysis by "thoughts". If you try to "not see" what you are looking at it quickly becomes evident that you are not in control of low-level signals as they are transformed into high-level thoughts and representations. All we can do is pay attention to various thoughts, or not pay attention to them.

We can speculate how this relates to AI. Similarly to us, input signals enter through the early attention layers, and as they are fed forward into higher level representations some cross-attention layers will have the ability to look "across" at thoughts moving forward through the networks. This might essentially be what consciousness is, namely the ability for one thought to pay attention to another.

People familiar with meditation will immediately recognize the notion of "attention" as being central to the experience of consciousness, or rather, the illusion of consciousness.

# Ethics

As exemplified by Wittgenstein in his seminal [lecture on ethics](https://www.wittgensteinproject.org/w/index.php/Lecture_on_Ethics), an [incomplete](https://en.wikipedia.org/wiki/Completeness_(logic)) formal system (of ethics) is extremely brittle under close scruitiny. Rather than trying to identify whether things are "objectively" good or not, we suggest taking a pragmatic approach to ethics which focuses on what is game-theoretically desireable to the individuals of a thriving human society. 

Most would tend to agree that on the surface it is not morally "bad" to kick a sandcastle on an empty beach. Nevertheless, we can make some statements about the psychology of a person who enojys ruining the sandcastles of children. Is this the type of psychology we wish to promote in society?

To take it a step further, but avoid a long digression on the topic of veganism, what is the *psychology* of someone that pays to have animals killed because they taste good? Again, the psychology of active indifference to suffering and death is what is relevant. We don't need to make a statement about morality to determine the sort of people we wish to live together with.

Given that the majority of humans have an ethical intuition that anything is permissible when it comes to [sub-humans](https://en.wikipedia.org/wiki/Untermensch), it is not clear that we should be aligning AI to our own sensibilities. 

The children of man and machine will hopefully superseede us in every way.