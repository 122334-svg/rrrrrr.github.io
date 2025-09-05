**grdient descent 梯度下降**
梯度下降是一种优化算法，通过沿着损失函数梯度的反方向逐步调整模型参数，以最小化损失函数值的过程。
**nerual network 神经网络
ALGC artificial intelligence generate content 人工智能生成内容
recap 概要描述
map 映射
overfit 过拟合
VAE variational autoencoder
ligand 配体
target 靶点
robustness 鲁棒性**
鲁棒性是模型的抗干扰能力，系统或模型在收到外部干扰、输入数据存在噪声或自身参数略有变化时，仍然能保持稳定性能和正确输出的能力。
**gradient conflict 梯度冲突**
梯度冲突是指在多任务学习后多目标优化中，不同任务或目标对同一组参数的梯度方向相反或互相干扰，导致模型难以在多个任务上取得良好的表现。
感受野半径Receptive field：感受野是指神经网络中某一特征（如卷积层输出的特征图上的像素）对应的感受野区域的 “半宽”。感受野通常被简化为正方形区域（k*k），一般就是中心到边缘的垂直距离。
**global feature vector 全局特征向量**
对整个样本的整体属性进行编码后的低维数值向量（全部降维），用于表示样本的全局特征。
**Dimensionality reduction 降维**
比较常用的降维方法：PCA、t-SNE等 本质保留数据关键信息的前提下，减少特征维度。
**ReLU：激活函数**
作用：引入非线性，计算简单高效
**BN：批归一化**
作用：标准化（均值0，方差1）、再缩放（因为标准化有会抹杀特性，所以BN还允许分队有自己的特点，通过缩放get）
**pad：填充**
作用：让所有样本在同一维度有相同的尺寸
**stack：堆叠**
作用：将多个意见填充好的、形状完全一致的样本，组合成一个更大的批量张量（batch tensor），形成模型一个batch所需的批量输入张量。所以stack的输出是批量张量（第一个维度是batch_sized d d d d d d d d d d d d d d d d d d d d d d d d d d d d d d d d d d d）




