Given clients $D$ and facilities $F$, facility costs $f_{i}, i \in F$ and assignment costs $c_{ij}$, $i \in F$, $j \in D$. Select a subset of facilities to open and an assignment of clients to facilities such that the total cost is minimized. (Any client can be assigned to any facility)
### 3-approximation algorithm
#### Pseudocode
Step 1:
- $v \leftarrow 0$
- $w \leftarrow 0$
- $T \leftarrow \emptyset$
- $S \leftarrow \mathcal{D}$
Step 2
- while $S \neq \emptyset$
	- increase $v_j$ for all $j \in S$ and $w_{ij}$ for all $i \in N(j)$ uniformly until some $j \in S$ neighbours some $i \in T$ or some $i \not \in T$ has a tight dual constraint
	- if for some $j \in S$ we have that $j$ now neighbours $i \in T$
		- then $S \leftarrow S - \{j\}$
	- if for some $i \not \in T$ we have that $\sum\limits_{j \in \mathcal{D}}w_{ij} = f_{i}$
		- then $T \leftarrow T \cup \{i\}$
		- $S \leftarrow S  - N(i)$
Step 3
- $T' \leftarrow \emptyset$
- while $T \neq \emptyset$
	- Pick $i \in T$; $T' \leftarrow T' \cup \{i\}$
	- $T \leftarrow T - \{ h \in T: \exists j \in \mathcal{D}, w_{ij} > 0, w_{hj}> 0    \}$ 
Output $T'$ as the set of facilities to open

