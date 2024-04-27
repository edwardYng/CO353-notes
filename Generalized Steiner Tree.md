Given a graph $G = (V,E)$ and edge costs $c_{e} \geq 0$, $e \in E$, $k$ pairs $s_{i}, t_{i} \in V \space, i = 1, \dots , k$. Find $F \subseteq E$ such that $c(F)$ is minimized and for every $i = 1, \dots , k$ there is an $s_{i} - t_{i}$ path in $(V, F)$.

### 2-Approximation Algorithm
#### Pseudocode
Step 1.
- $y \leftarrow 0$
- $F \leftarrow \emptyset$
- $t \leftarrow 0$
Step 2.
- While not all $s_it_i$ pairs are connected by $F$ do
	- $t \leftarrow t + 1$
	- let $C_{t}$ be the set of connected components $C$ of $(V, E)$ such that $|C \cap \{s_{i},t_{i}\}|= 1$ for some $i = 1, \dots , k$ 
	- increase $y_c$ for all $c \in C_t$ uniformly by $\mathcal{E}_t$ until for some $e_t$ such that $e_{t} \in \delta(C'), C' \in C$ we have $c_{e_{t}}  = \sum_{s: e_t \in \delta(S)} y_s$ 
	- $F \leftarrow F \cup \{e_t\}$
Step 3
- $F' \leftarrow F$
- for $k \leftarrow t$ to 1 do
	- if $F' - \{e_{k}\}$ is a feasible solution then
		- $F' \leftarrow F' - \{e_{k}\}$
Output $F'$ 
#### Lemma
For every iteration $t$ we have $\sum_{c \in C_{t}}|\delta(c) \cap F'| \leq 2*|C_t|$ where $F'$ is the output
##### Proof
Let us consider an iteration at which $e_{i}$ was added to $F$. Let $F_i$ be the edges included in $F$ before $e_i$, i.e $F_{i} = \{e_{1}, \dots , e_{i-1}\}$.

Let $H = F' - F_{i}$ 
#### Proof of 2-approximation
The proof relies on the lemma above.
$$
\begin{align*}
c(F') &= \sum_{c\in F'}c_{e} \\
&= \sum_{e \in F'} \sum_{S: e \in \delta(S)}y_{s} \\
&= \sum_{S}y_{s}|F' \cap \delta(S)|\\
&= \sum\limits_{S}\sum\limits_{t: S \in C_t}\mathcal{E}_{t}|F'\cap \delta(S)|\\
&\leq \sum\limits_{t}2\mathcal{E}_{t}|C_{t}|\\
&= 2\sum\limits \mathcal{E}_t|C_t|\\
&= 2\sum\limits_{S}y_s\\
&\leq 2*OPT
\end{align*}
$$
Therefore, $c(F')$ is a 2-approximation of the true optimal value.