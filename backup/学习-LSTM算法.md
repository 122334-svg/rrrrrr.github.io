LSTM算法是一种特殊的循环神经网络（RNN）算法，专门设计用于解决传统RNN在处理长序列数据时存在的梯度消失和梯度爆炸问题。

<img width="1080" height="524" alt="Image" src="https://github.com/user-attachments/assets/ff3a9ba9-7d18-41a9-bbfc-f78de7549c1a" />

通过引入细胞状态和门控机制，使得模型能够捕捉和保存长期依赖信息，从而有效地处理序列数据中的长期依赖关系。

**1. 细胞状态：LSTM的core，网络的“记忆单元”。能够沿着时间链传递信息，只受到门控单元的少量线性交互。
2. 遗忘门：决定细胞状态中哪些信息需要被丢弃。**

<img width="822" height="384" alt="Image" src="https://github.com/user-attachments/assets/994e21a9-f300-4739-afd9-5cd198ae80ac" />

**3. 输入门：决定哪些信息需要写入细胞状态。（输入门层+候选细胞状态）**

<img width="322" height="64" alt="Image" src="https://github.com/user-attachments/assets/1bf5b771-bec0-49a2-a704-4b349bf7d1af" />

<img width="340" height="58" alt="Image" src="https://github.com/user-attachments/assets/0d91728d-11c1-4077-99a6-69f46dce5e01" />

**4. 更新细胞状态**

<img width="600" height="206" alt="Image" src="https://github.com/user-attachments/assets/766b49a9-346a-454b-a410-5a3bba982f91" />

**5. 输出门：决定当前细胞状态哪些信息应该被输出。**

<img width="602" height="106" alt="Image" src="https://github.com/user-attachments/assets/da6685ff-497e-408a-b595-81e11c4aedff" />

通过这三个门的控制，LSTM 能够选择性地保留和丢弃信息，从而有效捕捉长期依赖。
LSTM计算过程：遗忘门--输入门--更新细胞状态--输出门

LSTM 的优势
解决长期依赖问题：LSTM 能够有效地捕获和利用序列中远距离的依赖关系，这是其最显著的优势。
更好的梯度流动：门控机制确保了梯度在反向传播时能够更好地流动，缓解了梯度消失问题。
适用于各种序列任务：在语音识别、自然语言处理（机器翻译、文本生成、情感分析）、时间序列预测等领域表现出色。

数据归一化的意义：

1. 消除量纲差异（单位不同带来的数据差异大）
2. 加速模型收敛（优化算法（如SGD）在归一化参数空间更易找到最优解）     
3. 增强模型跨数据集预测能力                   

> 原文链接：https://blog.csdn.net/Q2024107/article/details/149447301

名词解释：
“梯度”：每个环节的”责任反馈“。梯度是误差信号随时间步反向传播时的参数更新量。
“梯度消失/爆炸”：反馈信号过弱/过强。
隐藏状态：网络在每一时间步中保留的记忆。压缩储存了从序列开始到当前时间步的所有关键信息。



