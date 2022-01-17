# Rumor Detection on Twitter with Tree-structured Recursive Neural Networks

> Jing Ma, Wei Gao, Kam-Fai Wong  
> ACL 2018  
> https://aclanthology.org/P18-1184.pdf  

## Abstract
提出RvNN来建模学习谣言的传播结构，模型输入为源自原推文的传播树，节点为回复帖子。  
（因为考虑到被回复方是其父节点而不是根节点，所以树状结构很好地表示传播过程中不同回复与源节点之间的关系。但也正如PLAN模型中提到，该方法忽略了一个人的回复可能会基于其他人的回复而作出判断。）

# Overview
> ## Model Name
> RvNN，递归神经网络
> * Bottom-up（BU）模型
> *	Top-down（TD）模型  
在给定传播树路径和方向的情况下，通过递归有选择地优化节点特征。
> ## Motivation
> 少有基于谣言传播结构的检测方法，通过树结构进行递归特征学习，可以获得推文语义和推文之间的响应关系。
> ## Structure
> **原始RvNN:**  
> ![Note02-2-1](/Img/Note02-2-1.bmp)  
> **BU-RvNN:**  
> ![Note02-2-2](/Img/Note02-2-2.bmp)  
> ![Note02-2-3](/Img/Note02-2-3.bmp)  
> ![Note02-2-4](/Img/Note02-2-4.bmp)  
> **TD-RvNN:**  
> ![Note02-2-5](/Img/Note02-2-5.bmp)  
> ![Note02-2-6](/Img/Note02-2-6.bmp)  
> ![Note02-2-7](/Img/Note02-2-7.bmp)  
> 模型训练： 用平方损失进行训练，采用L2正则化  
> ![Note02-2-8](/Img/Note02-2-8.bmp)  
> ## Experiment
> ![Note02-2-9](/Img/Note02-2-9.bmp)  
> ![Note02-2-10](/Img/Note02-2-10.bmp)  
> ![Note02-2-11](/Img/Note02-2-11.bmp)  
> ![Note02-2-12](/Img/Note02-2-12.bmp)  

## Brief Comment
这篇文章是在PLAN之后阅读的，现在看来PLAN的最大贡献就是使用了transformer模型，总体思路和本文比较像。  

但是个人感觉PLAN的逻辑不如该文章严谨：因为该文章提出的模型基于树结构，是对不同的分支单独进行学习，不涉及不同分支之间的相互关系，子节点直接与父节点相关，这也对应了现实情况中回复者直接回复被回复者，两者直接相关。  

而PLAN模型考虑到不同推文之间的两两交互，这种思路很好，实验结果也不错，但是反应到现实情况中，并不是所有的回复者都会基于其他回复者提出的内容而发出质疑或肯定，而且在训练数据中也并不能保证不同分支的节点间建立相互关系时它们实际上也存在相互关系。
