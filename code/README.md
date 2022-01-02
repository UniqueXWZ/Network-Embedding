# DeepWalk 
---
DeepWalk借用了`Word2Vec`的`skip-gram`模型，通过最大化节点之间的共现概率来学习出节点的***Embedding***表示。而对于节点之间的共现关系，该算法使用的是Random Walk在网络中进行采样得到的节点序列来进行描述。Random Walk是一种类似于深度优先遍历（DFS）的方法，但与DFS不同的是，Random Walk可重复访问已访问过的节点。  
Random Walk算法首先需要预设一个随机游走的步长作为节点序列的长度，从起始节点开始，从当前节点的邻居节点中随机选取一个节点作为下一个将要访问的节点直至达到预设的步长，得到的节点序列便可视为是一种特殊的句子，将其输入到skip-gram模型中便可训练出节点的***Embedding***表示。  
![image](https://user-images.githubusercontent.com/50071592/147873203-01f6c01d-dc2b-49bd-b146-0e719f8474e6.png)
## skip-gram模型  
在`nlp`中，skip-gram模型是使用中心词来预测上下文以完成对词向量的训练，即，给定一个句子![image](https://user-images.githubusercontent.com/50071592/147872355-47cd3d86-b6af-4791-a323-7048dd6cc3c1.png)，则skip-gram的目标是要最大化条件概率![image](https://user-images.githubusercontent.com/50071592/147872393-9072fefc-f4aa-4bdc-bf7b-7082a07a5d99.png)，其中w表示窗口大小。将其对应到DeepWalk算法中：首先利用Random算法采样得到一个节点序列![image](https://user-images.githubusercontent.com/50071592/147872441-5f25168e-dcd6-400c-828b-23e5e8bf0b35.png)
，则DeepWalk的目标是要最大化一个窗口内节点的共现概率![image](https://user-images.githubusercontent.com/50071592/147872424-c7448085-7dbf-48f8-ba15-c11235e43793.png)。  
  DeepWalk的目标是要学习网络中节点的潜在表示，而不仅仅是节点之间共现的概率分布，因此引入一个映射函数![image](https://user-images.githubusercontent.com/50071592/147872730-71f688ad-c98c-4793-b3c8-20f6dae39552.png)，实际上，可用隐藏层的权重矩阵来表示映射函数Φ。这样，模型的优化目标就变为![image](https://user-images.githubusercontent.com/50071592/147872881-aea453d6-6acf-4a1e-b264-dce67268886c.png)  
以下是skip-gram算法：   
![image](https://user-images.githubusercontent.com/50071592/147873304-5743b1af-c718-4cf9-b8cd-7517b7143a63.png)  
该模型与自动编码器原理很相似，当模型训练完成后，我们真正需要的并不是输出层数据，而是中间隐藏层的权重矩阵。权重矩阵的为|V|×d为的矩阵，  
![skip-gram](https://user-images.githubusercontent.com/50071592/147868922-d25d9a9d-cc2f-407e-b255-7e1607f9996f.png)
