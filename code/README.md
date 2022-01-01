# DeepWalk 
---
DeepWalk借用了![Word2Vec](https://zh.wikipedia.org/wiki/Word2vec)的![skip-gram](https://zhuanlan.zhihu.com/p/27234078)模型，通过最大化节点之间的共现概率来学习出节点的***Embedding***表示。而对于节点之间的共现关系，该算法使用的是Random Walk在网络中进行采样得到的节点序列来进行描述。Random Walk是一种类似于深度优先遍历（DFS）的方法，但与DFS不同的是，Random Walk可重复访问已访问过的节点。  
Random Walk算法首先需要预设一个随机游走的步长作为节点序列的长度，从起始节点开始，从当前节点的邻居节点中随机选取一个节点作为下一个将要访问的节点直至达到预设的步长，得到的节点序列便可视为是一种特殊的句子，将其输入到skip-gram模型中便可训练出节点的Embedding表示。  
![DFS和BFS](https://user-images.githubusercontent.com/50071592/147851933-78d937a2-a22d-4e64-930b-aaca6b6c4cbd.png)  
## skip-gram模型  
