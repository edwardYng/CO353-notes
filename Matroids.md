### Definition
A matroid is an ordered pair $M = (S, l)$ satisfying the following conditions.
1) $S$ is a finite non-empty set
2) $l$ is a non-empty family of subsets of $S$, called the independent subsets of $S$, such that if $B \in l$ and $A \subseteq B$. We say that $l$ is hereditary if it satisfies this property. Note that the empty set $\emptyset$ is a member of $l$. 
3) If $A \in l$, $B \in l$, $|A| < |B|$, there there is some $x \in B - A$ such that $A \cup \{x\} \in l$. We say that $M$ satisfies the exchange property.
### Graphic Matroid
The graphic matroid $M_G = (S_G, l_G)$ defined in terms of a given undirected graph $G = (V,E)$ as follows.
- The set $S_G$ is defined to be $E$, the set of edges of $G$
- If $A$ is a subset of $E$, then $A \in l_G$ if and only if $A$ is acyclic. That is, a set of edges $A$ is independent if and only if the subgraph $G_A = (V, A)$ forms a forest.
The graphic matroid $M_G$ is closely related to the minimum-spanning-tree problem.
#### Proof
Clearly $S_G = E$ is a finite set. Furthermore, $l_G$ is hereditary, since a subset of a forest is a forest as removing an edge cannot create cycles.

Now we show that $M_g$ satisfies the exchange property. Suppose that $G_A = (V, A)$ and $G_B = (V, B)$ and that $|B| > |A|$. Since $G_B$ contains fewer trees than $G_A$ forest $G_B$ must contain some tree $T$ whose vertices are in two different trees in $G_A$. Moreover, since $T$ is connected, it must contain an edge $(u,v)$ such that vertices $u$ and $v$ are in different trees in forest $G_A$. The edge $(u,v)$ can be added to $G_A$ without creating a cycle (since $(u,v)$ does not create a cycle in $G_B$ which is by definition acyclic). Therefore, $M_G$ satisfies the exchange property, and thus $M_G$ is a matroid.


### Maximum Independent Sets of a Matroid
#### Definiton
Given some $M = (S, l)$. we say that $A \in l$ is maximal if it has no extensions. Where an extension is an element $x \not \in A$ such that $A \cup \{x\} \in l$. 
#### Theorem
All maximal independent subsets in a matroid have the same size. 
#### Proof
Prove by contradiction
Suppose to the contrary that $A$ is a maximal independent subset of $M$ and there exists another larger maximal independent $B$ of $M$. Then, the exchange property implies that $A$ is extendible to a larger independent set $A \cup \{x\}$ for some $x \in B - A$, contradicting the assumption that $A$ is maximal.
### Greedy Algorithm on Weighted Matroids

#### Pseudocode
Input: Matroid $M$, Weights $w$.
Step 1:
- $A \leftarrow \emptyset$
- sort $e \in S$ in decreasing weight
- $k \leftarrow 1$
Step 2
- While $k \neq n$
	- $k \leftarrow k + 1$
	- If $A \cup \{e_k\} \in l$
		- $A \leftarrow A \cup \{e_k\}$
#### Proof of correctness
