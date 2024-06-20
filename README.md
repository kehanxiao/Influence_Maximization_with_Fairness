# Approach 
With an influence maximization problem on a graph, we defines a weighted RR-Set algorithm to achieve a effect of gap reduction while maximizing the total influence among the graph.
1) An graph $G=(V,E)$, in this algorithm is undirected. 
2) A finite set of communities $\{C_1,C_2,...,C_x\}$, such that each node in G participate in at least 1 of the communities.
   
I. Define the first weight, the Community size weight $w1$ by: Community $C_i$, define its weight as $w1_i=\frac{|C_i|}{|V|}$. 

II. For the second weight, the connectivity weight $w2$, we first apply the notion of Diversity Constraint to each of the r-hop bounded Communities $C^r_i$, such that we calculate the optimal $ki$ seeds on $C^r_i$ that gives a maximal influence on the community $C_i$ (ki $\approxeq k*w1_i$). Then, we find the maximum K-Core (or K-Truss) on $C^r_i$, such that it contains all the ki optimal seeds. Define the second weight $w2_i$ as, \textbf{foreach} community $C_i$, let its weight $w2_i=K$

III. Apply the random root selection with reverse reachable path on the graph G (similar to the RR-Set algorithm) to obtain the RR-Sets. Then, for each of the RR-Set with the root $v_r$, if $v_r$ belongs to some communities $C_{i1},C_{i2},...,C_{ih}$, we set its weights to be $w1_{vr}=min_{1 \leq j\leq h}w1_{ij}^{\alpha1}$, $w2_{vr}=min_{1 \leq j\leq h}w2_{ij}{\alpha2}$, which $\alpha1$ and $\alpha2$ are the hyper-parameters used to control the trade-off between IM and fairness, which can be defined by the user them-selves. 

IV. Finally, we do the greedy weighted set cover problem on those weighted RR-Sets with a constraint of k seeds.

# Usage

```shell
$ python3 IMP.py -i <graph file path> -k <the number of seeds> -m <IC or LT> -t <termination time> 
```
