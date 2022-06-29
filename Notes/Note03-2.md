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

![BERT_3](/Img/BERT_3.bmp)  

BERT使用两个新的无监督预测任务进行预训练，如下：

### 1. Masked LM(MLM)  
目标：训练深度双向Transformer表示  
方法：随机掩盖部分输入词，对被掩盖的词进行预测（类似于完型填空）  
特点：MLM的性质与Transformer的结构匹配（类似传统的LM算法和RNN匹配）

训练：  
* BERT在预训练时只预测[Mask]位置的单词，这样可以同时利用上下文信息。在后续使用时，并不会出现[Mask]的单词，否则会影响模型性能。  
* 由于上述原因，在训练时随机选择句子中15%的单词进行Mask。在选择为Mask的单词中，有80%真的使用[Mask]进行替换，10%使用一个随机单词进行替换，10%保留原词不进行替换。  
* 上述10%保留原词，是为了将表征偏向真实观察值；10%随机词替代，不会影响模型对语言的理解能力。  
* 因为每次只能预测15%的词，模型收敛比较慢。

### 2. Next Sentence Prediction(NSP)  
目标：是一个二分类任务，判断句子B是否是句子A的下文。若是，输出标签‘IsNext’；若否，输出标签‘NotNext’。  
原因：很多句子级别的任务，如自动问答QA和自然语言推理NLI都需要理解两个句子之间的关系  
特点：训练数据的生成方式是从平行语料中随机抽取的连续两句话。其中50%保留抽取的两句话，它们符合‘IsNext’的关系；另外50%的第二句话是随机从语料中提取的，它们的关系是‘NotNext’。
BERT模型使用[CLS]的编码信息进行预测。  


## 微调(Fine-tune)

预训练得到的BERT模型可通过Fine-tune来适应不同的NLP任务。  

![BERT_a](/Img/BERT_a.bmp)

### a. 句子对分类任务  

如自然语言判断MNLI，句子语义等价判断QQP等  

将两个句子输入BERT，使用[CLS]的输出向量C进行句子对分类。

### b. 单句分类任务  

如句子情感分析SST-2，判断句子语法是否可以接受CoLA等  

将一个句子输入BERT，无需使用[SEP]标签，使用[CLS]的输出向量C进行分类。  

![BERT_b](/Img/BERT_b.bmp)

### c. 问答任务  

将Question和Paragraph传入BERT，然后BERT根据Paragraph所有单词的输出预测Start和End的位置。

### d. 单句标注任务

如命名实体识别NER

将单个句子输入BERT，根据BERT对每个单词的输出向量T预测这个单词的类别（Person, Organization,Lacation,Miscellaneous, or Other）



### 任务效果

![BERT_result](/Img/BERT_result.bmp)







