<img width="551" height="575" alt="Image" src="https://github.com/user-attachments/assets/09d1eb34-8b6b-4728-b8b8-4916b14c2852" />
VAE（Variational AutoEncoder）：最简单的生成式模型之一。基本流程：编码-采样-解码。
变分自编码器与自编码器最大的区别就在潜在表示。在自编码器中，潜在表示是一个**固定值**，而 VAE 中，潜在表示则是一个**不确定变量**，或者换一个说法，是一个**概率分布**。在VAE中，编码器不只学习输入数据的编码信息，而是学习获取输入数据的概率分布。 

<img width="826" height="349" alt="Image" src="https://github.com/user-attachments/assets/ffc882df-0b04-4ac4-85fc-03977f87d329" />
在潜在空间中进行采样（概率分布：一般是正态分布）可以得到不同的输出。 
encoder：数据编码与压缩。学习潜在分布的参数。
重参数化采样：难点：直接采样，反向传播时梯度无法从解码器传回编码器，导致模型无法训练。
decoder：数据生成。AIGC（artificial intelligence generate content）! 
VAE的目标：通过办法，让隐空间平滑。how to do？ how to 平滑--增加随机性（引入概率，贝叶斯定律Bayesian Rules）。 
VAE公式：p（z｜x）表示encoder p（x｜z）表示decoder
<img width="468" height="102" alt="Image" src="https://github.com/user-attachments/assets/ec6f6caa-913b-4d48-b888-9102183bcdaf" />
VAE的具体目标：用两个neural network （encoder decoder）去逼近（损失函数）和模拟p（z｜x）、p（x｜z）这两个概率分布，并且尽量保证p（z）和p（z｜x）【隐空间】是平滑的。

loss（逼近）：用于做gradient descent（梯度下降）。这里就是要知道如何逼近（近似模拟）一个概率分布？需要一个判断概率分布距离的方法，需要这个方法能很方便计算，而且可导，才方便做gradient descent。这里的想法都可以用VI（Variational infernece），用来让两个概率分布逼近，并且计算简单。

--recap--
VAE目标是平滑隐空间。训练目标是“让模型学习到的数据分布尽可能接近真实数据分布”
VAE引入概率来平滑隐空间，计算loss的方法是用neural network 来逼近p（x｜z）和p（z｜x），并且尽量保证p（z）和p（z｜x）【隐空间】是平滑的。loss函数本质：求KL散度（两个分布之间的距离）min值。
VAE的损失函数：重构误差（确保输入能被准确重构）+KL散度（保证潜在分布接近先验分布）

--补充：概率的英文读法--
p（z｜x）--p of z given x