 # Dual-View Distilled BERT for Sentence Embedding

> Xingyi Cheng  
> SIGIR2021  
> https://arxiv.org/pdf/2104.08675v1.pdf  

## Abstract  
BERT在单词级cross sentence attention实现句子匹配方面取得重大进展，但使用siamese BERT推导两个句子时性能下降，且由于两句子间无单词级的关系，无法捕获全局语义、忽略单词级的交互特征。
因此文章提出DvBERT模型，通过结合双塔模型和交互式模型的优点，优化句子嵌入表示及多任务知识蒸馏，对文本相似度计算进行改进。  
# Overview
> ## Model Name  
> DvBERT 双视图蒸馏BERT  
> · siamese视图： 生成句子嵌入的主干，计算向量距离，捕获语义相似性  
> · interaction视图： 将cross sentence之间的交互整合成多个teacher模型，并对siamese的训练集进行预测（类似于标注伪标签/银标签/知识蒸馏），以提高句子嵌入的表示能力（6个STS数据集上有比孪生BERT取得更好的效果）。  
> ## Motivation  
> · 候选句子对未提前给出时，需对所有句子进行配对，计算复杂度O(n^2)。   
> · SBERT（2019）使用孪生BERT网络，仅限于捕获全局语义匹配的全部复杂性，忽略两句子间单词级的交互特征。  
> ## Structure  
> ![Note02-7-1](Img/Note02-7-1.bmp)  
> 基于cross sentence interaction模型，结合siamese BERT模型进行训练，共同优化得到预测Y。  
> ## Method
> 1. siamese BERT：  
> 该模型是普通的双塔结构，利用句子嵌入之间的相似度来预测标签Y。  
> siamese BERT将两个句子转换为连续向量（BERT/RoBERTa），通过平均池化得到两个句子嵌入u和v（mean），经过全连接层将输出投到概率分布中：  
> ![Note02-7-2](Img/Note02-7-2.bmp)  
> 2. cross sentence interaction:  
> 使用来自不同与训练模型的多个teacher（本文用了2个）引入单词间的交互矩阵，丰富单词级的交互特征。模型分别先用标记的数据进行与训练，然后重新进行伪标签并添加到新的数据集中。  
> [CLS]被认为是句子对的聚合语义间隙，用来预测与训练过程中的一个句子对是否连贯，通过全连接层得到分类器：  
>  ![Note02-7-3](Img/Note02-7-3.bmp)  
> 用交叉熵损失进行优化：  
>  ![Note02-7-4](Img/Note02-7-4.bmp)  
> ## Experiment  
> 1. 在6个STS任务上取得SoTA效果  
> 2. DvBERT可以提高泛化能力，优于基础模型  
> 3. teacher annealing策略比损失甲醛有更好的相关性  

## Brief Comment  
本文的主要思想是在文本相似度计算上进行改进，从模型的一小部分出发，阅读本文能更好地了解某一模块的具体工作流程，对类似知识蒸馏的方法有初步的了解。  
