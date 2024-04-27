### Polynomial Class P
P is the class of problems that can be solved in polynomial time

Examples:
- Shortest path
- Minimum cost Spanning tree
- Minimum cost arborescence

### Polynomial Time Reduction
Given two problems $X$ and $Y$, we say that $X$ reduces to $Y$ denoted as $X \leq_{p} Y$ if any instance of $X$ can be solved using a polynomial number of operations and calls to solutions of instances of $Y$

### Class NP
NP is the class of decision problems

We say that $B$ is an efficient verifier for a problem $X$ if the following holds
- $B$ is an efficient algorithm that takes in 2 inputs, some instance of $X$ and a certificate for "YES"
- If the instance of $X$ is "NO", $B$ will produce "NO" for all certificates
- If the instance of $S$ is "YES", then there exists some certificate such that the size of the certificate is polynomial in the size of the instance.

### 3SAT Reduces to Decision Vertex Cover/Independent Set problems
#### 3SAT problem
Given a set of boolean variables $\{x_{1}, x_{2}, \dots ,x_{n}\}$ and clauses $C_{1}, C_{2}, \dots , C_{k}$ where each of them have the form $(t_{1} \lor t_{2} \lor t_{3})$  where $t_{i} \in \{x_{1}, x_{2}, \dots ,x_{n}, \overline{x_{1}}, \overline{x_{2}}, \dots ,\overline{x_{n}}\}$ determine whether there exists an assignment of the variables such that $C_{1}, C_{2}, \dots , C_{k} =$ TRUE 
#### Decision Vertex Cover problem
Given a graph $G = (V,E)$ and a number $k$ determine whether there exists $U \subseteq V$ such that $|U| \leq k$ and and every edge in the graph has at least 1 endpoint in $U$.

#### Reduction
We construct the following graph $G = (V,E)$, $V = \{v_{ij}, \enspace i = 1, \dots , k \enspace j = 1,2,3\}$ And the edge set being the edges that form triangles for $v_{ij}$ for every $j = 1, \dots ,k$ in addition to edges connecting "conflicts" being when the negation of $x_{i}$ being in another component

For example
![[Pasted image 20240422172827.png]]

We set the target for the dec vertex cover to be $t = 2 * k$.
The reduction of 3SAT to dec vertex cover constructed above will output the answer for the obtained dec vertex cover as the answer of the original 3SAT instance
##### Proof
Let us claim that the original 3-SAT instance is satisfiable if and only if the graph $G$ we have constructed has an independent set of size at least $k$. 

First, if the 3SAT instance is satisfiable, then each triangle in our graph contains at least one node whose label evaluates to 1. Let $S$ be a set consisting of one such node from each triangle. We claim $S$ is independent; for if there were an edge between two nodes $u, s \in S$, then the labels of $u$ and $v$ would have to conflict; but this is not possible, since they both evaluate to 1.

Conversely, suppose our graph $G$ has an independent set $S$ of size at least $k$. Then, first of all, the size of $S$ is exactly $k$, and it must consist of one node from each triangle. Now, we claim that there is a truth assignment $v$ for the variables in the 3SAT instance with the property that the labels of all nodes in $S$ evaluate to 1. Here is how we could construct such an assignment $v$. For each variable $x_i$, if neither $x_i$ or $\overline{x_i}$ appears as a label of a node in $S$, then we arbitrarily set $v(x_{i})= 1$. Otherwise, exactly one of $x_{i}$ or $\overline{x_i}$ appears as a label of a node in $S$; for if one node in $S$ were labeled $x_i$ and another were labeled $\overline{x_i}$, then there would be an edge between these two nodes, contradicting our assumption that $S$ is an independent set. Thus, if $x_i$ appears as a label of a node in $S$, we set $v(x_{i}) = 1$, and otherwise we set $v(x_{i)}= 0$. By constructing $v$ in this way, all labels of nodes in $S$ will evaluate to 1.

Since $G$ has an independent set of size at least $k$ if and only if the original 3SAT instance is satisfiable, the reduction is complete.