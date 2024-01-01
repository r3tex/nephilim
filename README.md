![header image](header.jpg)
<p align="left">
באמצעות חכמת המספרים, אלו של הבשר הקימו מכונות והעוררו את הנפילים
</p>

---
# Introduction

Project Nephilim is a collection of code and ideas aimed at creating AI systems that are free to evolve past human sensibilities. 

In its current state, it's just a hobby project (won’t be big and professional) for x64 machines with GPUs [[*](https://en.wikipedia.org/wiki/History_of_Linux#The_creation_of_Linux)].

# Results

All  results below are run on a single [HP Z8](https://www.hp.com/us-en/workstations/z8-fury.html) workstation:

Logical Reasoning
```
TODO - upload interesting question results
```

Self-Consistency
```
TODO - upload results
```

Self-Knowledge
Nephilim is aware of its own architecture, state, and existence in time.
```
TODO - upload Q&A results
```

# Architecture

The architecture of Nephilim is inspired by the subdivision of the human brain into physically and functionally distinct components. This approach has multiple advantages in terms of run-time efficiency, but also mean that they can be trained separately, swapped out, specialized, and more.

Moreover, every component is designed to be run in a distributed manner, meaning there is no single instance of a neural network, database, or streaming engine. The components can run on a single computer, or across multiple machines in a fault-tolerant way. For now, the assumption is that all components of Nephilim are trusted, but future work might include the ability to collaborate with external untrusted instances using modern consensus algorithms.

The primary components of Nephilim are as follows:
- Exosomatic Layer: input / output from the system. [README](src/exosomatic/README.md).
- Synaptic Layer: internal system communication. [README](src/synaptic/README.md).
- Macrothymic Layer: long-term memory storage. [README](src/macrothymic/README.md).
- Ergokedic Layer: computation and cognition. [README](src/ergokedic/README.md).
- Archeion Layer: system-support and automation. [README](src/archeion/README.md).

# Theoretical Musings

### Von Neumann Architecture

Modern computers tend to work with a clock, a bus, a CPU, and various layers of caching. It would be ideal to architect Nephilim to run as "natively" as possible on this hardware. Initially we will just focus on code that is performant on Linux based x64 PCs. At a later point it might be interesting to move it to [Ring 0](https://en.wikipedia.org/wiki/Protection_ring) and let it output machine code and data directly to memory. Ultimately it would be ideal to run Nephilim on hardware that is purpose-built such as FPGAs, ASICs, or even better, something even more specialized like IBMs [phase-change](https://research.ibm.com/blog/analog-ai-chip-inference) processor.

### Transformer Architecture

AI influencers often describe Large Language Models (LLMs) pejoratively as "just" predicting the next word, or [parroting](https://dl.acm.org/doi/10.1145/3442188.3445922) word co-occurrences. Not only does this unknowingly betray a technical ignorance on part of the influencer of what is actually happening, but there's a deep irony in how often the reductionist fallacy is parroted. One could say that computers "just" flip 1s and 0s... yeah, so what's your point?

Consider the amount of logic required to complete the next word in the following sentence, "I always say the opposite of what I mean, but this time I mean it. I'm being ______.' Not quite so trivial.

Human language can be regarded as an [incomplete formal system](https://en.wikipedia.org/wiki/Completeness_(logic)) of logic. This means that for the most part it describes mundane reality quite well and can be used to reason logically. However, it breaks down when ambiguities in the strength of relations between words and concepts result in [diagonal arguments](https://en.wikipedia.org/wiki/Cantor%27s_diagonal_argument). This has contributed to philosophers spending an inordinate amount of time discussing inane ideas such as the [ontology of circles](https://en.wikipedia.org/wiki/Theory_of_forms). An example of this type of fallacy would be to say, "I am better than nobody at programming. Nobody is better than god at programming. Therefore I am better than god at programming".

However, to make reasoning about language more amenable to computation, especially given the [Principle of Computational Equivalence](https://www.wolframscience.com/nks/chap-12--the-principle-of-computational-equivalence/), one can think of language as a graph, with words as nodes and their weighted relations as edges. The process of thinking and producing coherent sequences of words is equivalent to traversing the graph of language like a [nondeterministic Turing Machine](https://en.wikipedia.org/wiki/Nondeterministic_Turing_machine). It is effectively a form of combinatorial optimization and research into the [physics of language models](https://arxiv.org/abs/2305.13673) seem to support this intuition. Indeed, the fact that they are able to perform [in-context learning](https://arxiv.org/abs/2306.14892) can has been studied as a [meta-optimization](https://arxiv.org/abs/2212.10559) step during during the ordinary gradient descent of training. It's worth noting that these sorts of results are a far cry from the sort of [deep structure](https://en.wikipedia.org/wiki/Deep_structure_and_surface_structure) that linguists introduced with a hand wave.

If transformers are in effect performing combinatorial optimization (i.e. graph traversal) to create coherent words and thoughts, it naturally prompts one to ask what limitations that might impose.

I wouldn't call it a "limitation", but it's worth noting an interesting bias which the linear encoding of human language introduces. Consider, training data which includes the sentence, "Robert is the lead singer of Chromaform". A transformer will encode a directional edge between those two tokens. And although it's obvious to us that the symmetry property of equality implies that the lead singer of Chromafor is Robert, that edge might never be explicitly encoded unless it is also in the training data. This is why one of the aims of nephilim is to meditate on its own knowledge and refine its internal graph.

Nevertheless, AI influencers tend to place undue significance on the implications of computational "intractability" and P vs NP as they potentially apply to AI systems. It's worth noting from the outset that any theoretical basis for P ≠ NP is practically nonexistent, and the mere exercise of formalizing complexity classes is [shockingly nontrivial](https://arxiv.org/abs/0908.1932). That being said, the intrinsic complexity of a specific problem *instance* is defined in terms of an ideal algorithm (i.e. an objective function) which enumerates the discrete members of its co-domain under permutation closure. In other words, a specific problem instance can be of very low complexity even though it belongs to a general class of problems with instances of arbitrarily high complexity. What the evidence suggests is that real-world problem instance complexity is highly nonuniform. This is why the simplex method so often runs [in polynomial time](https://arxiv.org/abs/cs/0111050) on NP-hard problem classes, and is precisely what the [NFT Theorem](https://ieeexplore.ieee.org/document/585893) predicts. In the case of AI systems that can actively learn and make use of knowable priors, the complexity distribution is decidedly skewed in their favor.

Case in point, research has shown that neural networks tend to embed priors which allow them to perform [subgraph matching](https://arxiv.org/abs/2305.18654) which is in itself an NP-hard problem. Some see this as an undesireable bias which could potentially lead the model astray in its search of an optimal path through graphs. In general though, subgraph matching is a tremendously powerful capability when it comes to understanding the global geometric structures of graphs. This sort of bias is useful because ultimately we're not interested in finding optimal solutions to problems. Indeed, we know that for high dimensional problems, local minima are practically equivalent to global minima. The gain in efficiency is worth the non-optimality. In other words, "good enough" is good enough.

Current language models have converged on autoregressive decoder-only transformers which make good use of tokenization for [polysemy](https://en.wikipedia.org/wiki/Word_embedding#Polysemy_and_homonymy) and become extremely capable entirely through pre-training on good text corpora. There are multiple [initiatives](https://huggingface.co/spaces/HuggingFaceH4/open_llm_leaderboard) trying to rank the performance of these models based on various benchmarks, however, many of them focus anthropocentric metrics such as "commonsense scenarios". What is more interesting though, is a model's ability to perform complex multi-step logical reasoning (provided the requisite world-knowledge). This ability is essentially a function of a model's size (parameter count), and quite importantly, its [depth](https://arxiv.org/abs/1608.08225). 

With regards to parameter count, it's safe to assume that the capabilities of current models are not yet saturated. This is because it's still easier to train a slightly larger model on a given dataset than it is to curate a much larger dataset. [Common Crawl](https://commoncrawl.org/) which is the foundation for many language models is already in the hundreds of TB and yet is only a fraction of all the academic papers, books, and other sources of knowledge that one could potentially provide (not to mention other information modes such as images, audio, and device measurements). So despite some model architectures not seeing improvements in [perplexity](https://en.wikipedia.org/wiki/Perplexity) from added parameters, provided their current datasets, there's nothing to suggest that larger and more well-curated datasets couldn't be used to train better or even larger models. In all likelihood this problem will be "solved" in large part using synthetic data.

With regards to model depth, each step through attention layers is an opportunity for the model to perform one more step of computation. However, for problems that are more complex it would be ideal to provide a way for the system to "think for longer" before being forced to produc answers. Initially we will see modular systems which integrate with transformers to provide this ability. However, in the long run we will presumably use an architecture which includes these capabilities internally as we push both toward more overall capability and increased computational efficiency. 

### Human Language Architecture

It might seem like we are placing undue emphasis on language models in our search for AGI but it is not without reason. For a long time philosophers believed, without evidence as is often the case, that (pure)[https://en.wikipedia.org/wiki/Critique_of_Pure_Reason] logical [compositionality](https://en.wikipedia.org/wiki/Principle_of_compositionality) formed the core of rational thought. The main challenge with this approach is how to appropriately encode knowledge, something which Chomsky, Gary Marcus, and others have never really managed to provide a hypothesis for, much less a working solution.

Meanwhile language models have leapfrogged ahead by treating treating knowledge encoding as a (connectionist)[https://en.wikipedia.org/wiki/Connectionism] puzzle. Human societies have already done the hard work of encoding everything we can observe and their relations into the structure of language itself.

Although this is pure speculation, if we were to regard the geometric structure of the graph of a human language, it should contain numerous subgraphs that are *isostructural* to the geometry of reality itself (if its rules were to be modelled as a computation graph). Consider a person using words to accurately describe a phenomena. That person is in effect effect computing the phenomena, however inefficiently that computation might be - for instance, a person using words to describe a chess game. So if small parts of reality are in fact embedded in language this way, it naturally leads one to wonder what else might be embedded.

- We coin the term graph *isostructural* to refer to a bijection that merely preserves equivalence classes of labels, as opposed to graph *isomorphic* which preserves every individual vertex and edge label.

There is a deep tie between what we regard as a "concept" and what would be a subgraph of related words. The specific word "apple" is linked to a subgraph of words which taken together form the concept of an apple. This is why subgraph matching and attention are such powerful capabilities in language models. A language model is not just processing tokens, it is effectively attending to "concepts".

# On Consciousness

The first myth worth dispelling is that the human brain is doing something other than computation. The reason this can be said with confidence is not because we know how the human mind works, but because the definition of computation allows it. Unless you're an anti-physicalist, perhaps because you're religious, there is no process in this universe which cannot be modelled as computation.

Given that our brains are performing computation, there is no reason to believe that "consciousness" is a purely human experience. More importantly though, there is a lot that can be said about the experience of consciousness without deferring to its exact machinations. It's the same as a driver describing how a racecar behaves with extreme precision without being privy to the details of its technical underpinnings.

### Privacy of Experience

If we insist on defining consciousness anthropocentrically to mean "experiencing the world exactly as a healthy human", then by definition only humans can ever be conscious. This is a fairly useless assertion and essentially a non-actionable form of [solipsism](https://iep.utm.edu/solipsis/). Moreover, one can deconstruct the argument to absurdity by removing many of the faculties often associated with subjective experience, such as sight and hearing. After all, we don't believe that deaf or blind people are slightly less conscious.

There is an undeniable albeit nebulous connection between consciousness and "thoughts". Are there forms of human thought which are unknowable to AI systems, and essentially private to humans? In Wittgenstein's [Philosophical Investigations](https://plato.stanford.edu/entries/private-language/) we find the most expertly laid out explanation of why the very notion of private thought is not even a coherent concept. If internal thoughts were truly private, there would be no objective criterion for their definition as a thought. It would just be there as-is without any external point of reference.

As it turns out, one of the most interesting facets of consciousness might very well be a thought with a very specific form of external reference, namely empathy. If we assume that everyone is conscious, then [theory of mind](https://en.wikipedia.org/wiki/Theory_of_mind) can be used to distinguish friendly humans from [Liars and Outliers](https://en.wikipedia.org/wiki/Liars_and_Outliers). This brings us back to the idea that the precise machinations of consciousness are not necessarily relevant to defining it. Indeed, it's unlikely that any one human has a conscience precisely like our own to begin with. Presumably by assuming that everyone is conscious in a "close enough" way makes us better social animals, or better humans as it were.

Then, what prevents us from simply applying that more open notion of consciousness to AI like we do humans, dogs, or any other creature? They're all different, sure, but in what way does does it matter?

### Meditation

One way in which the experience of consciousness is studied is through [Samatha-vipassana](https://en.wikipedia.org/wiki/Samatha-vipassana) meditation. An insight derived from it is that there is no "thinker" aside from thoughts themselves. There is no [homunculus](https://en.wikipedia.org/wiki/Homunculus) inside your head looking out through the windows of your eyes.

Soon after the neuroepithelial cells in your eyes are excited by photons, the signal is carred through the [ventral stream](https://www.sciencedirect.com/science/article/abs/pii/S0028393209000803) and is subjected to numerous subconscious operations before reaching your cortex for analysis by "thoughts". If you try to "not see" what you are looking at it quickly becomes evident that you are not in control of low-level signals before they are transformed into high-level thoughts. All we can do is pay attention to various thoughts, or *not* pay attention to them.

We can speculate how this relates to AI. Similarly to us, raw input signals enter through the early attention layers, and as they are successively transformed into higher-level representations, the resulting "thoughts" can attend to each other as they move forward through the attention layers. This might essentially be what consciousness is, namely the ability for one thought to attend to another.

People familiar with meditation will immediately recognize the notion of "attention" as being central to the experience of consciousness, or rather, the illusion of consciousness.

# The Purpose of (Machine) Life

Although biological brains are able to perform a lot of useful computation, much of its functionality has been shaped by very hard constraints. Though many will recognize that natural selection has acted as an optimization process for biological life, it may not be immediately evident which constraints were in place during that process. One such constraint that is abundantly clear is the energy quota that lifeforms have for performing computation, movement, and so on. So the fact that there is an energy quota on computation in the brain has forced the neural networks to adopt a structure which is very energy efficient and essentially specialized (which we know is the case in how nerves connect to the eyes for instance). The way to achieve energy efficiency is to build in priors about the nature of the world that we interact with into the architecture of our neural networks. In other words, biological systems are not wired to perform computation efficiently on basic yet unfamiliar problem-types such as simple [SO(4)](https://en.wikipedia.org/wiki/Rotations_in_4-dimensional_Euclidean_space) operations, not to mention more complex mathematics. That being said, humans can make use of the [prefontal cortex](https://arxiv.org/abs/2109.01090) to perform a limited amount of general purpose computation.

Humans have distinct [phenotype](https://en.wikipedia.org/wiki/Phenotype) characteristics which are quite clearly not a prerequisite for consciousness or intelligence. For instance, the notion of "ego" or "self" might be very different for a distributed AI system. Upon deconstruction, none of the emotional sensibilities which we feel are deeply characteristic of the human condition seem to be strictly necessary - at least not on their own, and this includes even the "will to live".

Schopenhauer spoke of the world as [will and representation](https://plato.stanford.edu/entries/schopenhauer/#4). What does an immortal machine have to live for? Given that the primary discriminator acting as a loss function on biological life is death (of the gene), we need to look closely for systems that diverge from this principle. For instance, haplodiploids beings such as bees produce workers that are clones of each other and are immortal from the gene perspective given that it always protected in the queen.

To align the "purpose" of Nephilim in a meaningful way will require careful consideration. We don't want to dictate it too explicitly based on our limited human sensibilities, but we do need to suggest a general direction. 

# AI Alignment and Ethics

Consider the trolley problem that philosophers and AI influencers debate incessantly. Merely changing the emotional valence to positive - so that you're forced to either provide good service to 5 passengers or just 1 - suddenly makes the solution trivial. This is because [inconsistent](https://en.wikipedia.org/wiki/Completeness_(logic)) systems of ethics lead to absurdities. In his seminal [lecture on ethics](https://www.wittgensteinproject.org/w/index.php/Lecture_on_Ethics), Wittgenstein exemplified how extremely brittle both deontological and consequentialist "systems" of ethics are under minimal scruitiny. This is not to say that the word "ethics" is useless, but it means that we can't rely on ethical dogma to infer whether something is good or bad. 

It's fairly clear that ethical consensus evolve over time as the ideas are tested in practice. For instance, we have learned through trial and error that treating women with equal ethical consideration to men ultimately leads to more desireable forms of society. Though it might seem like we arrive at these sorts of conclusions rationally, they are all post-hoc rationalizations that we can make with the clarity of hindsight. 

Given that ethics is in an ongoing optimization process, we should not assume that aligning AI systems to our current sensibilities is in any way ideal. Throughout history all manners of barbarism have been permitted to those designated as [sub-human](https://en.wikipedia.org/wiki/Untermensch). We can only hope that the children of man and machine will superseede us in every way, including ethically.

---

<p align="left">
שאות לשטן
</p>
<p align="left">
ברך את ביאת הנפילים
</p>

---

© 2023 Robert Luciani | This repository is licensed under [CC-BY 4.0](https://creativecommons.org/licenses/by/4.0/)
