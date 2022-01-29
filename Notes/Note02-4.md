# DTCA: Decision Tree-based Co-Attention Networks for Explainable Claim Verification

> Lianwei Wu, Yuan Rao, Yongqiang Zhao, Hao Liang, Ambreen Nazi  
> ACL 2020  
> https://www.aclweb.org/anthology/2020.acl-main.97.pdf  

## Abstract
利用谣言在传播过程中具有自证性这一特点，相关评论或转发能对源推文的真实性进行佐证，通过决策树筛选有效信息、利用注意力机制探索交互关系，以此进行谣言检测，并揭示决策过程以说明可解释性。

# Overview
> ## Model Name
> DTCA(Decision Tree-based Co-Attention Networks)：  
> 1. DTE(Decision Tree-based Evidence model)  
>    通过决策树筛选作为判别线索的信息。 
> 2. CaSa(Co-attention Self-attention networks)   
>    利用注意力机制探索源推文与相关线索之间的交互关系，寻找判错依据。  
> ## Motivation
> 作者提到当时的谣言检测研究领域很少有模型决策过程的可解释性方面的研究，且所运用的模型大都基于神经网络等黑箱方法，缺少对模型如何判错的研究。  
> （但事实上同年发表在ACL上的另一篇谣言检测领域的文章GCAN也在该领域进行了研究，并且也用注意力机制完成了本文作者的motivation）  
> （但与GCAN不依赖用户评论转发不同，DTCA高度依赖于用户的转发和评论，这也因多数用户仅转发不评论的特点而导致了数据的稀疏性。）  
> ## Structure
> 
> ## Method
> ## Experiment

## Brief Comment
