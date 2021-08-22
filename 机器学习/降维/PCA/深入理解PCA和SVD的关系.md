先简单回顾下主成分析`PCA(principle component analysis)`与奇异值分解`SVD(singular value decomposition)`。

## **一、主成分析PCA**

**1、所解决问题**

给定 ![[公式]](https://www.zhihu.com/equation?tex=m) 个 ![[公式]](https://www.zhihu.com/equation?tex=n) 维样本![[公式]](https://www.zhihu.com/equation?tex=X%3D%5Cleft%5C%7B+x_0%2C+x_1%2C+...%2Cx_m+%5Cright%5C%7D) ，通过变换 ![[公式]](https://www.zhihu.com/equation?tex=y%3DPx) (其中 ![[公式]](https://www.zhihu.com/equation?tex=P_%7Bk%5Ctimes+n%7D) 为变换矩阵)，将样本 ![[公式]](https://www.zhihu.com/equation?tex=%28x_i%29_%7Bi%3D0%2C...%2Cm%7D) 从 ![[公式]](https://www.zhihu.com/equation?tex=n) 维降到 ![[公式]](https://www.zhihu.com/equation?tex=k) 维 ![[公式]](https://www.zhihu.com/equation?tex=%28y_i%29_%7Bi%3D0%2C...%2Cm%7D) ，计![[公式]](https://www.zhihu.com/equation?tex=Y%3D%5Cleft%5C%7B+y_0%2C+y_1%2C+...%2Cy_m+%5Cright%5C%7D) ，同时最大程度的减少降维带来的信息损失。

**2、所依赖的原则**

根据降维并减小信息损失的目标，可以得出以下两个原则

1. 降维后的各个维度之间相互独立，即去除降维之前样本 ![[公式]](https://www.zhihu.com/equation?tex=x) 中各个维度之间的相关性。
2. 最大程度保持降维后的每个维度数据的多样性，即最大化每个维度内的方差

记降维后样本集 ![[公式]](https://www.zhihu.com/equation?tex=Y) 的协方差矩阵为

![[公式]](https://www.zhihu.com/equation?tex=B_%7Bk%5Ctimes+k%7D%3D%5Cfrac%7B1%7D%7Bm%7DYY%5E%7BT%7D)

上述第一个条件要求协方差矩阵B除了对角线上元素外，其他均为0，也即 ![[公式]](https://www.zhihu.com/equation?tex=B) 为对角矩阵。

将变换关系![[公式]](https://www.zhihu.com/equation?tex=y%3DPx) 代入Y的协方差矩阵B中，

![[公式]](https://www.zhihu.com/equation?tex=B_%7Bk%5Ctimes+k%7D%3D%5Cfrac%7B1%7D%7Bm%7DYY%5E%7BT%7D%3D%5Cfrac%7B1%7D%7Bm%7DPX%28PX%29%5E%7BT%7D%3DP%5Cfrac%7B1%7D%7Bm%7DXX%5E%7BT%7DP%5E%7BT%7D%3DP_%7Bk%5Ctimes+n%7DC_%7Bn%5Ctimes+n%7DP%5E%7BT%7D_%7Bn%5Ctimes+k%7D) --------(1)

其中， ![[公式]](https://www.zhihu.com/equation?tex=C_%7Bn%5Ctimes+n%7D%3D%5Cfrac%7B1%7D%7Bm%7DXX%5E%7BT%7D) 是变换前数据 ![[公式]](https://www.zhihu.com/equation?tex=X) 的协方差矩阵。

![[公式]](https://www.zhihu.com/equation?tex=C_%7Bn%5Ctimes+n%7D) 的特征值分解形式如下：

![[公式]](https://www.zhihu.com/equation?tex=D_%7Bn%5Ctimes+n%7D%3DQ_%7Bn%5Ctimes+n%7DC_%7Bn%5Ctimes+n%7DQ%5E%7BT%7D_%7Bn%5Ctimes+n%7D) --------(2)

其中， ![[公式]](https://www.zhihu.com/equation?tex=D_%7Bn%5Ctimes+n%7D) 为对角矩阵。

明显的式(1)和式(2)除了维度不同，其他均一样。

结合上述第二条原则，变换矩阵 ![[公式]](https://www.zhihu.com/equation?tex=P_%7Bk%5Ctimes+n%7D) 即是矩阵C的前k大的特征向量按行组成的矩阵。

> 以下为特征向量按列排布
>
> $D_{n\times n}=Q_{n \times n}^TC_{n \times n}Q_{n\times n}$
>
> $Q_{n\times n}$为矩阵$C$的特征向量按列组成的矩阵
>
> 变换矩阵$P_{k\times n}$即是矩阵$C$的前$k$大的特征向量按列组成的矩阵的转置。



**3、问题求解方法**

式2就是协方差矩阵 ![[公式]](https://www.zhihu.com/equation?tex=C) 的特征值分解，变换矩阵 ![[公式]](https://www.zhihu.com/equation?tex=P_%7Bk%5Ctimes+n%7D) 即是矩阵C的前k大的特征向量按行组成的矩阵。所以，PCA的求解步骤为：

- 求 ![[公式]](https://www.zhihu.com/equation?tex=X) 均值
- 将 ![[公式]](https://www.zhihu.com/equation?tex=X) 减去均值
- 计算协方差矩阵 ![[公式]](https://www.zhihu.com/equation?tex=C%3D%5Cfrac%7B1%7D%7Bm%7DXX%5E%7BT%7D)
- 对协方差矩阵 ![[公式]](https://www.zhihu.com/equation?tex=C) 特征值分解
- 从大到小排列 ![[公式]](https://www.zhihu.com/equation?tex=C) 的特征值
- 取前 ![[公式]](https://www.zhihu.com/equation?tex=k) 个特征值对应的特征向量按行组成矩阵即为变换矩阵 ![[公式]](https://www.zhihu.com/equation?tex=P_%7Bk%5Ctimes+n%7D)

**这里的核心问题是协方差矩阵** ![[公式]](https://www.zhihu.com/equation?tex=C%3D%5Cfrac%7B1%7D%7Bm%7DXX%5E%7BT%7D) **的特征值分解**

## **二、奇异值分解SVD**

**1、所解决问题**

![[公式]](https://www.zhihu.com/equation?tex=A_%7Bm%5Ctimes+n%7D%3DU_%7Bm%5Ctimes+m%7D%5CSigma+_%7Bm%5Ctimes+n%7DV_%7Bn%5Ctimes+n%7D%5E%7BT%7D) --------(3)

其中 ![[公式]](https://www.zhihu.com/equation?tex=U_%7Bm%5Ctimes+m%7D) 和 ![[公式]](https://www.zhihu.com/equation?tex=V_%7Bn%5Ctimes+n%7D) 均为正交矩阵， ![[公式]](https://www.zhihu.com/equation?tex=%5CSigma+_%7Bm%5Ctimes+n%7D) 为对角矩阵

奇异值分解要解决的问题是将 ![[公式]](https://www.zhihu.com/equation?tex=A_%7Bm%5Ctimes+n%7D) 矩阵分解为对角矩阵 ![[公式]](https://www.zhihu.com/equation?tex=%5CSigma+_%7Bm%5Ctimes+n%7D) ，![[公式]](https://www.zhihu.com/equation?tex=%5CSigma+_%7Bm%5Ctimes+n%7D)中对角元素 ![[公式]](https://www.zhihu.com/equation?tex=%5Csigma+_i) 称为矩阵 ![[公式]](https://www.zhihu.com/equation?tex=A_%7Bm%5Ctimes+n%7D) 的奇异值

**2、问题求解方法**

![[公式]](https://www.zhihu.com/equation?tex=A%5E%7BT%7DA%3D%28U%5CSigma+V%5E%7BT%7D%29%5E%7BT%7DU%5CSigma+V%5E%7BT%7D%3DV%5CSigma+%5E%7BT%7DU%5E%7BT%7DU%5CSigma+V%5E%7BT%7D%3DV%5CSigma+%5E%7BT%7D%5CSigma+V%5E%7BT%7D%3DV%5CSigma+%5E%7B2%7D+V%5E%7BT%7D)

> ❗❗ 这里有个错误，$\Sigma$不是方阵，所以不能写成$\Sigma ^2$

所以 ==![[公式]](https://www.zhihu.com/equation?tex=V)是 ![[公式]](https://www.zhihu.com/equation?tex=A%5E%7BT%7DA) 特征值分解的特征向量按列组成的正交矩阵==， ![[公式]](https://www.zhihu.com/equation?tex=%5CSigma+%5E%7B2%7D) 是![[公式]](https://www.zhihu.com/equation?tex=A%5E%7BT%7DA) 特征值组成的对角矩阵，也可以看出 ![[公式]](https://www.zhihu.com/equation?tex=A_%7Bm%5Ctimes+n%7D) 的奇异值 ![[公式]](https://www.zhihu.com/equation?tex=%5Csigma+_i)是是![[公式]](https://www.zhihu.com/equation?tex=A%5E%7BT%7DA) 特征值 ![[公式]](https://www.zhihu.com/equation?tex=%5Clambda+_%7Bi%7D) 的平方根。

> ==$U$是$AA^T$特征分解的特征向量按列组成的正交矩阵。==

![[公式]](https://www.zhihu.com/equation?tex=%5Csigma+_%7Bi%7D%3D%5Csqrt%7B%5Clambda+_%7Bi%7D%7D) --------(4)

> 奇异值一定为正数。

假如![[公式]](https://www.zhihu.com/equation?tex=A%5E%7BT%7DA)的特征向量为 ![[公式]](https://www.zhihu.com/equation?tex=v_%7Bi%7D) ，则根据式3和式4， ![[公式]](https://www.zhihu.com/equation?tex=U) 中对应的 ![[公式]](https://www.zhihu.com/equation?tex=u_%7Bi%7D) 则可以由下式求出 ：

![[公式]](https://www.zhihu.com/equation?tex=u_%7Bi%7D+%3D+%5Cfrac%7BAv_%7Bi%7D%7D%7B%5Csigma+_%7Bi%7D%7D) --------(5)

也即**奇异值分解的关键在于对 ![[公式]](https://www.zhihu.com/equation?tex=A%5E%7BT%7DA) 进行特征值分解。**

> $A^TA$和$AA^T$具有相同的正特征根，区别只在0特征根的数量。

## **三、PCA与SVD的关系**

由上述分析可知，

1. PCA求解关键在于求解协方差矩阵![[公式]](https://www.zhihu.com/equation?tex=C%3D%5Cfrac%7B1%7D%7Bm%7DXX%5E%7BT%7D)的特征值分解
2. SVD关键在于 ![[公式]](https://www.zhihu.com/equation?tex=A%5E%7BT%7DA) 的特征值分解。

很明显二者所解决的问题非常相似，都是对一个实对称矩阵进行特征值分解，

如果取：

![[公式]](https://www.zhihu.com/equation?tex=A%3D%5Cfrac%7BX%5E%7BT%7D%7D%7B%5Csqrt%7Bm%7D%7D)

则有：

![[公式]](https://www.zhihu.com/equation?tex=A%5E%7BT%7DA%3D%5Cleft%28+%5Cfrac%7BX%5E%7BT%7D%7D%7B%5Csqrt%7Bm%7D%7D+%5Cright%29%5E%7BT%7D%5Cfrac%7BX%5E%7BT%7D%7D%7B%5Csqrt%7Bm%7D%7D%3D%5Cfrac%7B1%7D%7Bm%7DXX%5E%7BT%7D)

SVD与PCA等价，所以PCA问题可以转化为SVD问题求解，那转化为SVD问题有什么好处？

有三点：

1. 一般 ![[公式]](https://www.zhihu.com/equation?tex=X) 的维度很高，![[公式]](https://www.zhihu.com/equation?tex=A%5E%7BT%7DA) 的计算量很大
2. 方阵的特征值分解计算效率不高
3. ==SVD除了特征值分解这种求解方式外，还有更高效且更准确的迭代求解法，避免了![[公式]](https://www.zhihu.com/equation?tex=A%5E%7BT%7DA) 的计算==

其实，PCA只与SVD的右奇异向量的压缩效果相同。

1. 如果取 ![[公式]](https://www.zhihu.com/equation?tex=V)的前 ![[公式]](https://www.zhihu.com/equation?tex=k) 行作为变换矩阵 ![[公式]](https://www.zhihu.com/equation?tex=P_%7Bk%5Ctimes+n%7D) ，则 ![[公式]](https://www.zhihu.com/equation?tex=Y_%7Bk%5Ctimes+m%7D%3DP_%7Bk%5Ctimes+n%7DX_%7Bn%5Ctimes+m%7D) ，起到==压缩行==即降维的效果
2. 如果取 ![[公式]](https://www.zhihu.com/equation?tex=U)的前 ![[公式]](https://www.zhihu.com/equation?tex=d) 行作为变换矩阵 ![[公式]](https://www.zhihu.com/equation?tex=P_%7Bd%5Ctimes+m%7D) ，则 ![[公式]](https://www.zhihu.com/equation?tex=Y_%7Bn%5Ctimes+d%7D%3DX_%7Bn%5Ctimes+m%7DP_%7Bm%5Ctimes+d%7D) ，起到==压缩列==即去除冗余样本的效果。



[深入理解PCA与SVD的关系 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/58064462)

