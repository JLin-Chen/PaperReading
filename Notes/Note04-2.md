# Long Short-term Memory  

## Abstract   
RNN是包含循环的网络，允许信息的持久化，它可以被看做是同一神经网络的多次复制，每个神经网络模块会把消息传递给下一下网络，其链式的特征揭示了
RNN本质上是与序列和列表相关的。而LSTM是一种特别的RNN，它比标准的RNN在很多任务上都表现得更好，目前RNN的许多成功应用都是通过LSTM达到的。  

> # Overview  
> 
> ## 一、背景
> 在填空预测任务中，假设相关的信息和预测词的位置之间的间隔非常小，RNN可以较好地学会先前的信息并进行预测。但我们会遇到更加复杂的场景，
> 比如关键信息处于段首预测词处于段尾，在这种情况下，RNN会丧失学习到如此远的信息的能力（虽然理论上可行但在实际运用中将会有难度），
> 这也就是我们所说的*长期依赖问题(Long-term Dependencies)*.  但是，LSTM却能较好地解决上述情况。  
> 
> ## 二、标准RNN  
> 所有RNN都具有一种重复神经网络模块的链式形式，这种形式决定了先前学习到的只是将会向后传播，但随着传播距离的增加，信息开始逐渐遗忘。  
> 在标准RNN中，这个重复的模块只有一个非常简单的结构，如tanh层：  
> ![Note04-2-1](/Img/Note04-2-1.bmp)  
> 
> ## 三、标准LSTM  
> 
> 在LSTM中，重复的主模块拥有不同的结构，并且它们以特殊的形式进行交互，这里我们以拥有3个sigmoid层和2个tanh层的标准LSTM为例：  
> ![Note04-2-2](/Img/Note04-2-2.bmp)   
> 
> LSTM中有几个需要特别注意的地方：  
> * C负责传递细胞状态（我们成一个模块为一个细胞，类似于神经元），它主要以链式形式在模块间传递，仅有少量的交互，因此信息在传递过程中不容易有较大改变。  
> * 图中所示有3个“门”结构，该结构由sigmoid+pointwise构成，用于除去/增添信息。  
> * C保存的是长期记忆（通过门控将记忆信息直接传入主干），h保存的是短期记忆（存在梯度消失现象）。C与模块中多样的较复杂的结构是LSTM与传统RNN的主要区别。  
> 
> ### 1. 决定是否丢弃信息  
>  在读取上一层的输出信息h和该层的输入信息t后，经计算输出f给原细胞状态（1完全保留，0决定舍弃）  
>  ![Note04-2-3](/Img/Note04-2-3.bmp)  
>  
> ### 2. 确定是否更新信息  
>  sigmoid层，输入门层，决定什么值进行更新；  
>  tanh层，创建新的候选值向量。  
>  ![Note04-2-4](/Img/Note04-2-4.bmp)  
>  
> ### 3. 更新细胞状态  
> 上述步骤中的计算已经决定将对细胞状态做出什么改变，该步骤只需计算并更新细胞状态即可。  
> ![Note04-2-5](/Img/Note04-2-5.bmp)  
> 即根据前面确定的目标，丢弃旧信息并添加新信息。  
> 
> ### 4. 输出信息  
> sigmoid层确定细胞状态的哪个部分将被输出；  
> 细胞状态通过tanh并经过一个们结构，最终成为该层的输出内容。  
> ![Note04-2-6](/Img/Note04-2-6.bmp)  
> 
> ## 四、LSTM的变体  
> 正如RNN有许多种变体一样，为了适应不同的任务以及不同模型的具体需求，LSTM也拥有许多的变体：  
> 如增加peephole连接，让sigmoid层接受细胞状态输入：  
> ![Note04-2-7](/Img/Note04-2-7.bmp)  
> 如增改coupled忘记门和输入门：  
> ![Note04-2-8](/Img/Note04-2-8.bmp)  
> 如将忘记门和输入门合并为更新门的GRU(Gated Recurrent Unit)，这种LSTM变体在许多大模型中常见：  
> ![Note04-2-9](/Img/Note04-2-9.bmp)   
> 文章提到大部分的LSTM变体的效果其实差不多，但是在某些情况下，特定任务运用特定架构的LSTM可能会取得比较好的效果。  
> 
> 
