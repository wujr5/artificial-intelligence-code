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

**3.27**  
![](http://ww2.sinaimg.cn/large/ed796d65gw1ey2yzaxjhgj21kw0b3aed.jpg)
![](http://ww3.sinaimg.cn/large/ed796d65gw1ey2ywnuzerj21kw0h7wk8.jpg)

**3.30**  
![](http://ww4.sinaimg.cn/large/ed796d65gw1ey2z28nqhgj21kw0fadlq.jpg)

**3.32**
![](http://ww3.sinaimg.cn/large/ed796d65gw1ey2z3867hqj21kw06tjtu.jpg)

## 2 分析

### 2.1 题3.19分析 

搜索程序python实现如下：

