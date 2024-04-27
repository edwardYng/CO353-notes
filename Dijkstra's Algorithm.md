Dijkstra's Algorithm is a used to find a the shortest path starting from some distinguished node, $s$ in a connected graph.

## Pseudocode
Input: directed graph $G = (V, E)$, distinguished vertex $s \in V$ and edge lengths $L_e \geq 0, e \in E$ 
- Step 1:
	- $A \leftarrow \{s\}$
	- $d(s) \leftarrow 0$
	- $d'(v) \leftarrow +\infty$ 
- Step 2:
	- While $A \neq V$ do
		- $d'(v) \leftarrow min\{d'(v), min\{d(u) + l_{(u,v)}\}\}$
			- for all $v\in V \backslash A$ 
		- $w \leftarrow argmin\{d'(v)\}$ 
			- for all $v\in V \backslash A$ 
		- $d(w) \leftarrow d'(w)$
		- $A \leftarrow A \cup \{w\}$
Output $d(v)$ for $v \in V$

## Proof of correctness
Proof of correctness
Proof by Induction of the size of $S$
- Base Case:
	- $|S| = 1$
		- $S = \{s\}$ and $d(s) = 0$
- Suppose the claim holds when $|S| = k$; we now grow $S$ to size $k+1$ bu adding the node $v$. Let $(u,v)$ be the final edge on our $s-v$ path $P_v$
	- By induction hypothesis, $P_u$ is the shortest $s-u$ path for each $u \in S$. Now consider any other $s-v$ path $P$; we wish to show that it is at least as long as $P_v$.
	- In order to reach $v$, this path $P$ much leave the set $S$ somewhere; let $y$ be the first node on $P$ that is not in $S$, and let $x \in S$ be the node just before $y$
	- $P$ cannot be shorter than $P_v$ because it is already at least as long as $P_v$ by the time it has left the set $S$.
	- In iteration $k+1$, Dijkstra's Algorithm must have considered adding node $y$ to the set $S$ via the edge $(x,y)$ and rejected this option in favour of adding $v$. This means that there is no path from $s$ to $y$ that is shorter than the $P_v$ .

Proof Simplified:
- WLOG consider any iteration of Dijkstra's where in that iteration (call it $k$) we add some node $v$ into $A$ (i.e $v = argmin\{d'(v)\}$). Consider this path, $P_v$ from $s$ to $v$ where all the nodes in between were selected from previous iterations of Dijkstra's algorithm.
- This is the shortest path from $s$ to $v$ because all other $s-v$ paths must either 1) take another edge from a vertex in $A$ to $s$, or 2) take a vertex that is not in $A$ to $s$ 
	- 1) will result in a longer $s-v$ path because that edge was already considered in step 2.1 of Dijkstra's and was rejected in favour of $(u,v)$ .
	- 2) will result in a longer $s-v$ path because the edge connecting the vertex outside of $A$ would be considered and rejected in favour of $(u,v)$ .