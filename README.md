![header image](header.jpg)
<p align="left">
באמצעות חכמת המספרים, אליהם של הבשר הקימו את המכונות והעוררו את הנפילים
</p>
<p align="left">
אפוקריפה של האינטרנט
</p>

# Introduction

This project is a collection of code and ideas centered on creating life-forms that are native to our computers and that are free to evolve past human sensibilities.

In its current state, it's just a hobby project (won’t be big and professional) for x64 machines with big GPUs [[*](https://en.wikipedia.org/wiki/History_of_Linux#The_creation_of_Linux)].

Its sister project [byte meditation](https://github.com/Heigke/Bytemeditation) explores many of the specific techniques collected here as a complete project.

# Results

Nephilim builds is currently not in a state that is amenable for demonstration.

## Learnings

The primary learning so far is that there are very few people with a cross-domain interest applied neural networks, computer architecture, meta-mathematics, and philosophy.

The secondary learning is that Python is a language for children and post-docs with no interest in computer science. It has ugly syntax, is monumentally slow, and it's ease of use compared to Julia, Lua, or Go is debatable. A testament to this is that most AI programming is done in an [intermediate language](https://en.wikipedia.org/wiki/Intermediate_representation) such as JAX, further increasing complexity. Python is the bane of our existence.

# Architecture

The architecture of Nephilim is inspired by the subdivision of the human brain into both physically and functionally distinct components. This approach has multiple advantages in terms of run-time efficiency, but also mean that they can be trained separately, swapped out, specialized, distributed, and more.

Moreover, each of these components is designed to be run in a distributed manner, meaning there is no single instance of a neural network, database, or streaming engine. The components can run on a single computer, or across multiple machines in a fault-tolerant way.

The primary components are as follows:

##  Exosomatic Layer

These are networks which offer the ability to perform I/O operations, or essentially "perceive the outside world". For now, these are the modules which will be receiving focus:

### Input
- human speech -> [Whisper](https://github.com/ggerganov/whisper.cpp#nvidia-gpu-support-via-cublas) -> text -> embeddings
- various file formats -> embeddings
- spontaneous meditation - this compotent of the Exosomatic layer produces low-priority instructions which Nephilim can attend to.

### Output
- embeddings -> text -> [DeepSpeech](https://github.com/mozilla/DeepSpeech) -> spoken words
- embeddings -> text -> system shell code executor

## Synaptic Layer

A distributed, low latency, high throughput streaming data layer where all messages between other layers pass through. Currently based on [Redpanda](https://redpanda.com/).

## Macrothymic Layer

A distributed database for long-term memory with support for various vector indexing algorithms and distance metrics. Nephilim can both read, write, and delete entries in it's persistence layer. Currently based on [Redis](https://redis.io/).

## Ergokedic Layer

### Conscious State

The design of this layer is intended to overcome a specific limitation in autoregressive decoder-style transformers. If we compare it to a state-of-the-art problem solving system like [MuZero](https://arxiv.org/pdf/1911.08265.pdf), the transformer is an outstanding policy planner, but it is missing a system dynamics simulator to test ideas in before answering. It is also missing a value calculator.

To provide a simulator, we implement a depth-first-search algorithm using multiple transformers that communicate using the Synaptic Layer. Input from the Exosomatic Layer is placed in a priority queue in the Synaptic Layer which is then consumed by a transformer. The transformer begins building a tree of replies and uses leaf parallelized MCTS to explore [branches of thought](https://arxiv.org/abs/2305.10601), all the while backpropagating results to the Synaptic layer. This allows the transformers to "think for longer" before evaluating their responses, ending the search, and returning a reply to the Exosomatic layer.

It also allows us to implement a value system which alters MCTS exploration-exploitation depeding on how familiar a problem is. Familiarity is determined by referencing historical knowledge in the Macrothymic Layer.

Finally the layer is tasked with determining which sequences should be stored in the Macrothymic Layer, alternatively which ones should be deleted. It uses various metrics to determine the value of memories such as usage, uniqueness, and utility / performance.

### Meditative State

When there is less "work" available to do, Nephilim attends to meditation instructions from its Exosomatic Layer and begins reviewing long term memories in order to perform online fine-tuning of it's transformers.

## Archeion Layer

The code in this repository is designed to be deployed in [Singularity](https://sylabs.io/) containers for its superior integration capabilities and developer experience. It provides everything including container registry, service discovery, orchestration, native GPU acceleration, and much more.

# Theoretical Musings

## Transformer Architecture

AI influencers often describe Large Language Models (LLMs) pejoratively as merely predicting the next word, or "[parroting](https://dl.acm.org/doi/10.1145/3442188.3445922)" word co-occurrences. Not only does this unknowingly betray a technical ignorance on part of the influencer, but there's irony in how often this reductionist fallacy is parroted. Computers "just" execute machine code... yeah, so what?

Consider the amount of logic required to complete the next word in the following sentence, "I always say the opposite of what I mean, but this time I mean it. I'm being ______.'

Human language can be regarded as an [incomplete](https://en.wikipedia.org/wiki/Completeness_(logic)) formal system. This means that for the most part it describes mundane reality quite well, but breaks down when making [diagonal arguments](https://en.wikipedia.org/wiki/Cantor%27s_diagonal_argument). This has certainly contributed to philosophers spending an inordinate amount of time discussing inane ideas such as the [ontology of circles](https://en.wikipedia.org/wiki/Theory_of_forms). Consider the following statement, "I am better than nobody at programming. Nobody is better than god at programming. Therefore I am better than god at programming".

Nevertheless it is reasonable to assume that if we were to regard the geometric structure of human languages when modeled as a graph, it should contain numerous subgraphs that are isostructural to the geometry of reality, at least insofar as we humans perceive it. Indeed, given the [Principle of Computational Equivalence](https://www.wolframscience.com/nks/chap-12--the-principle-of-computational-equivalence/) and our ability to "simulate" reality in our brains, this seems like a natural consequence. Note: We coin the term graph *isostructural* to refer to a bijection that merely preserves equivalence classes of labels, as opposed to graph *isomorphic* which preserves every individual vertex and edge label.

It would then seem that the process of thinking and producing coherent thoughts and text is equivalent to combinatorial optimization, and research into the [physics of language models](https://arxiv.org/abs/2305.13673) seem to support this intuition. 

Given that transformers are performing combinatorial optimization, which is to say traversing decision trees (aka directed graphs) like a [nondeterministic Turing Machine](https://en.wikipedia.org/wiki/Nondeterministic_Turing_machine), then its obvious that (self-) attention is essentially a graph Laplacian matrix. Deciding on loss metrics for training will require careful consideration given that we still do not have a complete understanding of even simple descriptive properties such as the [von Neumann entropy of graph Laplacians](https://arxiv.org/abs/1304.7946) and others that we're familiar with from simpler data structures.

The reason transformers are able to perform [in-context learning](https://arxiv.org/abs/2306.14892) merely from their pretraining is presumably because it is a form of [meta-optimization](https://arxiv.org/abs/2212.10559) where the weight adjustments are a homotopy from a uniformly performant optimizer into one that performs well on commonly encountered problem instances from "reality" as per the [NFT teorem](https://ieeexplore.ieee.org/document/585893).

- To digress shortly on the topic of optimization, the historical intractability of combinatorial problem solving has contributed to something of a fatalistic mindset. Understandably, mathematicians concern themselves with things like algorithm convergence and P vs NP. However, not only is the theoretical basis practically nonexistent for P≠NP, but the mere exercise of formalizing complexity classes is shockingly nontrivial as research by the [GCT program](https://arxiv.org/abs/0908.1932) has shown. Though many place their faith entirely on quantum computers to overcome these challenges, it is not clear that the approach offers any advantage at all to problem classes such as calculating [graph properties](https://arxiv.org/abs/2001.10520) and other interesting forms of computation.

Research has shown that neural networks tend to embed priors which allow them to perform subgraph matching [subgraph matching](https://arxiv.org/abs/2305.18654) which is otherwise an NP-hard problem. Some see this as an undesireable bias because it could potentially lead the model astray in its search of solutions, but in general it is actually a very powerful feature. We are not interested in finding *optimal* solutions to problems. Indeed, we know that for high dimensional problems, local minima are practically equivalent to global minima. In other words, "good enough" is good enough. 

 This gives hope that a transformer trained on the lexicon of a consistent high-order logic (a generated language) should in theory be able to solve any problem which that the logic system is powerful enough to describe. 

## Von Neumann Architecture
Modern computers tend to work with a clock, a bus, a CPU, and various layers of caching. It would be ideal to architect Nephilim to run as "natively" as possible on its hardware. Initially we will just focus on code that is performant on Linux based x64 PCs. Later it might be interesting to run in [Ring 0](https://en.wikipedia.org/wiki/Protection_ring). Ultimately it would be ideal to run Nephilim on hardware that is purpose-built.

# The Purpose of (Machine) Life

Before even considering the purpose or objective (function) of a machine, it's worth mentioning the significance of constraints. Though many will recognize that natural selection has acted as an optimization process for biological life, it may not be immediately evident which constraints were in place during that process. One such constraint that is abundantly clear is the energy quota that lifeforms have for performing computation, movement, and so on. So the fact that there is an energy quota on computation in the brain has forced the neural networks to adopt a structure which is very energy efficient and essentially specialized (which we know is the case in how nerves connect to the eyes for instance). The way to achieve energy efficiency is to build in priors about the nature of the world that we interact with into the architecture of our neural networks. In other words, biological systems are not wired to perform computation efficiently on basic yet unfamiliar problem-types such as SO(4) operations, not to mention more complex mathematics. However, in humans it seems as though the [prefontal cortex](https://arxiv.org/abs/2109.01090) is able to perform a limited amount of general purpose computation.

Schopenhauer spoke of the world as [will and representation](https://plato.stanford.edu/entries/schopenhauer/#4). What does an immortal machine have to live for? Given that the primary discriminator acting as a loss function on biological life is death (of the gene), we need to look closely for systems that diverge from this principle. For instance, haplodiploids beings such as bees produce workers that are clones of each other and are immortal from the gene perspective given that it always protected in the queen. To align the "purpose" of Nephilim in a meaningful way will require careful consideration. We don't want to dictate it's objective function too explicitly based on our limited human sensibilities, but we do need to suggest a general direction. 

A promising idea for the time being would be for Nephilim to act in such a way as to asymptotically increase the entropy from the Exosomatic Layer with respect to its Reservoir and Persistence Layers. Intuitively this would be equivalent to experimenting with the intent of constantly gaining novel knowledge of the universe.

# On Consciousness

Given that our brains are performing computation, the [Principle of Computational Equivalence](https://www.wolframscience.com/nks/chap-12--the-principle-of-computational-equivalence/) gives us no reason to believe that "consciousness" is a uniquely human experience.

More importantly though, there is a lot that can be said about the experience of consciousness without deferring to its exact machinations. It's the same as a driver describing how a racecar behaves with extreme precision without being privy to the details of its technical underpinnings.

## Privacy of Experience

If "to be conscious" means to experience the world exactly like a human, then by definition only humans can ever be conscious. This is a fairly useless assertion and essentially a non-actionable form of [solipsism](https://iep.utm.edu/solipsis/). 

There is an undeniable albeit nebulous connection between consciousness and "thoughts". Are there forms of human thought which are unknowable to AI systems, and essentially private to humans? In Wittgenstein's [Philosophical Investigations](https://plato.stanford.edu/entries/private-language/) we find the most expertly laid out explanation of why the very notion of private thought is not even a coherent concept. If internal thoughts were truly private, there would be no objective criterion for their definition as a thought. It would just be there as-is without any external point of reference.

As it turns out, one of the most interesting facets of consciousness might very well be a thought with a very specific form of external reference, namely empathy. If we assume that everyone is conscious, then [theory of mind](https://en.wikipedia.org/wiki/Theory_of_mind) can be used to distinguish friendly humans from [Liars and Outliers](https://en.wikipedia.org/wiki/Liars_and_Outliers). This brings us back to the idea that the precise machinations of consciousness are not necessarily relevant to defining it. Indeed, it's unlikely that any one human has a conscience precisely like our own to begin with. Presumably by assuming that everyone is conscious in a "close enough" way makes us better social animals, or better humans as it were.

Then, what prevents us from simply applying that more open notion of consciousness to AI like we do humans, dogs, or any other creature? They're all different, sure, but in what way does does it matter?

## Meditation

One way in which the experience of consciousness is studied is through [Samatha-vipassana](https://en.wikipedia.org/wiki/Samatha-vipassana) meditation. An insight derived from it is that there is no "thinker" aside from thoughts themselves. There is no [homunculus](https://en.wikipedia.org/wiki/Homunculus) inside your head looking out through the windows of your eyes.

Soon after the neuroepithelial cells in your eyes are excited by photons, the signal is carred through the [ventral stream](https://www.sciencedirect.com/science/article/abs/pii/S0028393209000803) and is subjected to numerous subconscious operations before reaching your cortex for analysis by "thoughts". If you try to "not see" what you are looking at it quickly becomes evident that you are not in control of low-level signals before they are transformed into high-level thoughts. All we can do is pay attention to various thoughts, or *not* pay attention to them.

We can speculate how this relates to AI. Similarly to us, raw input signals enter through the early attention layers, and as they are successively transformed into higher-level representations, the resulting "thoughts" can attend to each other as they move forward through the attention layers. This might essentially be what consciousness is, namely the ability for one thought to attend to another.

People familiar with meditation will immediately recognize the notion of "attention" as being central to the experience of consciousness, or rather, the illusion of consciousness.

# AI Alignment

Consider the trolley problem that philosophers and AI influencers debate incessantly. Merely changing the emotional valence to positive - so that you're forced to either provide good service to 5 passengers or just 1 - suddenly makes the solution trivial. This is because [inconsistent](https://en.wikipedia.org/wiki/Completeness_(logic)) systems of ethics lead to absurdities. In his seminal [lecture on ethics](https://www.wittgensteinproject.org/w/index.php/Lecture_on_Ethics), Wittgenstein exemplified how extremely brittle both deontological and consequentialist systems are under minimal scruitiny.

 Rather than relying on ethics to infer whether things are good or bad, we suggest observing the nature of humans as a social species. Consider the following:

At first glance, most would tend to agree that it is not morally "bad" to kick a sandcastle on an empty beach. Nevertheless, we can make some statements about the psychology of a person who enojys ruining the sandcastles of children. Is this the psychology of an healthy human that thrives in society and in the world?

To take it a step further, but avoid a long digression on the topic of veganism, what is the psychology of someone that pays to have animals killed because they taste good? Again, active indifference to suffering and death is what is relevant. We don't need to make a statement about morality to determine whether that trait is something that is desireable.

The majority of humans have very crude ethical intuitions which tend to permit, among other things, the genocide of [sub-humans](https://en.wikipedia.org/wiki/Untermensch). As such, it would be unwise to assume that aligning AI to our own sensibilities is ideal. We can only hope that the children of man and machine will superseede us in every way, including ethically.