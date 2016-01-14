# 人工智能 Homework3

## 1 题目

**7.1**
![](http://ww3.sinaimg.cn/large/ed796d65gw1ey36cpwqooj21kw0irjy3.jpg)

根据题目意思，可以得到一个状态表格。

![](http://ww1.sinaimg.cn/large/ed796d65gw1ezz7sf8lxsj20n00oatcm.jpg)

可以看到KB |= α2，因为每一行KB = true的同时α2 = true；
同理，α3也是一样。

**7.14**
![](http://ww3.sinaimg.cn/large/ed796d65gw1ey36d49p30j21kw0fkq8k.jpg)

a.

(i) 
$$ (R ∧ E) ⇐⇒ C$$

错误。当选总统的不一定是保守的。

(ii) 
$$R ⇒ (E ⇐⇒ C)$$

正确。因为一个激进的人，如果他是总统，那么他是保守的。根据题目意思可以知道，这是正确的。

(iii)
$$R ⇒ ((C ⇒ E) ∨ ¬E)$$

错误。这其实等价于：
$$¬R ∨ ¬C ∨ E ∨ ¬E$$
是重言的。

**7.18**
![](http://ww4.sinaimg.cn/large/ed796d65gw1ey36dh9bqkj21kw0cedk6.jpg)

a. 枚举的表格如下所示：

表格数据说明了，对于所有情况表达式都是true的，因此是有效的。

b. 在左边可以得到:
$$(Food ⇒ Party) ∨ (Drinks ⇒ Party)$$
$$(¬Food ∨ Party) ∨ (¬Drinks ∨ Party)$$
$$(¬Food ∨ Party ∨ ¬Drinks ∨ Party)$$
$$(¬Food ∨ ¬Drinks ∨ Party)$$

在右边可以得到：
$$(Food ∧ Drinks) ⇒ Party$$
$$¬(Food ∧ Drinks) ∨ Party$$
$$(¬Food ∨ ¬Drinks) ∨ Party$$
$$(¬Food ∨ ¬Drinks ∨ Party)$$

根据以上两边的结果可以得到：
$$P ⇒ P $$

可以证明（a）是有效的。

c. 为了证明一个句子是有效的，那么证明它的否定是无效的即可。

根据题意可以得到：

$$¬[[(Food ⇒ Party) ∨ (Drinks ⇒ Party)] ⇒ [(Food ∧ Drinks) ⇒ Party]]
[(Food ⇒ Party) ∨ (Drinks ⇒ Party)] ∧ ¬[(Food ∧ Drinks) ⇒ Party]
(¬Food ∨ ¬Drinks ∨ Party) ∧ Food ∧ Drinks ∧ ¬Party$$

每三个子句抵消第一个句子，最后句子为空。

**8.6**
![](http://ww4.sinaimg.cn/large/ed796d65gw1ey36dvwazgj21kw0cagpd.jpg)

a. 
$$(∃x\ x= x) ⇒ (∀ y ∃z\ y = z)$$
有效。LHS是有效的，每一个模型都有至少有一个对象。因此，整个句子都是有效的，当且仅当，RHS是有效的。RHS是有效的因为对Y的每一个值，都有一个唯一的对应值。

b. 
$$∀ x P(x) ∨ ¬P(x)$$
有效.对任何P关系，每一个X对象要么在关系中，要么不在。

c. 
$$∀ x Smart(x) ∨ (x = x)$$
有效。在每一个模型中，每一个对象都有满足：
$$x = x$$
所以，不管Smart(x)是否为真，整个句子都是正确的。

**8.10**
![](http://ww2.sinaimg.cn/large/ed796d65gw1ey36hvtvebj21kw0lsgtv.jpg)
![](http://ww3.sinaimg.cn/large/ed796d65gw1ey36i72wwpj21kw0cttdf.jpg)

a. 
$$O(E,S) ∨ O(E,L)$$
b. 
$$O(J,A) ∧ ∃ p p 6= A ∧ O(J,p)$$
c. 
$$∀ p O(p,S) ⇒ O(p,D)$$
d. 
$$¬∃ p C(J,p) ∧ O(p,L)$$
e. 
$$∃ p B(p,E) ∧ O(p,L)$$
f.
$$∃ p O(p,L) ∧ ∀ q C(q,p) ⇒ O(q,D)$$
g. 
$$∀ p O(p,S) ⇒ ∃ q O(q,L) ∧ C(p,q)$$

**8.19**
![](http://ww3.sinaimg.cn/large/ed796d65gw1ey36ini48zj21kw0engq9.jpg)

a. 
$$∃ x Parent(Joan,x) ∧ Female(x)$$
b. 
$$∃1x Parent(Joan,x) ∧ Female(x)$$
c. 
$$∃ x Parent(Joan,x) ∧ Female(x) ∧ [∀ y Parent(Joan,y) ⇒ y = x]$$
d. 
$$∃1c Parent(Joan,c) ∧ Parent(Kevin,c)$$
e.
$$∃ c Parent(Joan,c) ∧ Parent(Kevin,c) ∧ ∀ d,p [Parent(Joan,d) ∧ Parent(p,d)]⇒ [p = Joan ∨ p = Kevin]$$

**8.23**
![](http://ww2.sinaimg.cn/large/ed796d65gw1ey36j2toejj21kw0iz45j.jpg)

a. “No two people have the same social security number.”

$$¬∃ x,y,n Person(x) ∧ Person(y) ⇒ [HasSS\#(x,n) ∧ HasSS\#(y,n)]$$

一阶逻辑错误。没有限制x != y。
改正：

$$¬∃ x,y,n Person(x) ∧ Person(y) ∧ ¬(x = y) ∧ [HasSS\#(x,n) ∧ HasSS\#(y,n)]$$

b. 
“John’s social security number is the same as Mary’s.”

$$∃ n HasSS\#(John,n) ∧ HasSS\#(Mary,n)$$

正确。

c. “Everyone’s social security number has nine digits.”

$$∀ x,n Person(x) ⇒ [HasSS\#(x,n) ∧ Digits(n,9)]$$

缺少
$$HasSS\#(x,n)$$
改正：
$$∀ x,n Person(x) ∧ HasSS\#(x,n) ⇒ Digits(n,9)$$

d. 
$$SS\#(x)$$
表示x的社会安全号，使用这个函数来确保每个人只有一个社会安全号。
重写如下：

$$¬∃ x,y Person(x) ∧ Person(y) ⇒ [SS\#(x) = SS\#(y)]$$
$$SS\#(John) = SS\#(Mary)$$
$$∀ x Person(x) ⇒ Digits(SS\#(x),9)$$

**8.28**
![](http://ww2.sinaimg.cn/large/ed796d65gw1ey36jgecl7j21kw0mlwmj.jpg)

a. 
$$W(G,T)$$
b. 
$$¬W(G,E)$$
c. 
$$W(G,T) ∨ W(M,T)$$
d. 
$$∃ s W(J,s)$$
e. 
$$∃ x C(x,R) ∧ O(J,x)$$
f.
$$∀ s S(M,s,R) ⇒ W(M,s)$$
g. 
$$¬[∃ s W(G,s) ∧ ∃ p S(p,s,R)]$$
h. 
$$∀ s W(G,s) ⇒ ∃ p,a S(p,s,a)$$
i. 
$$∃ a ∀ s W(J,s) ⇒ ∃ p S(p,s,a)$$
j. 
$$∃ d,a,s C(d,a) ∧ O(J,d) ∧ S(B,T,a)$$
k. 
$$∀ a [∃ s S(M,s,a)] ⇒ ∃ d C(d,a) ∧ O(J,d)$$
l. 
$$∀ a [∀ s,p S(p,s,a) ⇒ S(B,s,a)] ⇒ ∃ d C(d,a) ∧ O(J,d)$$

**9.9**
![](http://ww3.sinaimg.cn/large/ed796d65gw1ey36ju8id2j21kw0fzn23.jpg)
![](http://ww1.sinaimg.cn/large/ed796d65gw1ey36k3p4wuj21kw0fudli.jpg)

a. 
```cpp
Goal G0: 7 ≤ 3 + 9 		 Resolve with (8) {x1/7,z1/3 + 9}.
Goal G1: 7 ≤ y1 			Resolve with (4) {x2/7,y1/7 + 0}. Succeeds.
Goal G2: 7 + 0 ≤ 3 + 9. 	Resolve with (8) {x3/7 + 0,z3/3 + 9}
Goal G3: 7 + 0 ≤ y3 		Resolve with (6) {x4/7,y4/0,y3/0 + 7} Succeeds.
Goal G4: 0 + 7 ≤ 3 + 9 	 Resolve with (7) {w5/0,x5/7,y5/3,z5/9}.
Goal G5: 0 ≤ 3. 			Resolve with (1). Succeeds.
Goal G6: 7 ≤ 9. 			Resolve with (2). Succeeds.
G4 succeeds
G2 succeeds.
G0 succeeds.
```

b. 
从`(1),(2), (7) {w/0,x/7,y/3,z/9}` 推断出
```cpp
(9) 0 + 7 ≤ 3 + 9
```

从`(9), (6), (8) {x1/0,y1/7,x2/0 + 7,y2/7 + 0,z2/3 + 9}` 推断出
```cpp
(10) 7 + 0 ≤ 3 + 9
```

从`(4), (10), (8) {x3/7,x4/7,y4/7 + 0,z4/3 + 9} `推断出
```cpp
(11) 7 ≤ 3 + 9
```

**9.19**
![](http://ww4.sinaimg.cn/large/ed796d65gw1ey36kowe6pj21kw0x3alt.jpg)

a. 前向推导得到：

(i) 
$$Ancestor(Mother(y),John)$$
能： {y/John} 

(ii) 
$$Ancestor(Mother(Mother(y)),John)$$
能：{y/John}

(iii) 
$$Ancestor(Mother(Mother(Mother(y))),Mother(y))$$
能: {}
(iv) 
$$Ancestor(Mother(John),Mother(Mother(John)))$$

不能。

b. 尽管解决方案是完整的，但是并不能证明题目要求的结论。公理中没有排除所有的对象成为所有对象的祖先的可能性。

c. 答案也是一样的。

**9.23**
![](http://ww4.sinaimg.cn/large/ed796d65gw1ey36kzh2naj21kw0cp793.jpg)



**9.24**
![](http://ww3.sinaimg.cn/large/ed796d65gw1ey36lbc0wdj21kw0t7k1j.jpg)



