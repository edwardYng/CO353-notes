Given a graph $G = (V,E)$, edge costs $c_{e} \geq 0$, $e \in E$, terminals $T \subseteq V$, find a minimum cost tree that spans T


### Transformation to Steiner Tree Problem
Given $G = (V,E)$, $c_{e} \geq 0$, $e \in E$ and $T \subseteq V$, construct $G' = (V', E')$ which is a complete graph.
- $T' = T$
- $c'_{uv}$ = the length of a shortest path between $u$ and $v$ in the graph $G$ with respect to the costs $c$ for every $u, v \in V$

Lemma
1) Given a Steiner tree $F$ for $G = (V,E)$ and terminals $T$, we can efficiently compute a Steiner tree $F'$ for each $G' = (V, E')$ and $T'$ such that $c(F) \geq c'(F')$

Corollary.
The minimum cost of a Steiner Tree is the same for both the original and transformed problems

Proof
1) Take $F'$ equal to $F$. $F'$ is a Steiner tree in the transformed instance and $c'(F') = c'(F) \leq c(F)$ because $c'_{e}\leq c_{e}$ for every $e \in E$ 
2) Consider $\overline{F} = \cup P_{uv}$ ($\overline{F}$ is the union of all shortest $u-v$ paths in $G$). Note that in $\overline{F}$ we keep multiple copies of the same edges and that $c(F') = c(\overline{F})$ 

### 2-approximation Algorithm for Steiner tree
#### Pseudocode
Inputs: Given $G = (V, E)$, $c_{e} \in E$, $e \in E$ and terminals $T$
Compute minimum cost spanning tree $F'$ in the graph $(T, E'[T])$ where $E'[T]$ are the edges in $E'$ with both endpoints in $T$
Output $F$ that corresponds to $F'$ in the above lemma

#### Theorem
The above algorithm is a 2-approximation algorithm for the optimal Steiner tree.
##### Proof
Let $F^*$ be an optimal Steiner tree with cost $OPT$
Construct a tour, $z$ by following $F^*$ starting from the root node in a DFS way. The tour $z$ uses all the nodes in $F^{*}$ and $c(Z) \leq 2c(F^{*)}= 2OPT$ 

Let us shortcut $z$ by constructing $\overline{z}$ which is the cycle of terminal nodes visited in order of how they were visited in $z$ (i.e $\overline{z} = u_{i1}, u_{i2} \dots u_{i|T|}$). Because of triangle equality, the shortcuts do not increase the cost of the tour. If we delete one edge in $\overline{z}$ we obtain a path that spans $T$ and has cost at most $2 * OPT$ 