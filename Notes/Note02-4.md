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
>    
> ## Motivation
> 作者提到当时的谣言检测研究领域很少有模型决策过程的可解释性方面的研究，且所运用的模型大都基于神经网络等黑箱方法，缺少对模型如何判错的研究。  
> （但事实上同年发表在ACL上的另一篇谣言检测领域的文章GCAN也在该领域进行了研究，并且也用注意力机制完成了本文作者的motivation）  
> （但与GCAN不依赖用户评论转发不同，DTCA高度依赖于用户的转发和评论，这也因多数用户仅转发不评论的特点而导致了数据的稀疏性。）  
> 
> ## Structure
> DTCA:  
> ![Note02-4-1](/Img/Note02-4 (1).bmp)   
> 
> _A. DTE_  
> ![Note02-4(2)](/Img/Note02-4 (2).bmp)    
> （1）根据评论转发之间的关系建立评论树结构  
> （2）通过决策树筛选具有高可信度的评论作为evidence，其中，可信度的依据为评论与源推文的相似度、用户特征和评论本身的质量。  
> 由于被选为evidence的评论本身是由决策树产生的，因此根据决策条件，evidence具有可解释性。  
> 
> _B. CaSa_  
> （a）Sequence Representation Layer  
> 将evidence（评论）和claim（源推文）用向量表示，作为模型输入（l是tokens长度，d是向量维度）：  
> ![Note02-4(3)](/Img/Note02-4 (3).bmp)   
> 把X分别编码为固定长度的隐层向量，并经过BiLSTM得到各自的向量表示：  
> ![Note02-4(4)](/Img/Note02-4 (4).bmp)   
> ![Note02-4(5)](/Img/Note02-4 (5).bmp)   
> 
> （b）Co-attention Layer  
> ![Note02-4(6)](/Img/Note02-4 (6).bmp)   
> （1）evidence作为Q，作用于claim部分的self-attention，挖掘评论与源推文的深层语义关系，以便获得假新闻claim中的false part。  
> （2）将由上步得到的包含评论与源推文语义关系的claim作为Q，作用于evidence部分的self-attention，以便获得用于判别的评论evidence中的细粒度关键文本。  
> ![Note02-4(7)](/Img/Note02-4 (7).bmp)     
> 其中，这两部分的self-attention均基于multi-head attention，分别经过各自的feed-forward network（FFN）得到evidence、claim的输出E、C。  
> 输出O（E、C）：  
> ![Note02-4(8)](/Img/Note02-4 (8).bmp)   
> 最后，将E、C合并为整体用于进行判别：  
> ![Note02-4(9)](/Img/Note02-4 (9).bmp)   
> 
> （c）Output Layer  
> 预测：  
> ![Note02-4(10)](/Img/Note02-4 (10).bmp)   
> 损失函数：  
> ![Note02-4(11)](/Img/Note02-4 (11).bmp)   
> 

> ## Experiment
> 实验结果：  
> ![Note02-4(12)](/Img/Note02-4 (12).bmp)   
> 通过attention权重进行可解释性举例说明：  
> ![Note02-4(13)](/Img/Note02-4 (13).bmp)   

## Brief Comment
