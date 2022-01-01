# DeepWalk  
DeepWalk借用了Word2Vec的skip-gram模型，通过最大化节点之间的共现概率来学习出节点的Embedding表示。而对于节点之间的共现关系，该算法使用的是Random Walk在网络中进行采样得到的节点序列来进行描述。Random Walk是一种类似于深度优先遍历（DFS）的方法，但与DFS不同的是，Random Walk可重复访问已访问过的节点。  
![DFS和BFS](https://user-images.githubusercontent.com/50071592/147851933-78d937a2-a22d-4e64-930b-aaca6b6c4cbd.png)

