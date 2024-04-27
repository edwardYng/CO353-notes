Similar to the UFL problem, we are given an input of clients $D$, facilities $F$ and assignments costs $c_{ij}$ for $i \in F$ and $j \in D$. However, now there are no longer any facility costs, instead we are given as an input an positive integer $k$ which is an upper bound on the number of facilities we can open. The goal is to select a subset of at most $k$ facilities to open such that the assignment costs are reduced.

#### Proof of 3-approximation
The primal of the k-median problem can be formulated as the same as the UFL problem, but with $\lambda$ facility opening costs and with an extra $- \lambda k$ constant term in the objective function. With that, we can construct a dual program similarly to the one in the UFL problem. 

Now, we consider a possible solution from the primal-dual approximation algorithm for UFl problem. We know that the algorithm produces a set of facilities to open, $S$, and a feasible solution $(v,w)$.
$$
\sum\limits_{j\in D} \min_{i\in S}c_{ij} + \sum\limits_{i \in S} f_{i} \leq 3\sum\limits_{j \in D} v_j
$$
Let $c(s) = \sum\limits_{j\in D} \min_{i\in S}c_{ij}$ and we set $f_{i}=\lambda$ to get.
$$
c(S) \leq 3\sum\limits_{j \in D}(v_{j} - \lambda |S|)
$$
Therefore, if by chance that we have $|S| = k$, then we clearly see that
$$
c(S) \leq 3\sum\limits_{j \in D}(v_{j} - \lambda k) = 3*OPT_k
$$
And therefore, we obtain a 3-approximation of the optimal value.

#### Finding $\lambda$
We want to find some $\lambda$ such that the UFL algorithm opens a set of facilities $S$ with $|S| = k$. A natural way to do this is through binary search where with $\lambda_{min} = 0$ and $lambda_{max} = \sum\limits_{j \in D} \sum\limits_{i \in F} c_{ij}$. We run the UFL approximation algorithm until we get some $\lambda$ such that $|S| = k$ to obtain a 3 approximation.

If we cannot find such $\lambda$ specifically, we have $\lambda_{max} - \lambda_{min} \leq \frac{\epsilon c_{min}}{|F|}$. We will use $S_{1}$ and $S_{2}$ to obtain a solution $S$ in polynomial time such that $|S| = k$ and $c(S) \leq 2(3 + \epsilon)OPT_k$. 

Let $\alpha_{1}$ and $\alpha_2$ be such that $\alpha_{1}|S_{1}|+ \alpha_{2}|S_{2}|= k$, $\alpha_{1} + \alpha_{2} = 1$  with $\alpha_{1}, \alpha_{2} \geq 0$. Which implies
$$
\alpha_{1}= \frac{k - |S_2|}{|S_{1}| - |S_{2}|} 
\text{ and }
\alpha_{2}= \frac{k - |S_1|}{|S_{1}| - |S_{2}|}
$$
We get a dual solution $(\tilde{v}, \tilde{w})$ by letting $\tilde{v} = \alpha_{1}v^{1} + \alpha_{2}v^2$ and $\tilde{w} = \alpha_{1}w^{1} + \alpha_{2}w^2$. Note that $(\tilde{v}, \tilde{w})$ is feasible for the dual linear program with facility costs $\lambda_{max}$ since it is a convex combination of two feasible dual solutions. 