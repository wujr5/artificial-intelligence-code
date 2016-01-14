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



**8.10**
![](http://ww2.sinaimg.cn/large/ed796d65gw1ey36hvtvebj21kw0lsgtv.jpg)
![](http://ww3.sinaimg.cn/large/ed796d65gw1ey36i72wwpj21kw0cttdf.jpg)

**8.19**
![](http://ww3.sinaimg.cn/large/ed796d65gw1ey36ini48zj21kw0engq9.jpg)

**8.23**
![](http://ww2.sinaimg.cn/large/ed796d65gw1ey36j2toejj21kw0iz45j.jpg)

**8.28**
![](http://ww2.sinaimg.cn/large/ed796d65gw1ey36jgecl7j21kw0mlwmj.jpg)

**9.9**
![](http://ww3.sinaimg.cn/large/ed796d65gw1ey36ju8id2j21kw0fzn23.jpg)
![](http://ww1.sinaimg.cn/large/ed796d65gw1ey36k3p4wuj21kw0fudli.jpg)

**9.19**
![](http://ww4.sinaimg.cn/large/ed796d65gw1ey36kowe6pj21kw0x3alt.jpg)

**9.23**
![](http://ww4.sinaimg.cn/large/ed796d65gw1ey36kzh2naj21kw0cp793.jpg)

**9.24**
![](http://ww3.sinaimg.cn/large/ed796d65gw1ey36lbc0wdj21kw0t7k1j.jpg)

