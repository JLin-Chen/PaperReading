# Cross-lingual COVID-19 Fake News Detection

> Jiangshu Du, Yingtong Dou, Congying Xia, Limeng Cui, Jing Ma, Philip S. Yu  
> arXiv  
> https://arxiv.org/pdf/2110.06495.pdf  

## Abstract  
文章提出中文新冠疫情虚假新闻数据集，实现多语言场景下对虚假新闻进行分类。

# Overview  
利用预训练好的BERT在标注充足的英文数据集上进行微调，将中文翻译为英文后，再输入到微调后的BERT中，进行分类。  
> ## Model Name
> ## Motivation
> ## Structure
> ## Method
> ## Experiment

## Brief Comment  
个人感觉整个模型的关键步骤在于中译英这一块，翻译的地道程度在很大程度上会影响模型分类的准确性。
可能作者的主要迁移工作是把中文语境下的新闻事件放到外国语境中的这一种迁移。
