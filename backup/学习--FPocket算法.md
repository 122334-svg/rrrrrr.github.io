fpocket 是一种蛋白质口袋预测算法。它允许用户根据 PDB 蛋白质结构识别有效的结合位点。该算法基于 Voronoi 网格细分，速度非常快，尤其适用于大规模蛋白质结合口袋筛选以及开发用于表征结合口袋的评分函数。现在，fpocket 还支持在 MD 轨迹上进行口袋检测，并评估结合位点的体积和成药性。最后，现在还可以使用 fpocket 和 mdpocket 计算相互作用能量。

蛋白质结合口袋是配体识别的关键单元。而这些口袋不是静止不变的，而是有“动态行为”，随构象的变化而出现、扩张或消失。

Fpocket是一个无监督的口袋检测算法。基于蛋白质的3D结构，通过几何和化学特征来从头预测所有可能的结合口袋，并给出每个口袋的打分。不依赖任何已知的结合信息。使用算法：基于Voronoi tessellation（沃罗诺伊剖分） 和 α球（Alpha Sphere） 方法来识别空腔与口袋。

fpocket 程序套件是一款基于 Voronoi 镶嵌的快速开源蛋白质口袋检测算法。该平台适用于希望开发新的评分函数并大规模提取口袋描述符的科研人员。
fpocket程序套件中包含：

1. fpocket ：单个蛋白质结构的原始口袋预测
2. mdpocket ：fpocket 的扩展，用于分析蛋白质的构象集合（例如 MD 轨迹）
3. dpocket ：提取口袋描述符
4. tpocket ：测试你的口袋得分功能

常见蛋白质文件格式

1. PDB：常用的生物大分子结构文件格式。PDB 文件主要包含生物大分子的原子坐标信息，以及一些基本的结构描述，如原子名称、残基名称、链标识符等。
2. MMCIF：CIF（晶体学信息文件）格式在大分子晶体学领域的扩展。MMCIF 格式的数据内容更加丰富和灵活，不仅包含了 PDB 文件中的基本结构信息，还能详细记录更多的元数据，如实验条件（温度、pH 值等 ）、数据处理过程、结构模型的验证信息、生物分子的化学修饰等。

### 代码实现
安装（使用conda）
```
conda config --add channels conda-forge
conda install fpocket
```

输入（可以接受PDB or PDBx/mmcif格式）
```
1: flag -f :    one standard PDB or PDBx/mmcif file name. #单个文件输入
2: flag -F :    one text file containing a simple list of pdb path #多个文件输入
````

输出文件：fpocket 直接在数据文件目录中生成输出，并使用 PDB 文件名加上 _out 扩展名创建一个目录。
```
    total 332
    -rw-r--r-- 1 peter users    769 Nov 29 00:14 3LKF.pml
    -rw-r--r-- 1 peter users    698 Nov 29 00:14 3LKF.tcl
    -rwxr-xr-x 1 peter users     30 Nov 29 00:14 3LKF_PYMOL.sh
    -rwxr-xr-x 1 peter users     41 Nov 29 00:14 3LKF_VMD.sh
    -rw-r--r-- 1 peter users 245835 Nov 29 00:14 3LKF_out.pdb
    -rw-r--r-- 1 peter users   6725 Nov 29 00:14 3LKF_pockets.info
    -rw-r--r-- 1 peter users  49355 Nov 29 00:14 3LKF_pockets.pqr
    -rw-r--r-- 1 peter users   4073 Nov 29 00:14 3LKF_info.txt
    drwxr-xr-x 2 peter users   4096 Nov 29 00:14 pockets
````

--补充：点云--
“点云”（Point Cloud）是一种三维空间数据的表示形式，本质是由大量离散的 “点” 组成的集合，每个点都包含精确的三维坐标（X、Y、Z），部分点还会附带额外属性（如颜色、法向量、强度等），最终通过这些点的密集排列来 “还原” 真实物体的三维形状和空间位置。

可以通俗理解为：把一个 3D 物体 “拆成无数个极小的点”，每个点记录自己在空间中的位置，这些点拼在一起，就能让计算机 “看见” 物体的立体结构 —— 就像用无数个像素点组成 2D 图片，点云是用无数个 3D “空间像素点” 组成立体模型。

点云必备：三维坐标。还有些点云可能福袋其他属性：如颜色、法向量、强度、类别标签。
点云如何获得三维点？用生物大分子（蛋白质/药物）举例：直接从PDB/MMCIF文件中提取，将蛋白质的原子坐标（X、Y、Z）直接转换为点云（每个原子对应一个点）。

>具体的输出文件详解见 [https://github.com/Discngine/fpocket/blob/master/doc/GETTINGSTARTED.md#fpocket-advanced](url)

> fpoket源码自 [https://github.com/Discngine/fpocket](url)

> fpocket讲解学习自公众号[https://mp.weixin.qq.com/s/Pfz7znc-QtG2FpwudOXTrw](url)