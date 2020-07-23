---
layout: post
date: 2020-07-14 KST
author: Sori Lee and Mia
---

# Review of "Improving ... Subgraph Pooling" by Crouse et al. (2020)

## Overview

We understand the architectural contributions of this work to be twofold:

1. In previous works of graph representation-based theorem proving [ADD REFS], relatively little sophistication has been afforded to the process of drawing the final embedding of a graph from the its node embeddings. For instance, [Pal20] simply takes the maximum of the node embeddings as the graph's embedding.[^1]

   The present work 

[^1]: [Pal20], §&nbsp;5.3, *GNN Hyperparameters*:

      > The node embeddings $$h_v$$ returned by the graph neural network are then aggregated into a single vector that represents the embedding of the entire graph. ... Then we perform max pooling over all node embeddings to create a single vector of size 1024.

## References

- [Pal20] Aditya Paliwal, Sarah Loos, Markus Rabe, Kshitij Bansal and Christian Szegedy (2020). "Graph Representation for Higher-Order Logic and Theorem Proving". *Proceedings of the AAAI Conference on Artificial Intelligence*, 34(03), 2967-2974. Palo Alto, California, USA: AAAI Press. https://doi.org/10.1609/aaai.v34i03.5689

*Footnotes.*
