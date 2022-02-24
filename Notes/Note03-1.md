 # Deep contextualized word representations

> Matthew E. Peters, Mark Neumann, Mohit Iyyer, Matt Gardner，Christopher Clark, Kenton Lee, Luke Zettlemoyer  
> NAACL  
> https://arxiv.org/pdf/1802.05365.pdf  

## Abstract  
该论文提出的模型是基于深度学习的词向量表征模型，它能表征词汇的语法和语义特征，且这些特征会随着上下文语境的改变而改变。它的本质是基于大规模语料训练后的双向语言模型内部隐状态特征的组合。  

# Overview
> ## Model Name  
> ELMo（ Embeddings from Language Models）  
> ## Motivation  
> 该论文首次提出了预训练模型这一思想。作者通过把ELMo这一模型与经过预训练的NLP模型的输入层或输出层相结合的方式，
> 使得使用一个模型可以适应不同的NLP下游任务，且进行fine-tune后对于具体的某一任务也有提升效果。  
> ## Structure  
> ![Note03-1-1](/Img/Note03-1-1.bmp)  
> ## Method  
> ELMo模型本质上是由biLM模型得来的  
> 1. biLM  
> 给定句子，通过上下文预测词tk：  
> 前向：![Note03-1-2](/Img/Note03-1-2.bmp)  
> 逆向：![Note03-1-3](/Img/Note03-1-3.bmp)   
> 通过多层LSTM，前向逆向结果相结合，在最后一层进行softmax得到预测词，目标函数去最大化：  
> ![Note03-1-4](/Img/Note03-1-4.bmp)   
> 其中，两个方向的LSTM参数不共享。  
> 
> 2. ELMo  
> 对于每一个词t，L层的biLM可以得到（2L+1）个表达：  
> ![Note03-1-5](/Img/Note03-1-5.bmp)   
> ELMo的通用表达式：  
> ![Note03-1-6](/Img/Note03-1-6.bmp)   
> 即biLM的本质是一个以具体任务为导向的，biLM内部的隐状态层的组合。让NLP模型去学习ELMo内部状态的线性组合，生成共同的词向量，用于后续训练。  
> 
> ## Experiment  
> 1. ELMo只取最后一层输出时效果不错，运用多层的线性组合效果提升不明显  
> 2. 对于不同的任务，把ELMo放在输入层、输出层、输入层和输出层取得的效果都不错，对于某些任务，两层都放效果更好  
> 3. ELMo的不同层能从不同方面表达一个词（低层——语法层面，高层——语义层面）  

## Brief Comment  
阿巴阿巴
