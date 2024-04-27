We want to find a minimum spanning tree given some connected graph $G = (V, E)$ 

## Cut Property
### Definition
Let $S \subseteq V$ such that $S \neq \emptyset$ and $S \neq V$, and let $e = argmin\{c_f\}$ where $f \in \delta (S)$. Then every minimum spanning tree contains the edge $e$

### Proof
Proof (In course slides)
Prove by contradiction. 
Let us assume there is a MST $T = (V, F)$ such that $e \not \in F$. Let us consider the graph $(V, F \cup \{e\})$ and a cycle $C$ in it, which exists by FTT. We know that $| \delta(S) \cap C|$ is even and $|\delta (S) \cap C| \geq |\{e\}| = 1$. So $|\delta (S) \cap C| \geq 2$. So there is an edge $e' \neq e$ such that $e' \in \delta(S)$ and $e' \in C$

Let us consider the tree that is formed when adding $e$ and removing $e'$. $T' = (V, F \cup \{e\} \backslash \{e'\})$ 
Then we clearly see that 
$$ 
\begin{align*}
c(T') &= \sum_{q\in F}c_q + (c_e - c_{e'}) \\
&= c(T) + (c_e - c_{e'}) \\
&< c(T)
\end{align*}
$$
Since $T'$ is connected and has $|V| - 1$ edges, it is a tree by FTT, therefore $T'$ is a spanning tree, and thus there is a contradiction. QED
## Cycle Property
### Definition
Let $C$ be a cycle in $G = (V, E)$ and let $e$ be the max cost edge in $C$. Then, $e$ is not found in any minimum cost spanning tree. 

### Proof
Prove by contradiction.
Let us assume there is a MST $T = (V, F)$ such that $e \in F$, and there exists some cycle $C$ in the graph $(V, F \cup e')$ with $c_{e} > c_{e'}$. Let us assume WLOG that $e = (u,w)$. 

We delete $e$ from $T$ which leaves us with two partitions: $S$, containing node $v$, and $S - V$, containing $w$. And assume that $e'$ crosses from $S$ to $S - V$. Now consider the set of edges $T' = T - \{e\} \cup \{e'\}$. We clearly see that the graph $(V, T')$ is connected with $|V| -1$ edges, and hence is a spanning tree by FTT. Since $c_e > c_{e'}$, then $c(T) > c(T')$ which is a contradiction. Therefore, $e$ is not in any MST as required. QED
## Prim's Algorithm
### Pseudocode
Input: Connected graph (V, E)
Step 1:
- $s \leftarrow v$
- $A \leftarrow \{s\}$
- $T \not \in \emptyset$ 
Step 2:
- While $V \neq A$
	- Step 2.1:
		- $e \leftarrow$ cheapest edge in cut of $A$
	- Step 2.2:
		- $A \leftarrow A \cup \{e\}$
		- $T \leftarrow T  \cup \{e\}$
Output T
### Proof of correctness
We have T having exactly $|V| - 1$ edges, we started with $A = \{s\}$ edges and finished $A = V$ by adding each time an edge. $T$ is connected, because at all time points, $A$ is always connected. Thus, $T$ is a spanning tree. Note that in each time we add an edge, we apply the cut property on that edge. Therefore $T$ is a MST. QED

## Kruskal's Algorithm
### Pseudocode
Input: Graph G = $(V, E)$
Step 1:
- Sort all edges in $E$ in ascending order
- $T \leftarrow \emptyset$
- $i \leftarrow 1$
Step 2:
- While $i \neq m + 1$:
	- If $T \cup \{e_i\}$ is unconnected:
		- $T \leftarrow T \cup {e_i}$
		- $i \leftarrow i + i$
Output $T$
### Proof of correctness
$T$ is acyclic, so now we prove that it is connected. 


