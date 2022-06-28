 # BERT

> Jacob Devlin Ming-Wei Chang Kenton Lee Kristina Toutanova  
> 论文链接： https://arxiv.org/pdf/1810.04805.pdf  
> Github地址：https://github.com/google-research/bert

## Abstract
2018年，Google提出的**BERT**(**B**idirectional **E**ncoder **R**epresentations from **T**ransformer)模型在11项NLP任务中取得state of art结果，成为NLP发展史上的里程碑式的模型成就。

* **B**idirectional: BERT模型结构和ELMo类似，均为双向

* **E**ncoder: BERT只用到了Transformer的Encoder编码部分

* **R**epresentation: BERT可进行词或句子的语义表征

* **T**ransformer: Transformer Encoder是BERT的核心组成部分

BERT模型的目标是利用**自监督学习**方法在大规模**无标注**语料上进行与训练，从而捕捉丰富的文本**语义**信息。

在特定的NLP任务中，可以根据任务类型对BERT预训练模型参数进行**微调(fine-tune)**，以适应不同的下游任务，取得更好的效果。


# Overview
## Model Architechture

BERT的网络架构采用多层Transformer Encoder结构，最大特点是抛弃了传统的RNN和CNN，通过Attention机制将任意位置的两个单词的距离转换成1，有效的解决了NLP中棘手的长期依赖问题。

![BERT_1](/Img/BERT_1.bmp)  

* Transformer具体架构移步[Note04-4](/Notes/Note04-4.md)  
* BERT使用的是双向Transformer解码器，GPT使用的是单向Transformer解码器，ELMo使用两个独立训练的LSTM结构； 
* BERT和GPT是基于微调的方式，ELMo是基于特征的方式；   
* 只有BERT的表征会基于所有层中的左右两侧语境。

BERT提供了基础和复杂两个模型，对应超参数如下：

1. BERT-base：L=12，H=768，A=12，参数总量110M

2. BERT-large：L=24，H=1024，A=16，参数总量340M

* L是网络的层数（Transformer blocks的数量），A是Multi-Head Attention中self-Attention的数量，H是输出向量的维度。

## BERT的输入表示

BERT模型的输入为表示单个文本句或一对文本的词序列。对于给定的词，其输入的表示通过三部分Embedding求和得到。

![BERT_2](/Img/BERT_2.bmp)  

* Token Embedding：分词后的词向量；  
* Position Embedding：位置嵌入是指将单词的位置信息编码成特征向量，位置嵌入是向量模型中引入单词位置关系的至关重要的一环；  
* Segment Embedding：用于区分两个句子。对于句子对的输入，第一个句子的特征值是0，第二个句子的特征值是1.

* [CLS]一般位于句首，是输入的第一个token，其对应的输出向量可以作为整个输入句子的表示，用于之后的分类任务。  
* [SEP]表示分句符号，用于断开输入预料中的两个句子。  

## 预训练任务



