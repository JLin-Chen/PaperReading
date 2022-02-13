# Rumour Detection via Zero-shot Cross-lingual Transfer Learning

> Lin Tian, Xiuzhen Zhang, and Jey Han Lau  
> ECML/PLDD  
> https://2021.ecmlpkdd.org/wp-content/uploads/2021/07/sub_661.pdf  

## Abstract
使用标注充足的英文语料微调teacher-BERT，让teacher-BERT在zero-shot中文语料标注伪标签，利用伪标签数据训练student-BERT，
在每次迭代的最后用student替换teacher并进行下一次迭代，不断循环，直至student-BERT取得很好的分类效果。（知识蒸馏）  
# Overview
> ## Model Name  
> a zero-shot cross-lingual transfer learning framework  
> ## Motivation  
> 同一个谣言可能通过不同的语言进行传播，文章利用迁移学习的方法使得通过监督训练的model能够在无标签的另一种语言的数据集上进行预测，
> 并且迁移后的模型拥有在两种语言上进行预测的能力。  
> ## Structure  
> ![Note02-6-1](/Img/Note02-6-1.bmp)  
> ## Method  
> A. self-training  
> teacher BERT-用labeled data训练，在unlabeled data上预测，以便为student提供更多训练data。  
> studetn BERT-在每次迭代过程的最后，替换teacher并进入下一次迭代过程，在不断finetune中，提供给student的伪标签的可信度将会提高。  
> 
> B. rumor classifier  
> 将源推文s和回复r按照下面方式构造后输入到多语言预训练模型（multilangual BERT/XML-RoBERTa）中：  
> ![Note02-6-2](/Img/Note02-6-2.bmp)  
> 通过全连接网络后输出预测：  
> ![Note02-6-3](/Img/Note02-6-3.bmp)  
> 根据真实标签用标准二分类cross-entropy loss进行微调，除word embedding外，更新所有向量。  
> 
> C. cross-lingual transfer  
> 因为文章要同时实现源语言和目标语言的二分类问题，所以teacher和student model都采用multilingual model。  
> （但为了进行对比，实验中也使student采用monolingual model进行对照）  
> ![Note02-6-4](/Img/Note02-6-4.bmp)  
> 在self-training loop中，  
> · student model用teacher model进行初始化；  
> · 一旦student model训练完毕，在下一次迭代开始时，原teacher model将被刚训练的student model替代；  
> · 为了降低标签中的噪声，将得分低于阈值p的标签过滤；为避免分类数目不均等影响学习，使用平衡机制滤除得分较高的一些标签。  
> 
> ## Experiment  
> ![Note02-6-5](/Img/Note02-6-5.bmp)  
> 上面数据展示了用中文/英文分别作为源语言/目标语言时，该文章中proposed model的表现情况。  

## Brief Comment  
文章的亮点在于创新性地提出了teacher-student这一学习方法并且在实验上也取得了较好的表现，较好地进行了知识的迁移。  
