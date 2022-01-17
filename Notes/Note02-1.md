# Interpretable Rumor Detection in Microblogs by Attending to User Interactions

> Ling Min Serena Khoo, Hai Leong Chieu, Zhong Qian, Jing Jiang  
> AAAI 2020  
> https://arxiv.org/pdf/2001.10667.pdf  

## Abstract
*	模型：将RvNN树状结构改造为按推文发表的时间顺序排列的链式结构，基于transformer架构, 允许所有推文之间两两交互。  
（类似于某人发布一条质疑或肯定时不仅仅看父节点，可能会看到其他分支不同时间发表的不同推文然后做出判断。）
* 可解释性：事后解释，利用attribution（local）和by example（global）方法。
## Related Work
Rumor Detecct Approaches：
(i) the content of the claim,
(ii) the bias and social network of the source of the claim, 
(iii) fact checking with trustworthy sources (e.g., Wikipedia), 
**(iv) community response to the claims.（该论文direction）**

# Overview
> ## Model Name
> 基本：post-level attention model **(PLAN)**
> 引入结构信息： structure aware post-level attention model **(StA-PLAN）**
> 学习每篇推文更复杂表示：structure aware hierarchical token post-level attention network **(StA-HiTPLAN)**
> ## Motivation
> 以往研究采用树模型未能考虑到不同分支节点之间可能存在的交互关系，故提出此模型以充分考虑到用户交互中的信息的价值。
> ## Structure
> ![Note02-1-1](/Img/Note02-1-1.bmp)  
> StA-PLAN加入位置信息：  
> ![Note02-1-2](/Img/Note02-1-2.bmp)
> ## Experiment
> ![Note02-1-3](/Img/Note02-1-3.bmp)  
> ![Note02-1-4](/Img/Note02-1-4.bmp)  

## Brief Comment
个人认为该论文最核心的点就是改变树模型不同分支节点之间信息不能交互的状况，在序列结构中用transformer架构使得各个节点之间能建立关系，并且能保留原树结构中的位置信息进行学习。  

该文章是用expainable和rumor detect为关键词检索出来的，但是它在可解释性方面并没有很特别的思路的提出，个人感觉只是用了attribution和example方法来解释为什么能检测出谣言，没有解释到他的proposed model为什么会好（可能因为这暂时无法解释）。  

作者的实验数据仅用了community response，文中也提到其他研究者使用identity information的效果会更好。如果在此模型的基础上进行改进，给identity一定的权重，加入到输入数据中进行训练，不知道会不会取得更好的效果

