---
layout: post
date: 2020-07-14 KST
author: Sori Lee and Mia
---

# Review of "Improving ... Subgraph Pooling" by Crouse *et al.* (2020)

## Overview

We understand the architectural contributions of this work to be twofold:

1. In previous works of graph representation-based theorem proving, relatively little sophistication has been afforded to the process of drawing the final embedding of a graph from its node embeddings. All of the only such works the reviewers are aware of, namely [Wang17] and [Pal20], simply take the maximum of the node embeddings.[^1] The work under discussion introduces so-called DAG LSTMs, a simple generalisation of Tree LSTMs [Tai15], and uses it for the aggregation of node embeddings in an effort to TBC

<!-- This effort 



 to aggregate the node embeddings in a way respecting 



 The work under discussion adds sophistication to 
invents / devises 
uses so-called DAG LSTM
in order to take the graph structure of the formula into account

from the syntax tree of the formula.-->

[^1]: [Pal20], §&nbsp;5.3, *GNN Hyperparameters*:

      > The node embeddings $$h_v$$ returned by the graph neural network are then aggregated into a single vector that represents the embedding of the entire graph. ... Then we perform max pooling over all node embeddings to create a single vector of size 1024.

      [Wang17], §&nbsp;3.2:

      > Then we max-pool the node embeddings across all of nodes in the graph to form an embedding for the graph.


## References

- [Pal20] Aditya Paliwal, Sarah Loos, Markus Rabe, Kshitij Bansal and Christian Szegedy (2020). "Graph Representation for Higher-Order Logic and Theorem Proving". In *Proceedings of the AAAI Conference on Artificial Intelligence*, 34(03), 2967-2974. Palo Alto, California, USA: AAAI Press. <https://doi.org/10.1609/aaai.v34i03.5689>

- [Tai15] Kai Sheng Tai, Richard Socher and Christopher D. Manning (2015). "Improved semantic representations from tree-structured long short-term memory networks". In *Proceedings of the 53rd Annual Meeting of the Association for Computational Linguistics and the 7th International Joint Conference on Natural Language Processing (Volume 1: Long Papers)*, pp. 1556–1566. <http://dx.doi.org/10.3115/v1/P15-1150>

*Footnotes.*
