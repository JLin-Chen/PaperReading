# GCAN: Graph-aware Co-Attention Networks for Explainable Fake News Detection on Social Media

> Yi-Ju Lu, Cheng-Te Li  
> ACL 2020  
> https://arxiv.org/abs/2004.11648  

## Abstract
该论文提出的GCAN模型，是基于短文本源推文、转发用户序列和用户资料，在不使用用户评论和不使用社交网络和传播网络的情况下，通过图和协同注意力机制来实现假新闻二分类问题.
# Overview
> ## Model Name
> GCAN
> ## Motivation
> 1.谣言检测方面,为了更好地学习到词和句子,常要求使用长文本以获得较好的效果,而网络中的推文却多数是短文本的形式.  
> 2.且目前SOTA的方法要求有大量用户评论辅助验证,而绝大多数用户仅转发不评论.  
> 3.大多数模型缺乏可解释性,不能很好地提供机器进行判断的证据。  
> 
> 为了解决上述问题,作者提出GCAN模型.  
> 该模型从用户资料和社交互动中提取用户特征，使用CNN和GRU分别学习基于用户特征的传播表示，用GCN来通过图建模学习用户之间的可能潜在交互，
> 提出dual co-attention机制来分别学习源推文S与用户传播C以及源推文S与用户交互G之间的相关性，最后利用学习到的embedding进行预测。  
> 
> 且在可解释性方面,该模型能够指出可疑转发者并突出机器在进行判断时特别关注的源推文的词。
> ## Structure
> ![Note02-3-1](/Img/Note02-3-1.bmp)  
> ## Method
> _A. User Characteristics Extraction_  
> ![Note02-3-2](/Img/Note02-3-2.bmp)  
> 首先，先通过定义来量化得到用户的特征向量。特征包含：  
> ①用户自我描述的字数；
>②用户账户名的字数；
>③关注用户的数量；
>④用户关注的人的数量；
>⑤用户创建的story数量；
>⑥举例用户第一个story经过的时间；
>⑦用户的账户是否被验证过；
>⑧用户是否允许地理空间定位；
>⑨源推文发布时间和用户转发时间的时差；
>⑩用户和源推文之间转发路径的长度（如果用户转发源推文则为1）。  
 >![Note02-3-3](/Img/Note02-3-3.bmp)  
 >
 > _B. Source Tweet Encoding_   
 >首先对源推文进行one-hot编码，其中e是词的one-hot向量：  
 > ![Note02-3-4](/Img/Note02-3-4.bmp)   
 > 然后，利用全连接网络得到word-embedding，其中d是embedding的维度：  
 > ![Note02-3-5](/Img/Note02-3-5.bmp)   
 >![Note02-3-6](/Img/Note02-3-6.bmp)  
 > 最后，利用GRU学习词的序列表示，得到源推文的embedding：  
 > ![Note02-3-7](/Img/Note02-3-7.bmp)   
 > ![Note02-3-8](/Img/Note02-3-8.bmp)  
 > 
 > _C. User Propagation Representation_  
 > 推文s的转发用户特征向量序列：  
 > ![Note02-3-9](/Img/Note02-3-9.bmp)  
 > 若转发用户数量超过n，则截取n个；若少于n，则从PF中重采样直至n。  (感觉如果重采样次数多的话应该会对结果的正确性产生一定的影响)  
 > _(a)CNN-based Representation_  
 > 学习用户特征之间的相关性，最终学习到用户特征的表示序列：  
 > ![Note02-3-10](/Img/Note02-3-10.bmp)  
 > 共使用d个卷积核。  
 > _(b)GRU-based Representation_  
 > 学习用户传播之间的相关性，  
 > ![Note02-3-11](/Img/Note02-3-11.bmp)  
 > 通过平均池化pooling得到最终的输出：  
 > ![Note02-3-12](/Img/Note02-3-12.bmp)
 > ![Note02-3-13](/Img/Note02-3-13.bmp)  
 > 
 > _D. Graph-aware Interaction Representation_  
 > 通过创建图来建模转发用户之间潜在的交互：每个源推文的转发用户集U都被用来创建一个图，由于不清楚用户之间的真实交互，故图采用全连接的方式，每条边都被关联到一个权重w。  
 > 其中，权重w由用户特征向量之间的余弦相似度得出：  
 > ![Note02-3-14](/Img/Note02-3-14.bmp)  
 > 得到的权重矩阵W将在D中使用。  
 > 图的邻接矩阵：  
 > ![Note02-3-15](/Img/Note02-3-15.bmp)  
 > ![Note02-3-16](/Img/Note02-3-16.bmp)  
 > 
 > _E. Dual Co-attention Mechanism_  
 > 考察源推文与用户传播及用户交互之间的相互作用，通过attention机制使得模型具有可解释性。  
 > _(a)Source-Propagation Co-attention_  
 > 源推文S与用户交互G，  
 > 计算相似性矩阵：  
 > ![Note02-3-17](/Img/Note02-3-17.bmp)  
 > 然后得到：  
 > ![Note02-3-18](/Img/Note02-3-18.bmp)  
 > 计算attention权重：  
 > ![Note02-3-19](/Img/Note02-3-19.bmp)  
 > 得到源推文和用户交互G的attention向量：  
 > ![Note02-3-20](/Img/Note02-3-20.bmp)  
 > 其中s和g用于描述，源推文中的单词是如何被用户参与互动的。  
 > _(b)Source-Interaction Co-attention_  
 > 源推文S与用户传播C：按照上述类似过程得到S和C的attention向量。  
 > 
 > _F. Make Prediction_  
 > ![Note02-3-21](/Img/Note02-3-21.bmp)  
 > 
> ## Experiment

## Brief Comment
