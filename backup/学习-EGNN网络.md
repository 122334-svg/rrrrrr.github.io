EGNN（E(n)-Equivariant Graph Neural Network）是一种保持欧几里得变换（平移、旋转、反射）等变的图神经网络，通过几何感知的消息传递处理动态或3D图结构数据。（EGNN最重要的思想就是几何等变）。

EGNN网络的工作原理可以用通俗易懂的例子描述：首先EGNN网络它处理的是图结构，这些数据的特点（以药物配体为例）：节点之间有联系（边），但没有固定的顺序，且节点位置可能在空间中变换（比如分子旋转）。
EGNN的工作过程是每个节点回西安关注自己邻居的状态，收集邻居的“信息”（比如原子类型、坐标、电荷等特征信息），然后，节点会根据邻居的信息更新自己的“状态”（让自己的特征变得更加综合，包含邻居的影响）。那么，EGNN最特别的地方就是“等变”，他所有的特征都会随着空间变换自动动。

在EGNN中，（在github中分为egnn_pytorch和egnn_pytorch_geometric，其中的egnn_pytorch是按照我这个思路的），输入的数据是一张大图（一个batch一个图，batch_size表明了一个batch有多少个样本），这个大图中包含了很多小图，每个小图就是一个样本。小图和小图之间是通过先将独立的小图进行填充（使得小图和小图之间的张量对齐），然后创建掩码，再堆叠成批（变成一个列表中的多个元素）。

EGNN处理的数据类型：“节点“和”边“

### 代码实现
先准备环境
`pip install egnn-pytorch`
准备工作：
```
import torch
from egnn_pytorch import EGNN_Network
```

1. define neural network （EGNN）
```
net = EGNN_Network(
    num_tokens = 21,    # 节点的“身份类型”有21种（比如20种氨基酸+1种空节点）
    dim = 32,           # 每个节点的“特征向量”长度为32（相当于给节点的身份信息编码）
    depth = 3,          # 网络有3层（类似过滤筛，每层提炼更高级的信息）
    edge_dim = 4,       # 每条边的“特征向量”长度为4（描述两个节点的关系，比如距离、作用力）
    num_nearest_neighbors = 3  # 每个节点最多关注3个近邻（太远的节点关系弱，忽略）
)
```
2.准备输入数据，输入数据将被分成3类：节点信息、坐标信息、边信息
```
# 1. 节点的“身份信息”（比如原子类型）
feats = torch.randint(0, 21, (1, 1024))  
# 形状：(1, 1024) → 1个样本，1024个节点，每个节点是0-20中的一个数字（代表一种类型）

# 2. 节点的3D坐标（比如原子在空间中的位置）
coors = torch.randn(1, 1024, 3)  
# 形状：(1, 1024, 3) → 每个节点有x、y、z三个坐标值

# 3. 标记“有效节点”（排除填充的假节点）
mask = torch.ones_like(feats).bool()  
# 形状：(1, 1024) → 全是True，代表这1024个节点都是真实的
```
3.定义“边”的信息
```
# 1. 边的“细节特征”（比如两个原子的距离、电荷差异等）
continuous_edges = torch.randn(1, 1024, 1024, 4)  
# 形状：(1, 1024, 1024, 4) → 每个“节点对”（i和j）有4个数字描述关系

# 2. 哪些节点相连（邻接矩阵）
i = torch.arange(1024)  # 生成0-1023的序号（代表1024个节点）
adj_mat = (i[:, None] >= (i[None, :] - 1)) & (i[:, None] <= (i[None, :] + 1))  
# 这行代码的意思：只让“序号相邻”的节点相连（比如节点5只连4、5、6）
# 形状：(1024, 1024) → 像个表格，adj_mat[i][j]为True表示节点i和j相连
```
4.运行模型
```
feats_out, coors_out = net(feats, coors, edges = continuous_edges, mask = mask, adj_mat = adj_mat)
```

> 代码引用自[[egnn-pytorch](https://github.com/lucidrains/egnn-pytorch)](url)