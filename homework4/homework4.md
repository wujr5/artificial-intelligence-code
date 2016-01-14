# 人工智能 Homework4

## 1 题目

**14.6**
![](http://ww2.sinaimg.cn/large/ed796d65gw1eyznrqz8nyj21kw0ra48e.jpg)
![](http://ww4.sinaimg.cn/large/ed796d65gw1eyzodup2poj21kw0nidoc.jpg)

a. （c）图

b. (a) 和 (b)

c. (a) 最好。

d. 根据题意得到：
```cpp
G(mother)   G(father)   P(Gchild =l|...)	P(Gchild = r|...)
l 			l 			1 − m 				m
l 			r 			0.5 				0.5
r 			l 			0.5 				0.5
r 			r 			m 				  1 − m
```

e. 
$$
P(G_{child} = l) 
= \sum_{g_m,g_f}P(G_{child} 
= l|g_m,g_f)P(g_m,g_f)
= \sum_{g_m,g_f}P(G_{child} = l|g_m,g_f)P(g_m)P(g_f)
= (1 − m)q^2 + 0.5q(1 − q) + 0.5(1 − q)q + m(1 − q)^2
= q^2 − mq^2 + q − q^2 + m − 2mq + mq^2
= q + m − 2mq
$$

f. 遗传平衡意味着，
$$P(G_{child} = l)$$
必须等于
$$P(G_{mother} = l) 和 P(G_{father} = l)$$
例如
$$q + m − 2mq = q, hence q = 0.5$$
但是，少数人是左撇子，所以，继承或表现的对称模型就发生了问题。

**14.14**
![](http://ww3.sinaimg.cn/large/ed796d65gw1eyzoeczjbej21kw1elh4c.jpg)

a. (ii) 和 (iii)

b. 
$$P(b,i, ¬m,g,j)= P(b)P(¬m)P(i|b, ¬m)P(g|b,i, ¬m)P(j|g) = .9 × .9 × .5 × .8 × .9 = .2916$$

c. 
$$
P(J|b,i,m) = α Pg P(J,g) = α[P(J,g) + P(J, ¬g)]
= α[hP(j,g),P(¬j,g)i + hP(j, ¬g),P(¬j, ¬g)i
= α[(.81,.09) + (0,0.1)] = (.81,.19)
$$

所以，进监狱的概率为0.81

d. 如果不控诉，一个人不能被判有罪，无论他们是否触犯了法律，或者被公诉。这就是CPT的意义，所以G对B和M是上下文独立的，对于给定的I = false。

**14.15**
![](http://ww2.sinaimg.cn/large/ed796d65gw1eyzoeq93avj21kw0nkn7u.jpg)

This question definitely helps students get a solid feel for variable elimination. Students may need some help with the last part if they are to do it properly.
a.
![](http://ww4.sinaimg.cn/large/ed796d65gw1ezzf9hv3edj20kq0cxjud.jpg)

e
P(e) ..598525 59223 ..183055 0011295 
= αP(B).002 ×  ..598525 183055  + .998 ×  ..59223 0011295 
= α  ..001 999  ×  ..59224259 001493351 
= α  ..00059224259 0014918576 
≈ h.284,.716i
b. Including the normalization step, there are 7 additions, 16 multiplications, and 2 divisions. The enumeration algorithm has two extra multiplications.

c. To compute P(X1|Xn = true) using enumeration, we have to evaluate two complete
binary trees (one for each value of X1), each of depth n −2, so the total work is O(2n).
Using variable elimination, the factors never grow beyond two variables. For example,
the first step is
P(X1|Xn = true)
= αP(X1)... X
xn−2
P(xn−2|xn−3) X
xn−1
P(xn−1|xn−2)P(Xn = true|xn−1)
= αP(X1)... X
xn−2
P(xn−2|xn−3) X
xn−1
fX
n−1(xn−1,xn−2)fXn(xn−1)
= αP(X1)... X
xn−2
P(xn−2|xn−3)fX
n−1Xn(xn−2)
The last line is isomorphic to the problem with n − 1 variables instead of n; the work
done on the first step is a constant independent of n, hence (by induction on n, if you
want to be formal) the total work is O(n).

d. Here we can perform an induction on the number of nodes in the polytree. The base
case is trivial. For the inductive hypothesis, assume that any polytree with n nodes can
be evaluated in time proportional to the size of the polytree (i.e., the sum of the CPT
sizes). Now, consider a polytree with n + 1 nodes. Any node ordering consistent with
the topology will eliminate first some leaf node from this polytree. To eliminate any
135
leaf node, we have to do work proportional to the size of its CPT. Then, because the
network is a polytree, we are left with independent subproblems, one for each parent.
Each subproblem takes total work proportional to the sum of its CPT sizes, so the total
work for n + 1 nodes is proportional to the sum of CPT sizes.

**14.18**
![](http://ww3.sinaimg.cn/large/ed796d65gw1eyzof6y9qdj21kw0j07as.jpg)

a. 
There are two uninstantiated Boolean variables (Cloudy and Rain) and therefore four
possible states.

b. 
First, we compute the sampling distribution for each variable, conditioned on its Markov
blanket.
P(C|r,s) = αP(C)P(s|C)P(r|C)
= αh0.5, 0.5ih0.1, 0.5ih0.8, 0.2i = αh0.04, 0.05i = h4/9, 5/9i
P(C|¬r,s) = αP(C)P(s|C)P(¬r|C)
= αh0.5, 0.5ih0.1, 0.5ih0.2, 0.8i = αh0.01, 0.20i = h1/21, 20/21i
P(R|c,s,w) = αP(R|c)P(w|s,R)
= αh0.8, 0.2ih0.99, 0.90i = αh0.792, 0.180i = h22/27, 5/27i
P(R|¬c,s,w) = αP(R|¬c)P(w|s,R)
= αh0.2, 0.8ih0.99, 0.90i = αh0.198, 0.720i = h11/51, 40/51i
Strictly speaking, the transition matrix is only well-defined for the variant of MCMC in
which the variable to be sampled is chosen randomly. (In the variant where the variables
are chosen in a fixed order, the transition probabilities depend on where we are in the
ordering.) Now consider the transition matrix.

• Entries on the diagonal correspond to self-loops. Such transitions can occur by
sampling either variable. For example,
q((c,r) → (c,r)) = 0.5P(c|r,s) + 0.5P(r|c,s,w) = 17/27
• Entries where one variable is changed must sample that variable. For example,
q((c,r) → (c,¬r)) = 0.5P(¬r|c,s,w) = 5/54
• Entries where both variables change cannot occur. For example,
q((c,r) → (¬c,¬r)) = 0
his gives us the following transition matrix, where the transition is from the state given
y the row label to the state given by the column label:
(c,r)
(c,¬r)
(¬c,r)
(¬c,¬r)
(c,r) (c,¬r) (¬c,r) (¬c,¬r)

17/27 5/54 5/18 0
11/27 22/189 0 10/21
2/9 0 59/153 20/51
0 1/42 11/102 310/357

Q2 represents the probability of going from each state to each state in two steps.
Qn (as n → ∞) represents the long-term probability of being in each state starting in
ach state; for ergodic Q these probabilities are independent of the starting state, so
very row of Q is the same and represents the posterior distribution over states given
he evidence.
We can produce very large powers of Q with very few matrix multiplications. For
xample, we can get Q2 with one multiplication, Q4 with two, and Q2k with k. Unfor
unately, in a network with n Boolean variables, the matrix is of size 2n ×2n, so each
multiplication takes O(23n) operations.
