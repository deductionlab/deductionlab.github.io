---
layout: post
date: 2020-07-14 KST
author: Sori Lee and Mia
---

# Review of "Improving ... Subgraph Pooling" by Crouse *et al.* (2020)

### Overview

We understand the modelling contributions of this work to be twofold. Both moves seek to improve the neural representations of logical formulae in such a way that they are better suited particularly for the two crucial subtasks of theorem proving: premise selection and proof step classification.

1. In previous works of graph neural network-based theorem proving, relatively little sophistication has been afforded to the process of drawing the final embedding of a graph from its node embeddings. All such works the reviewers are aware of, which are just [Wang17] and [Pal20], simply take the maximum of the node embeddings.[^1] The work under discussion introduces so-called DAG LSTMs, a simple generalisation of Tree LSTMs [Tai15], and use it for the aggregation of node embeddings in a manner that respects the structure of the formula graph.

2. Previous neural approaches to automated theorem proving, certainly all the two that used graph neural networks, have embedded premise and conjecture formulae independently of each other.[^2] The authors consider this as a room for improvement, and proposes an attention mechanism that facilitates the exchange of information between the two graph embeddings.

[^1]: [Pal20], §&nbsp;5.3, *GNN Hyperparameters*:

      > The node embeddings $$h_v$$ returned by the graph neural network are then aggregated into a single vector that represents the embedding of the entire graph. ... Then we perform max pooling over all node embeddings to create a single vector of size 1024.

      [Wang17], §&nbsp;3.2:

      > Then we max-pool the node embeddings across all of nodes in the graph to form an embedding for the graph.

[^2]: The work under discussion, [Cro20v3], on p.&nbsp;2 writes:

      > Additionally, most prior approaches have embedded the premise and conjecture formulae independently of each other [22, 21, 23, 18].

      Here, the citations 22 and 23 are the two previous graph-based appraoches.

### Overall architecture



### DAG LSTMs

The DAG LSTM is a simple generalisation of the Child-Sum Tree LSTM [Tai15].
It is basically an intact adaptation of the latter to directed acyclic graphs, except for an added flexibility over the direction of information flow: in a Child-Sum Tree LSTM, information flows from children to parents, whereas in a DAG LSTM, the direction is a hyperparameter.

The DAG LSTM is described by the following equations.

1. $$i_v = \sigma(W^\text{input})$$

<!--

Let $$R$$ be

A DAG LSTM is determined by the following equations

DAG LSTMs are a simple generalisation of Child-Sum Tree-LSTMs [Tai15]. Here I will give a self-contained description of DAG LSTMs without reference to Tree LSTMs.

A DAG LSTM consists of DAG LSTM *units* indexed by nodes $$v$$.
The unit associated with node $$v$$ is a parametrised function that takes three vectors -- (1) the *input vector* at $$v$$, (2) the *cell states* of the neighbouring nodes and (3) the *hidden states* of the neighbouring nodes -- to two vectors -- (1) the hidden state $$h_v$$ of $$v$$ and (2) the cell state $$c_v$$ of $$v$$.

$$h_v = o_v \odot \tanh(c_v)$$

The *forget gate* at $$v$$ refers to the function
\\[
f_v = \sigma(W^\text{f}s_v + \sum_{w \in V \mid vRw} U^\text{f}_).
\\]

 that takes
- a vector
- a vector
Its parameters are
- 
Its independent variable is 


It is defined in terms of three subcomponents: *forget gate*, *input gate* and *output gate*.
Each gate is a function that 

-->


### Attention mechanism for information exchange between premises and conjectures

<!-- ### Discussions -->

### References

- [Cro20v3] Maxwell Crouse, Ibrahim Abdelaziz, Cristina Cornelio, Veronika Thost, Lingfei Wu, Kenneth Forbus and Achille Fokoue. "Improving Graph Neural Network Representations of Logical Formulae with Subgraph Pooling". 5 Jun 2020. <https://arxiv.org/abs/1911.06904v3>

- [Pal20] Aditya Paliwal, Sarah Loos, Markus Rabe, Kshitij Bansal and Christian Szegedy (2020). "Graph Representation for Higher-Order Logic and Theorem Proving". In *Proceedings of the AAAI Conference on Artificial Intelligence*, 34(03), 2967-2974. Palo Alto, California, USA: AAAI Press. <https://doi.org/10.1609/aaai.v34i03.5689>

- [Tai15] Kai Sheng Tai, Richard Socher and Christopher D. Manning (2015). "Improved semantic representations from tree-structured long short-term memory networks". In *Proceedings of the 53rd Annual Meeting of the Association for Computational Linguistics and the 7th International Joint Conference on Natural Language Processing (Volume 1: Long Papers)*, pp. 1556–1566. <http://dx.doi.org/10.3115/v1/P15-1150>

*Footnotes.*
