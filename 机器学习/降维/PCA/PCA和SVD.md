###　PCA

**主成分分析**（英语：Principal components analysis，PCA）是一种统计分析、简化数据集的方法。它利用正交变换来对一系列可能相关的变量的观测值进行线性变换，从而投影为一系列线性不相关变量的值，这些不相关变量称为主成分（Principal Components）。

PCA是通过

1. 减少维度之间的冗余关系，来实现降维，同时

2. 最大化每个维度数据的方差，以减小信息损失。

**推导过程**：

1. 设我们有$m$个$n$维数据$X_{n\times m}$，$X = \{x_1, x_2, ... x_m\}$，目的是寻找一个变换矩阵$P_{k\times n}$，使得 $Y_{k\times m}=PX$，将数据从$m$维降到$k$维，同时保持$Y$的协方差最大，以保证最小的信息损失。
2. 数学目的就是找到一个矩阵$P$，使得Y的协方差矩阵为对角矩阵。
3. $Y$的协方差矩阵$D=1/mYY^T=PCP^T$，其中$C=1/mXX^T$，为$X$的协方差矩阵。
4. 将$C$因式分解，$C=QΣQ^T$，则 $D=PQΣQ^TP^T$，
5. 因为$Q$为正交矩阵，$Q^{-1}=Q^T$，只要令$P=Q^T$，则$PQ=I$和$Q^TP^T=I$，得到$D=Σ$，成功将$D$对角化。

所以变换矩阵$P$就是$C$的前$k$个正交特征向量按列组成的矩阵的转置。

**性质**：

设$x$是$m$维随机变量，$Σ$是$x$的协方差矩阵，则$x$的第$k$主成分的方差是协方差矩阵$Σ$的第$k$个特征值。

#### 参考

算例参考 [PCA的数学原理(转) - 知乎](https://app.yinxiang.com/shard/s45/nl/27030704/51e7082a-245c-4644-9945-4c4b7fc6701c)

[主成分分析 - 维基百科，自由的百科全书](https://app.yinxiang.com/shard/s45/nl/27030704/90df4d73-4b0a-45ae-ac9e-014bbb2c81b8)

李航 主成分分析

----



### SVD



优质资料https://medium.com/@jonathan_hui/machine-learning-singular-value-decomposition-svd-principal-component-analysis-pca-1d45e885e491