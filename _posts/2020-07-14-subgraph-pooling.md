---
layout: post
date: 2020-07-14 KST
author: Sori Lee and Mia
---

# Review of "Improving ... Subgraph Pooling" by Crouse et al. (2020)

## Overview

We understand the architectural contributions of this work to be twofold:

1. In previous works of graph representation-based theorem proving [ADD REFS], relatively little sophistication has been afforded to the process of drawing the final embedding of a graph from the its node embeddings. 
For instance, Paliwal *et al.* (2020) simply take the maximum of the node embeddings as the graph's embedding.[^1]

[^1]: [Pal2020], §&nbsp;5.3, GNN Hyperparameters:

> The node embeddings $$h_v$$ returned by the graph neural network are then aggregated into a single vector that represents the embedding of the entire graph. ... Then we perform max pooling over all node embeddings to create a single vector of size 1024.
