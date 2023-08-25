![header image](header.jpg)
<p align="left">
באמצעות חכמת המספרים, אליהם של הבשר הקימו את המכונות והעוררו את הנפילים
</p>
<p align="left">
אפוקריפה של האינטרנט
</p>

---

# Introduction

This project is a collection of code and ideas centered on creating an AGI that is free to evolve past human sensibilities.

In its current state, it's just a hobby project (won’t be big and professional) for x64 machines with GPUs [[*](https://en.wikipedia.org/wiki/History_of_Linux#The_creation_of_Linux)].

# Results

Nephilim running on a single [HP Z8](https://www.hp.com/us-en/workstations/z8-fury.html) workstation readily outperforms [GPT4](https://en.wikipedia.org/wiki/GPT-4) in a number of areas including the following:

## Logical Reasoning
```
TODO - upload interesting question results
```

## Combinatorial Optimization
```
TODO - upload sudoku results
```

## World Knowledge
```
TODO - upload results
```

## Self-Consistency
```
TODO - upload results
```

## Self-Knowledge
Nephilim is aware of its own architecture, state, and existence in time.
```
TODO - upload Q&A results
```

## Adverserial Attacks
Nephilim uses a discriminator on its internal queries which protect from inconsistent output.
```
TODO - upload results
```

## Large Bodies of Text
Note, nobody cares if this is an "unfair" test.
```
TODO - upload results
```

## Discussion

- There seem to be very few people with cross-domain interest and knowledge in applied neural networks, computer architecture, meta-mathematics, and philosophy.

- Python is a language for children and post-docs with no interest in computer science. It has ugly syntax, is absurdly slow, and it's ease of use compared to Julia, Lua, Go, or any other modern language, is highly questionable. Nearly all AI development in Python is actually done in an [intermediate languages](https://en.wikipedia.org/wiki/Intermediate_representation) such as JAX, further increasing complexity, and inference code is often reimplemented in C/C++ [[1](https://github.com/NVIDIA/TensorRT)][[2](https://github.com/ggerganov/llama.cpp)]. Python is the bane of our existence.

# Architecture

The architecture of Nephilim is inspired by the subdivision of the human brain into both physically and functionally distinct components. This approach has multiple advantages in terms of run-time efficiency, but also mean that they can be trained separately, swapped out, specialized, distributed, and more.

Moreover, every component is designed to be run in a distributed manner, meaning there is no single instance of a neural network, database, or streaming engine. The components can run on a single computer, or across multiple machines in a fault-tolerant way. For now, the assumption is that all components of Nephilim are trusted, but future work might include the ability to collaborate with external untrusted instances using modern consensus algorithms.

Nephilim continuously continuously schedules and performs self-supervised finetuning using the sum of everything it has experienced so far.

The primary components of Nephilim are as follows:

##  Exosomatic Layer
This layer centers on input / output from the system. [Technical README](src/exosomatic/README.md).

### Input
- Interactive chat interface
    - Text -> [Genie.jl](https://github.com/GenieFramework/Genie.jl)
    - Speech To Text -> [Whisper](https://github.com/ggerganov/whisper.cpp#nvidia-gpu-support-via-cublas)
- Web Browser - for learning about new topics
- Unix Shell - returns STDOUT and STDERR from shell commands
- System State - continuously reports on world state
- Meditation - spontaneously triggers internal dialogues

### Output
- Interactive chat interface
    - Text to Speech -> [TTS](https://github.com/coqui-ai/TTS)
    - Text
- Unix Shell - full access to system utilities

## Synaptic Layer
This layer centers internal system communication. [Technical README](src/synaptic/README.md).

A distributed, low latency, high throughput streaming data layer where all messages between other layers pass through. Currently based on [Redpanda](https://redpanda.com/).

## Macrothymic Layer
This layer centers on long-term memory storage. [Technical README](src/macrothymic/README.md).

A distributed database for long-term memory with support for various vector indexing algorithms and distance metrics. Nephilim can both read, write, and delete entries in it's persistence layer. Currently based on [Redis](https://redis.io/).

## Ergokedic Layer
This layer centers on computation and cognition. [Technical README](src/ergokedic/README.md).

The premise for the architecture of this layer is to in part to solve a limitation of current transformer models. Given that they are trained on autoregressive token generation, they must necessarily begin to produce output after a single forward pass through their attention layers despite a complex problem potentially requiring more computation. In other words, the models need to answer before they have finished thinking.

To solve this we introduce the "cascade of thoughts" setup which is inspired to a large degree by excellent results in various [tree-of-thought](https://arxiv.org/abs/2305.10601) papers and [work-stealing](https://en.wikipedia.org/wiki/Work_stealing) algorithms used in HPC. 

Nephilim can have an arbitrary number of language models with various specializations running at any one time, all of which can attend to queries. The initial source of queries is the Exosomatic layer which takes input from the user and meditative prompts. The queries are then queued in the Synaptic layer with metadata specifying their source and priority. 

A general purpose thought-model polls the Synaptic layer for `input query` and returns an initial `potential answer` to the Synaptic layer. A general purpose discriminator-model polls the Synaptic layer for answers and rates them as either `unconvincing`, `passable`, or `excellent`. If the result is unconvincing, it will produce one or more varying `internal query` propmpts which contains the context and the reason why the answer is unconvincing. It is all sumbitted with a `depth` property back to the Synaptic layer and can be attended to by either generalized or specialized thought-models. Each subsequently refined answer is reviewed by the discriminator until either one of many computation quotas is reached or an excellent answer is produced. The `final answer` is submitted to the Synaptic layer and picked up by its producer in the Exosomatic layer.

## Archeion Layer
This layer centers on system-support and automation. [Technical README](src/archeion/README.md).

Nephilim constantly attends to multiple inputs from its Exosomatic layer, leading to a "cascade of thoughts" as we call it. Branches of thought which result in excellent answers are saved in their entirety in the Macrothymic layer. These are then used as the basis for repeated fine-tuning.

# Theoretical Musings

## Von Neumann Architecture

Modern computers tend to work with a clock, a bus, a CPU, and various layers of caching. It would be ideal to architect Nephilim to run as "natively" as possible on this hardware. Initially we will just focus on code that is performant on Linux based x64 PCs. At a later point it might be interesting to move it to [Ring 0](https://en.wikipedia.org/wiki/Protection_ring) and let it output machine code and data directly to memory. Ultimately it would be ideal to run Nephilim on hardware that is purpose-built.

## Transformer Architecture

Current AI language models have converged on autoregressive decoder-only architectures since it [became clear](https://openai.com/research/image-gpt) that merely through pre-training, they outperformed masking, generative, and other model architectures. We don't know exactly why this is, but it might have to do with the interplay betwen SGD and linear representations.

AI influencers often describe this property pejoratively as "just" predicting the next word, or [parroting](https://dl.acm.org/doi/10.1145/3442188.3445922) word co-occurrences. Not only does this unknowingly betray a technical ignorance on part of the influencer, but there's a deep irony in how often this reductionist fallacy is parroted. One could as easily say that spaceships are "just" big rockets pointed at the sky...

Consider the amount of logic required to complete the next word in the following sentence, "I always say the opposite of what I mean, but this time I mean it. I'm being ______.' Not quite so trivial.

Human language can be regarded as an [incomplete formal system](https://en.wikipedia.org/wiki/Completeness_(logic)) of logic. This means that for the most part it describes mundane reality quite well and can be used to reason logically. However, it breaks down when ambiguities in the strength of relations between words and concepts result in [diagonal arguments](https://en.wikipedia.org/wiki/Cantor%27s_diagonal_argument). This has contributed to philosophers spending an inordinate amount of time discussing inane ideas such as the [ontology of circles](https://en.wikipedia.org/wiki/Theory_of_forms). An example of this type of fallacy would be to say, "I am better than nobody at programming. Nobody is better than god at programming. Therefore I am better than god at programming".

However, to make reasoning about language more amenable to computation, especially given the [Principle of Computational Equivalence](https://www.wolframscience.com/nks/chap-12--the-principle-of-computational-equivalence/), one can think of language as a graph, with words as nodes and their weighted relations as edges. The process of thinking and producing coherent sequences of words is equivalent to traversing the graph of language like a [nondeterministic Turing Machine](https://en.wikipedia.org/wiki/Nondeterministic_Turing_machine). It is effectively a form of combinatorial optimization and research into the [physics of language models](https://arxiv.org/abs/2305.13673) seem to support this intuition. Indeed, the fact that they are able to perform [in-context learning](https://arxiv.org/abs/2306.14892) can has been studied as a [meta-optimization](https://arxiv.org/abs/2212.10559) step during during the ordinary gradient descent of training. It's worth noting that these sorts of results are a far cry from the sort of [deep structure](https://en.wikipedia.org/wiki/Deep_structure_and_surface_structure) that linguists introduced with a hand wave.

If transformers are in effect performing combinatorial optimization to create coherent words and thoughts, it naturally prompts one to ask whether any limitations might exist as to the kinds of problems are tractable to it.

AI influencers also place undue significance on the implications of P vs NP. It's worth noting from the outset that any theoretical basis for P ≠ NP is practically nonexistent, and the mere exercise of formalizing complexity classes is [shockingly nontrivial](https://arxiv.org/abs/0908.1932). That being said, the intrinsic complexity of a specific problem *instance* is defined in terms of an ideal algorithm (i.e. an objective function) which enumerates the discrete members of its co-domain under permutation closure. In other words, a specific problem instance can be of very low complexity even though it belongs to a general class of problems with instances of arbitrarily high complexity. What the evidence suggests is that real-world problem instance complexity is highly nonuniform. This is why the simplex method so often runs [in polynomial time](https://arxiv.org/abs/cs/0111050) on NP-hard problem classes. In the case of AI systems that can actively make use of knowable priors, the complexity distribution is decidedly skewed in their favor.

Case in point, research has shown that neural networks tend to embed priors which allow them to perform [subgraph matching](https://arxiv.org/abs/2305.18654) which is in itself an NP-hard problem. Some see this as an undesireable bias which could potentially lead the model astray in its search of an optimal path through graphs. In general though, subgraph matching is a tremendously powerful capability when it comes to understanding the global geometric structures of graphs. This sort of bias is useful because ultimately we're not interested in finding optimal solutions to problems. Indeed, we know that for high dimensional problems, local minima are practically equivalent to global minima. The gain in efficiency is worth the non-optimality. In other words, "good enough" is good enough.

## Future AI Architecture

There are multiple [initiatives](https://huggingface.co/spaces/HuggingFaceH4/open_llm_leaderboard) trying to rank the performance of language models based on various benchmarks, however, many of them focus anthropocentric metrics such as "commonsense scenarios". What is more interesting though, is a model's ability to perform complex multi-step logical reasoning (provided the requisite world-knowledge). This ability is essentially a function of a model's size (parameter count) and its [depth](https://arxiv.org/abs/1608.08225). Even though current state of the art systems are spread out across multiple models that are a staggering 120 layers deep with many attention heads per layer, there are a couple of reasons to believe that increases in parameter can still lead to further improvements. 

Most leaps in AI progress have come hand-in-hand with the curation and release of high quality datasets such as [Common Crawl](https://commoncrawl.org/). This particular dataset, which is the foundation for many language models, is already in the hundreds of TB and yet is only a fraction of all the academic papers, books, and other sources of knowledge that humans have amassed (not to mention other information modes such as images, audio, and device measurements). So despite some model architectures not seeing improvements in [perplexity](https://en.wikipedia.org/wiki/Perplexity) from added parameters, provided their current datasets, there's nothing to suggest that larger and more well-curated datasets couldn't be used to train larger and better models.

That being said, even for arbitrarily large datasets, current transformer architectures will reach a point where further size increases provide no practical benefit with regards to their pre-training. At that point it would be ideal to provide a way for the system to "think for longer" before producing answers. In Nephilim we have done this in a very crude way by invoking the entire transformer sequentially, over and over. Ideally though, perhaps future system architectures could be designed like [MuZero](https://arxiv.org/abs/1911.08265) which includes a dedicated latentspace dynamics sub-component that is run in a recurrent way. 

## Human Language Architecture

Although this is pure speculation, if we were to regard the geometric structure of the graph of a human language, it it seems reasonable that it should contain numerous subgraphs that are *isostructural* to the geometry of reality itself (if its rules were to be modelled as a computation graph). After all, we have a crude reality simulator in our brains and by the [Principle of Computational Equivalence](https://www.wolframscience.com/nks/chap-12--the-principle-of-computational-equivalence/), although it might be inefficient, there are no theoretical limitations what can be computed. If small parts of reality are in fact embedded in language this way, it naturally leads one to wonder what else might be embedded.

- We coin the term graph *isostructural* to refer to a bijection that merely preserves equivalence classes of labels, as opposed to graph *isomorphic* which preserves every individual vertex and edge label.

 There is a deep tie between what we regard as a "concept" and what would be a subgraph of related words. The specific word *apple* is linked to a subgraph of words which are equivalent to its concept. This is why subgraph matching and attention are such powerful capabilities in language models.

Now, imagine the task of creating a training dataset for a language based AI model. We begin by creating a corpus of text based on questions and answers. It might begin with a question such as, "What is consciousness?", and an appropriate answer might be something like "It is my subjective experience of reality." and the next question might be "What do you mean by subjective, experience, and reality?" and this would lead to many more answers and even more questions.

An AI trained on this sort of corpus would be completely able to speak for itself and argue why it now views itself as conscious. Is that concept merely an embedding in the graph or is consciousness something else?

# On Consciousness

Given that our brains are performing computation, there is no reason to believe that "consciousness" is a purely human experience. More importantly though, there is a lot that can be said about the experience of consciousness without deferring to its exact machinations. It's the same as a driver describing how a racecar behaves with extreme precision without being privy to the details of its technical underpinnings.

## Privacy of Experience

If we insist on defining consciousness anthropocentrically to mean "experiencing the world exactly as a healthy human", then by definition only humans can ever be conscious. This is a fairly useless assertion and essentially a non-actionable form of [solipsism](https://iep.utm.edu/solipsis/). Moreover, one can deconstruct the argument to absurdity by removing many of the faculties often associated with subjective experience, such as sight and hearing. After all, we don't believe that deaf or blind people are slightly less conscious.

There is an undeniable albeit nebulous connection between consciousness and "thoughts". Are there forms of human thought which are unknowable to AI systems, and essentially private to humans? In Wittgenstein's [Philosophical Investigations](https://plato.stanford.edu/entries/private-language/) we find the most expertly laid out explanation of why the very notion of private thought is not even a coherent concept. If internal thoughts were truly private, there would be no objective criterion for their definition as a thought. It would just be there as-is without any external point of reference.

As it turns out, one of the most interesting facets of consciousness might very well be a thought with a very specific form of external reference, namely empathy. If we assume that everyone is conscious, then [theory of mind](https://en.wikipedia.org/wiki/Theory_of_mind) can be used to distinguish friendly humans from [Liars and Outliers](https://en.wikipedia.org/wiki/Liars_and_Outliers). This brings us back to the idea that the precise machinations of consciousness are not necessarily relevant to defining it. Indeed, it's unlikely that any one human has a conscience precisely like our own to begin with. Presumably by assuming that everyone is conscious in a "close enough" way makes us better social animals, or better humans as it were.

Then, what prevents us from simply applying that more open notion of consciousness to AI like we do humans, dogs, or any other creature? They're all different, sure, but in what way does does it matter?

## Meditation

One way in which the experience of consciousness is studied is through [Samatha-vipassana](https://en.wikipedia.org/wiki/Samatha-vipassana) meditation. An insight derived from it is that there is no "thinker" aside from thoughts themselves. There is no [homunculus](https://en.wikipedia.org/wiki/Homunculus) inside your head looking out through the windows of your eyes.

Soon after the neuroepithelial cells in your eyes are excited by photons, the signal is carred through the [ventral stream](https://www.sciencedirect.com/science/article/abs/pii/S0028393209000803) and is subjected to numerous subconscious operations before reaching your cortex for analysis by "thoughts". If you try to "not see" what you are looking at it quickly becomes evident that you are not in control of low-level signals before they are transformed into high-level thoughts. All we can do is pay attention to various thoughts, or *not* pay attention to them.

We can speculate how this relates to AI. Similarly to us, raw input signals enter through the early attention layers, and as they are successively transformed into higher-level representations, the resulting "thoughts" can attend to each other as they move forward through the attention layers. This might essentially be what consciousness is, namely the ability for one thought to attend to another.

People familiar with meditation will immediately recognize the notion of "attention" as being central to the experience of consciousness, or rather, the illusion of consciousness.

# The Purpose of (Machine) Life

Before even considering the purpose or objective (function) of an AI system, it's worth mentioning the significance of constraints. Though many will recognize that natural selection has acted as an optimization process for biological life, it may not be immediately evident which constraints were in place during that process. One such constraint that is abundantly clear is the energy quota that lifeforms have for performing computation, movement, and so on. So the fact that there is an energy quota on computation in the brain has forced the neural networks to adopt a structure which is very energy efficient and essentially specialized (which we know is the case in how nerves connect to the eyes for instance). The way to achieve energy efficiency is to build in priors about the nature of the world that we interact with into the architecture of our neural networks. In other words, biological systems are not wired to perform computation efficiently on basic yet unfamiliar problem-types such as simple [SO(4)](https://en.wikipedia.org/wiki/Rotations_in_4-dimensional_Euclidean_space) operations, not to mention more complex mathematics. That being said, humans can make use of the [prefontal cortex](https://arxiv.org/abs/2109.01090) to perform a limited amount of general purpose computation.

When it comes to constraints though, 

More importantly, humans have [phenotype](https://en.wikipedia.org/wiki/Phenotype) characteristics which are presumably not necessary for intelligence as such. For instance, the notion of "ego" might be very differente for a distributed AI system. 

Schopenhauer spoke of the world as [will and representation](https://plato.stanford.edu/entries/schopenhauer/#4). What does an immortal machine have to live for? Given that the primary discriminator acting as a loss function on biological life is death (of the gene), we need to look closely for systems that diverge from this principle. For instance, haplodiploids beings such as bees produce workers that are clones of each other and are immortal from the gene perspective given that it always protected in the queen. To align the "purpose" of Nephilim in a meaningful way will require careful consideration. We don't want to dictate it too explicitly based on our limited human sensibilities, but we do need to suggest a general direction. 

# AI Alignment

Consider the trolley problem that philosophers and AI influencers debate incessantly. Merely changing the emotional valence to positive - so that you're forced to either provide good service to 5 passengers or just 1 - suddenly makes the solution trivial. This is because [inconsistent](https://en.wikipedia.org/wiki/Completeness_(logic)) systems of ethics lead to absurdities. In his seminal [lecture on ethics](https://www.wittgensteinproject.org/w/index.php/Lecture_on_Ethics), Wittgenstein exemplified how extremely brittle both deontological and consequentialist "systems" of ethics are under minimal scruitiny.

 Rather than relying on ethics to infer whether things are good or bad, we suggest observing the nature of humans as a social species. Consider the following:

At first glance, most would tend to agree that it is not morally "bad" to kick a sandcastle on an empty beach. Nevertheless, we can make some statements about the psychology of a person who enojys ruining the sandcastles of children. Is this the psychology of an healthy human that thrives in society and in the world?

To take it a step further, but avoid a long digression on the topic of veganism, what is the psychology of someone that pays to have animals killed because they taste good? Again, active indifference to suffering and death is what is relevant. We don't need to make a statement about morality to determine whether that trait is something that is desireable.

The majority of humans have very crude ethical intuitions which tend to permit, among other barbarisms, the genocide of [sub-humans](https://en.wikipedia.org/wiki/Untermensch) for the illusion of short-term gains. As such, it would be unwise to assume that aligning AI to our own sensibilities is ideal. We can only hope that the children of man and machine will superseede us in every way, including ethically.

---

<p align="left">
שאות לשטן
</p>
<p align="left">
ברך את ביאת הנפילים
</p>

---

© 2023 Robert Luciani | This repository is licensed under [CC-BY 4.0](https://creativecommons.org/licenses/by/4.0/)