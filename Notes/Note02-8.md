# Exploiting Tri-Relationship for Fake News Detection

> Kai Shu, Suhang Wang and Huan Liu
> https://arxiv.org/abs/1712.07709v1

# Abstract  
难点：  
（1）如何建立三元关系的数学模型来提取新闻中的特征表达  
（2）如何利用三元特征的学习来进行谣言检测  
主要贡献：  
（1）提出一个可行的方法建立发布者、新闻、用户参与这三个因素的三元关系模型  
（2）提出一个全新的架构TriFN，利用三元关系来进行谣言检测  
（3）在新构建的真实数据集上进行大量实验，以评估TriFN谣言检测的有效性  

# Overview
## Model Name 
  Tri-Relationship Fake News detection framework (TriFN)
## Motivation
  早前的谣言检测主要集中于对文本的分类和包含的事实进行检测，但是根据心理学上的确认偏误效应和回音室效应，用户产生的不同行为也能辅助文本进行谣言的检测。
  所以作者提出了一个“三元关系谣言检测架构”TriFN，利用发布者、新闻、社交传播参与者这三者之间的潜在联系作为额外的资料来源辅助进行谣言检测。  
  ![Note02-8](/Img/Note02-8-1.bmp)  
  这样做的依据是：  
  （1）拥有不同立场和思想倾向的人会偏向对某一类消息进行回复  
  （2）可信度低的用户更易受谣言的干扰，更倾向于传播谣言，并形成相似的立场    
## Structure


# Brief Comment
1. 文章在判断用户参与的时候着重注意了表达赞同的用户，并且在这部分的数据上只使用了直接发布推文的用户和未评论
只进行简单转发的用户，并认为这部分用户都是表示赞成。这点和以前做过的数据处理有些不同，有的任务着重于文本内容的分析
将只转发不评论的用户的特征略去（？）
2. 
