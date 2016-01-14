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

a.
![](http://ww4.sinaimg.cn/large/ed796d65gw1ezzf9hv3edj20kq0cxjud.jpg)

b. 7次加法，16次乘法。枚举算法多了2次额外的乘法。

c. 
$$
P(X_1|X_n = true)
= αP(X_1)... \sum_{x_{n−2}} P(x_{n−2}|x_{n−3}) \sum_{x_{n−1}} P(x_{n−1}|x_{n−2})P(X_n = true|x_{n−1})
= αP(X_1)... \sum_{x_{n−2}} P(x_{n−2}|x_{n−3}) \sum_{x_{n−1}} f_{X_{n−1}}(x_{n−1},x_{n−2})f_{X_n(x_{n−1})}
= αP(X1)... \sum_{x_{n−2}} P(x_{n−2}|x_{n−3}) f_{X_{n−1}X_n}(x_{n−2})
$$

可以知道，复杂度为：
$$O(n)$$

**14.18**
![](http://ww3.sinaimg.cn/large/ed796d65gw1eyzof6y9qdj21kw0j07as.jpg)

a. 
4个可能的状态。

b. 
首先为每个变量计算采样分布。
![](http://ww1.sinaimg.cn/large/ed796d65gw1ezzfrexyetj20ld07vn01.jpg)

得到以下几个事实：

$$q((c,r) → (c,r)) = 0.5P(c|r,s) + 0.5P(r|c,s,w) = 17/27$$

$$q((c,r) → (c,¬r)) = 0.5P(¬r|c,s,w) = 5/54$$

$$q((c,r) → (¬c,¬r)) = 0$$

转移矩阵为：
![](http://ww4.sinaimg.cn/large/ed796d65gw1ezzft56zp5j20df049dgs.jpg)

c. Q^2^表示从两步一个状态到另外一个状态的概率。

d.  Q^n^表示从每一个状态到其他的每个个状态的概率。

e. 我们可以利用少量矩阵乘法产生A的幂值。比如，我们可以通过一次乘法得到Q^2^，两次得到Q^4^，依次类推，但是，在一个网络中有n个布尔变量，矩阵式2n*2n的大小，所以每一次乘法需要O(2^3n^)次操作。
