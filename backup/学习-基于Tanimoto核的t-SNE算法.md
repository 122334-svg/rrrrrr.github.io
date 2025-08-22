由于化学空间的数据是高维的（常常包含多种信息，如原子类型，键类型，电荷等），在分析时，需进行降维可视化分析。此算法常用于筛选具有高成功率合成多靶点配体的靶点对。

基于分子特征使用t-SNE算法对分子空间进行二维表示是一种有效的可视化方法。化学空间被认为极其庞大，训练数据集中对该空间的高效采样预计将对预测模型的泛化性能产生重大影响。为可视化分子空间的高维特征，研究者常使用基于Tanimoto核的t-SNE算法，将其映射到2D空间中进行分析。

t-SNE（t-Distributed Stochastic Neighbor Embedding）算法是一种非线性降维技术，通过保留高维数据中的局部相似性关系，将复杂数据映射到低维空间（如2D/3D）进行可视化，使**相似样本聚集、不相似样本分离**。

Tanimoto核（Tanimoto Kernel）​是一种基于分子指纹（如Morgan指纹）的相似性度量函数，通过计算两个分子共有特征与总特征的比例（公式：T(A,B) = |A∩B| / (|A| + |B| - |A∩B|)），量化它们的结构相似性（范围0~1，1表示完全相同）。单用Tanimoto函数得到的是高维相似性矩阵。

有几个关键的函数加以说明。

计算分子指纹的函数--使用GetMorganFingerprintAsBitVect函数计算Morgon分子指纹
```
def calculate_fingerprints(smiles_list):
    mols = [Chem.MolFromSmiles(smiles) for smiles in smiles_list]
    fps = []
    for mol in tqdm(mols, desc="计算分子指纹"):
        fps.append(AllChem.GetMorganFingerprintAsBitVect(mol, 2, nBits=1024))
    return np.array(fps)
```

定义 Tanimoto 核函数--使用到pdist 函数​计算jaccard距离，再进行距离转换（Tanimoto=1−Jaccard Distance）得到Tanimoto相似性矩阵
```
def tanimoto_kernel(X):
    return 1 - pdist(X, metric="jaccard")
```

初始化 t-SNE 分析器，显式设置初始化为 'random'，学习率为 'auto'
```
tsne=TSNE(
    n_components=2,          # 降维目标维度 将高维指纹投影到2D平面，便于可视化筛选
    metric="precomputed",    # 使用自定义距离矩阵 但输入必须是距离矩阵（非原始特征）
    random_state=42,         # 随机种子
    init='random',           # 初始化策略
    learning_rate='auto'     # 学习率控制
)
```

> 本文学习自[sereinna](https://github.com/sereinna/sereinna.github.io/commits?author=sereinna)








