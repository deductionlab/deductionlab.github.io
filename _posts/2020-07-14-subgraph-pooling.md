---
layout: post
date: 2020-07-14 KST
author: Sori Lee and Mia
---

# Review of "Improving ... Subgraph Pooling" by Crouse *et al.* (2020)

### Overview

We understand the architectural contributions of this work to machine-learned theorem proving to be twofold. Both of the two seek to improve the neural representations of logical formulae in such a way that they are better suited for two major subtasks of theorem proving particularly: premise selection and proof step classification.

1. In previous works of graph neural network-based theorem proving, relatively little sophistication has been afforded to the process of drawing the final embedding of a graph from its node embeddings. All such works the reviewers are aware of, which are just [Wang17] and [Pal20], simply take the maximum of the node embeddings.[^1] The work under discussion introduces so-called DAG LSTM, a simple generalisation of Tree LSTM [Tai15], and use it for the aggregation of node embeddings in a manner that respects the structure of the graph.

2. Previous neural approaches to automated theorem proving, certainly both of the two that used graph neural networks, have embedded premise and conjecture formulae independently of each other.[^2] The authors consider this as a room for improvement, and proposes an attention mechanism that facilitates the exchange of information between the two graph embeddings.

[^1]: [Pal20], §&nbsp;5.3, *GNN Hyperparameters*:

      > The node embeddings $$h_v$$ returned by the graph neural network are then aggregated into a single vector that represents the embedding of the entire graph. ... Then we perform max pooling over all node embeddings to create a single vector of size 1024.

      [Wang17], §&nbsp;3.2:

      > Then we max-pool the node embeddings across all of nodes in the graph to form an embedding for the graph.

[^2]: The work under discussion, [Cro20v3], on p.&nbsp;2 writes:

      > Additionally, most prior approaches have embedded the premise and conjecture formulae independently of each other [22, 21, 23, 18].

      Here, the citations 22 and 23 are the two previous graph-based appraoches.

### Overall architecture



### DAG LSTM

The DAG LSTM is a simple generalisation of the N-ary Tree LSTM [Tai15].
An N-ary Tree LSTM takes trees with a fixed maximum branching factor <!--(in other words, $N$-ary trees for a fixed $N \in \mathbf{Z}_{\geq 0}$)--> with ordered children.
A DAG LSTM generalises this, in that it takes simple DAGs with typed edges for a fixed set of edge types: indeed, any $$N$$-ary tree (i.e. a tree whose maximum branching factor is $$N$$) with ordered is a simple DAG with $$\{0,\ldots,N-1\}$$-typed edges, without any loss of information[^3].
Other than a straight adaptation for this generalisation, there is no change from the N-ary Tree LSTM.

[^3]: That is, there is an injective function from the set consisting of the former to the set consisting of the latter.

<!-- Why not Chlid-Sum Tree LSTM approach? -->

<!--
It is basically an intact adaptation of the latter to directed acyclic graphs, except for an added flexibility over the direction of information flow: in an N-ary Tree LSTM, information flows from children to parents, whereas in a DAG LSTM, the direction is a hyperparameter.

A *model* of DAG LSTM is given by the following hyperparameters and parameters.
-->

**Definition.** A *model* of DAG LSTM consists of the following data.

*Model hyperparameters.*

1. $$\delta \in \{-1, 1\}$$, the direction of information flow. $$1$$ means information flows in accordance with the direction of edges, and $$-1$$ means it flows in the opposite direction.

2. $$T$$, a finite set of *edge types*.

*Model parameters.*

3. $$W^\mathrm{in} \in \mathbf{R}^{n \times k}$$, the weights for the input gate.



TBC

<!--
The inputs to DAG LSTM with respect to hyperparameters $$(\delta,T)$$ are as follows.

1. A triple $$(V,E,t)$$, where $$(V,E)$$

   - $$(V,E)$$ is a simple DAG ($$E \subset V \times V$$), and
   - $$t$$ is a function $$E \to T$$.

   The triple may be referred to as the *input graph*.

2. For each node $$v$$

$$s_v$$, the input embedding.

is a directed acyclic graph equipped with a function $$

Let $$G = (V,E,T,\tau)$$ be a simple ($$E \subset V \times V$$) directed acyclic graph.
Let $$R$$ be either the relation $$E$$ or its inverse $$E^{-1}$$.
-->

The evaluation of DAG LSTM is described by the following equations.

1. The *input gate*: $$i_v = \sigma( W^\text{in}s_v + \displaystyle\sum_{w \in V \mid vRw} U^{\text{in},t(v,w)} h_w + b^{\text{in}} )$$.

2. The *output gate*: $$o_v = \sigma( W^\text{out}s_v + \displaystyle\sum_{w \in V \mid vRw} U^{\text{out},t(v,w)} h_w + b^{\text{out}} )$$.

3. The *forget gate*: $$f_{e} = \sigma( W^\text{fgt}s_v + U^{\text{fgt},t(e)} h_w + b^{\text{fgt}} )$$.

4. $$\hat{c}_v = \tanh( W^\text{cell}s_v + \displaystyle\sum_{w \in V \mid vRw} U^{\text{cell},t(v,w)} h_w + b^{\text{cell}} )$$.

5. $$c_v = i_v \odot \hat{c}_v + \displaystyle\sum_{w \in V \mid vRw} f_{(v,w)} \odot c_w$$.

6. $$h_v = o_v \odot \tanh(c_v)$$.

TBC.

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
