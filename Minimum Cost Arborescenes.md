Let us begin with a direct graph $G = (V, E)$ with a distinguished node $r \in V$

An arborescence with respect to $r$ is a graph $T = (V, F)$
- $T$ is a spanning tree when ignoring directions
- for every $v \in V$, there is a directed path from $r$ to $v$
### Characterization of an Arborescenes
#### Theorem
$T = (V, F)$ is an arborescence if and only if every $v \in V$ has exactly one directed incoming edge, and $T$ has no directed cycles.
#### Proof
"Only if"
For $v \in V$ $v \neq r$, there is a path from $r$ to $v$ in $T$. So $v \in V$ has at least one incoming edge. AND Since $T$ has $|V| - 1$ edges, each $v \in V$ has exactly one incoming edge. T has no cycles even if you flip the directions are ignores. So, $T$ has NO directed cycles.

"If"
Let us consider $v \neq r$ and the edge $(v_1, v)$ from $T$, and the edge $(v_2, v_1)$ and so on. If we reach $r$ in this way, then there is a directed path from $v$ to $r$. If we do not reach $r$ at some point, then we have encountered the same vertex more than once, and thus a directed cycle, which is a contradiction. So, we will always reach $r$. Clearly, $T$ is connected.

Now prove that $r$ in $T$ has no incoming edges. If there was an incoming edge into $r$ then that would be a directed cycle which does not exist. 
### Relationship Between Arborescences' Costs with Respect to the Reduced Costs and the Original Costs
#### Theorem
$T$ is an optimal arborescence in $G$ subject to costs $\{c_e\}$ if and only if it is an optimal arborescence subject to the modified costs $\{c'_e\}$ 

#### Proof
Consider an arbitrary arborescence $T$. The difference between its cost with costs $\{c_e\}$ and $\{c'_e\}$ is exactly $\sum_{v\neq r}y_v$. That is
$$
\begin{align*}
\sum_{e\in T}c_e - \sum_{e \in T}c'_e = \sum_{v \neq r}y_v
\end{align*}
$$
This is because an arborescence has exactly one edge entering each node $v$ in the sum. Since the difference between the two costs is independent of the choice of the arborescence $T$, we see that $T$ has minimum cost subject to $\{c_e\}$ if and only if it has minimum cost subject to $\{c'_e\}$ 
### Edmond's Algorithm
#### Intuition
Given a directed graph $G = (V, E)$, and some distinguished node, $r \in V$. Then we try to find the MCA from $r$.
- Now, all edges in $F^*$ have 0 cost with respect to reduced costs $c'(u,v)$
- $F^* =$ set of cheapest edges entering $v$ for each $v \neq r$. 
- If $F^*$ does not contain a cycle, then it is a MCA
- otherwise, we can afford to use as many edges in the cycle as desired.
- Contract the edges and vertices in the cycle into a supernode
- Recursively solve problem with contracted network $G'$ with costs $c'(u,v)$
#### Pseudocode
Inputs: Directed graph $G = (V, E)$, distinguished node $r$, edge costs $c$ 
Step 1:
- For each $v \neq r$
	- $y(v) \leftarrow$ min cost of any edge entering $v$
	- $c'(u,v) \leftarrow c'(u,v) - y(v)$ for each $(u,v)$ entering $v$
Step 2:
- For each $v \neq r$
	- choose one 0-cost edge entering $v$ and let $F^*$ be the resulting set of edges.
If $F^*$ is an arborescence
- Output $F^*$
Else
- $C \leftarrow$ directed cycle in $F^*$
- Contract $C$ to a single supernode, yielding $G' = (V', E')$
- $T' \leftarrow$ $EdmondsAlgorithm(G', r, c')$ 
- Extend $T'$ to an arborescence $T$ in $G$ by adding all but one edge of $C$
Output $T$

#### Lemma
Let $C$ be a cycle in $G$ consisting of edges of cost 0, such that $r \not \in C$. Then there is an optimal arborescence rooted at $r$ that has exactly one edge entering $C$. 
##### Proof
Case 0. $T$ has no edges entering $C$. 
Since $T$ is an arborescence, there is an $r-v$ path for each node $v$, therefore at least edge enters $C$. So, case 0 will never occur.

Case 1. $T$ has exactly one edge entering $C$.
$T$ satisfies the lemma.

Case 2. $T$ has more than 1 edge entering $C$.
We show that we can construct another MCA $T^*$ that has exactly one edge entering $C$. We construct $T^*$ with the following rules. Let $(a,b)$ be an edge in $T$ entering $C$ that lies on a shortest path from $r$. We delete all edges of $T$ that enter a node in $C$ except $(a,b)$. We add in all edges of $C$ except the one that enters $b$. Now we will prove the claim that $T^*$ is a MCA for $G$

Since all the edges in $C$ are of cost 0, the cost of $T^*$ is at most of $T$ since we add only 0-cost edges. $T^*$ has exactly one edge entering each node $v \neq r$. $T$ has no directed cycles. Hence, $T^*$ is a MCA
#### Proof of Correctness
Proof by strong induction
- If the edges of $F^*$ form an arborescence, then it is a MCA.
- Otherwise, we use reduced costs, which is equivalent
- After contracting a 0-cost cycle $C$ to obtain a smaller graph $G'$, the algorithm finds a min-cost arborescence $T'$ in $G'$ (by induction).
- We know that there exists an MCA $T$ in $G$ that corresponds to $T'$ from lemma above.

