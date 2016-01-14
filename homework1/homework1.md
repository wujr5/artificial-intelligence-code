# 人工智能 Homework1

## 题目

**3.19**   
编写程序，输入为两个网页的URL，找出从一个网页到另一个网页的链接路径。用哪种搜索策略最适合？双向搜索适用吗？能用搜索引擎实现一个前任函数吗？

**分析**

广度优先搜索伪代码：

```cpp
search-link-maps-from-one-url-to-another-url-use-bfs(url-src, url-dist)
	url-queue: store url
	url-strings: array of urls
	path: record the path

	clear(url-queue)

	url-strings = extract-urls-from-the-page-of-url-src(url-src)
	url-queue.push(url-strings)

	while !url-queue.empty()
		one-url = url-queue.pop()
		path.add(one-url)
		if one-url is url-dist then return path

		url-strings = extract-urls-from-the-page-of-url-src(one-url)
		url-queue.push(url-strings)

	return null
```

深度优先搜索伪代码：

```cpp
search-link-maps-from-one-url-to-another-url-use-dfs(url-src, url-dist)
	url-strings: array of urls
	path: record the path

	url-strings = extract-urls-from-the-page-of-url-src(url-src)

	for one-url in url-strings
		path.add(one-url)
		if one-url is url-dist then return path
		search-link-maps-from-one-url-to-another-url-use-dfs(one-url, url-dist)

	return null
```
相对来说，深度优先搜索的效果可能会更好，能更快地找到目标url。

对搜索引擎来说，它会保持一个遍布整个web的图，其中节点是网页，中间的连线是链接。因此双向搜索是适用的。

前任函数可以是：对比两个url间的相似度。

**3.23**   
跟踪A*算法应用直线距离启发式求解从Lugoj到Bucharest问题的过程。给出节拓展的顺序和每个节点的f，g和h值。

```cpp
L[0+244=244]
M[70+241=311], T[111+329=440]
L[140+244=384], D[145+242=387], T[111+329=440]
D[145+242=387], T[111+329=440], M[210+241=451], T[251+329=580]
C[265+160=425], T[111+329=440], M[210+241=451], M[220+241=461], T[251+329=580]
T[111+329=440], M[210+241=451], M[220+241=461], P[403+100=503], T[251+329=580], R[411+193=604],
D[385+242=627]
M[210+241=451], M[220+241=461], L[222+244=466], P[403+100=503], T[251+329=580], A[229+366=595],
R[411+193=604], D[385+242=627]
M[220+241=461], L[222+244=466], P[403+100=503], L[280+244=524], D[285+242=527], T[251+329=580],
A[229+366=595], R[411+193=604], D[385+242=627]
L[222+244=466], P[403+100=503], L[280+244=524], D[285+242=527], L[290+244=534], D[295+242=537],
T[251+329=580], A[229+366=595], R[411+193=604], D[385+242=627]
P[403+100=503], L[280+244=524], D[285+242=527], M[292+241=533], L[290+244=534], D[295+242=537],
T[251+329=580], A[229+366=595], R[411+193=604], D[385+242=627], T[333+329=662]
B[504+0=504], L[280+244=524], D[285+242=527], M[292+241=533], L[290+244=534], D[295+242=537], T[251+329=580],
A[229+366=595], R[411+193=604], D[385+242=627], T[333+329=662], R[500+193=693], C[541+160=701]
```
**3.27**  
![](http://ww2.sinaimg.cn/large/ed796d65gw1ey2yzaxjhgj21kw0b3aed.jpg)
![](http://ww3.sinaimg.cn/large/ed796d65gw1ey2ywnuzerj21kw0h7wk8.jpg)

**a**

状态空间：n^2n^.

**b**

5^n^

**c**

曼哈顿距离可以作为启发式函数。|(n - i + 1) - x_i_| + |n - y_i_|.

**d**

可采纳的应该只有一个：（iii）min{h1,... ,hn}

题目需要两个观察值。

首先，设w为总的距离。可以得到：

$$w >= \sum_{i}h_i >> n * min \{h1, h2..., h_n\}$$

其次，

The explanation is nontrivial as it requires two observations. First, let the work W in a given solution be the total distance moved by all
vehicles over their joint trajectories; that is, for each vehicle, add the lengths of all the
steps taken. We have W ≥ Pi hi ≥≥ n · min{h1,...,hn}. Second, the total work we
can get done per step is ≤ n. (Note that for every car that jumps 2, another car has to
stay put (move 0), so the total work per step is bounded by n.) Hence, completing all
the work requires at least n · min{h1,...,hn}/n = min{h1,...,hn} steps.

**3.30**  
![](http://ww4.sinaimg.cn/large/ed796d65gw1ey2z28nqhgj21kw0fadlq.jpg)

This exercise reiterates a small portion of the classic work of Held and Karp (1970).
a. The TSP problem is to find a minimal (total length) path through the cities that forms
a closed loop. MST is a relaxed version of that because it asks for a minimal (total
length) graph that need not be a closed loop—it can be any fully-connected graph. As
a heuristic, MST is admissible—it is always shorter than or equal to a closed loop.
b. The straight-line distance back to the start city is a rather weak heuristic—it vastly
underestimates when there are many cities. In the later stage of a search when there are
only a few cities left it is not so bad. To say that MST dominates straight-line distance
is to say that MST always gives a higher value. This is obviously true because a MST
that includes the goal node and the current node must either be the straight line between
them, or it must include two or more lines that add up to more. (This all assumes the
triangle inequality.)
c. See "search/domains/tsp.lisp" for a start at this. The file includes a heuristic
based on connecting each unvisited city to its nearest neighbor, a close relative to the
MST approach.
d. See (Cormen et al., 1990, p.505) for an algorithm that runs in O(E log E) time, where
E is the number of edges. The code repository currently contains a somewhat less
efficient algorithm.



**3.32**
![](http://ww3.sinaimg.cn/large/ed796d65gw1ey2z3867hqj21kw06tjtu.jpg)

Students should provide results in the form of graphs and/or tables showing both runtime and number of nodes generated. (Different heuristics have different computation costs.)
Runtimes may be very small for 8-puzzles, so you may want to assign the 15-puzzle or 24-
puzzle instead. The use of pattern databases is also worth exploring experimentally.