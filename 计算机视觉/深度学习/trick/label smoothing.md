### label smoothing

label smoothing可以看做是一种正则化手段，而且是对标签进行正则化。

**target**为**one-hot**编码，损失函数为交叉熵的情况下。解析解是
$$
exp(z_{true})\to C,exp(z_{false})\to 0
$$

$$
z_{true}\to C,z_{false} \to -\infty
$$

这种最优的情况一般是不能达到的，且$z_{true}$会远大于$z_{false}$。在文章《Rethinking the inception architecture for computer vision》里面认为如果$z_{true}$远大于$z_{false}$，会出现两个不好的性质

1. 导致过拟合，将所有的概率都赋给了真值，会导致泛化能力下降。
2. 鼓励真值对应的$logit$远大于其他值的$logit$，但是导数![[公式]](https://www.zhihu.com/equation?tex=%5Cfrac%7B%5Cpartial+l%7D%7B%5Cpartial+z_i%7D)是有界的，也就是数值不会很大，想要达成远大于的效果，要更新很多很多次。

PS：我感觉理由有点牵强。



论文《bag of tricks for image classification with convolutional neural networks》还画出了gap图，此处的gap就是导数等于0的情况下，$z_{true}$和$z_{false}$之间的数值误差：

![img](https://pic2.zhimg.com/80/v2-24a151bbdec0b1fd5d56708a0408d251_720w.jpg)



gap就是![[公式]](https://www.zhihu.com/equation?tex=+log%28%5Cfrac%7B%28K-1%29%281-%5Cvarepsilon+%29%7D%7B%5Cvarepsilon%7D%29)，其中**K**是分类的类别数，![[公式]](https://www.zhihu.com/equation?tex=%5Cvarepsilon)（eps）是label smooth的超参数。假设![[公式]](https://www.zhihu.com/equation?tex=%5Cvarepsilon)取0.5且是1000分类，那么

![[公式]](https://www.zhihu.com/equation?tex=log%28%5Cfrac%7B%28K-1%29%281-%5Cvarepsilon+%29%7D%7B%5Cvarepsilon%7D%29%3Dlog%28%5Cfrac%7B%281000-1%29%281-0.5+%29%7D%7B0.5%7D%29%3Dlog%28999%29%5Capprox+7%EF%BC%88%E4%BB%A5e%E4%B8%BA%E5%BA%95%EF%BC%8C%E4%B8%8D%E6%98%AF%E4%BB%A510%E4%B8%BA%E5%BA%95%EF%BC%89+%5C%5C)

意思是，正确类和错误类的误差等于7就够了，损失不想要继续更新参数让他们的误差越来越大。 实际代码的过程中，一般取![[公式]](https://www.zhihu.com/equation?tex=%5Cvarepsilon%3D0.1)即可。

#### 参考

https://zhuanlan.zhihu.com/p/343807710

https://www.cv-foundation.org/openaccess/content_cvpr_2016/papers/Szegedy_Rethinking_the_Inception_CVPR_2016_paper.pdf

http://openaccess.thecvf.com/content_CVPR_2019/papers/He_Bag_of_Tricks_for_Image_Classification_with_Convolutional_Neural_Networks_CVPR_2019_paper.pdf



#### PS：

label smoothing在人脸任务上是负提升，具体可以参看王峰的相关工作

https://zhuanlan.zhihu.com/p/302843504