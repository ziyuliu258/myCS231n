# Data-driven Methods

## KNN

### Distance Metrics

#### L1 Distance (Manhattan Distance) (Find the nearest neighbor)

$d_1(I_1,I_2)=\displaystyle\sum_p \left| I_1^p-I_2^p \right|$

其中 $p$ 就是图像的对应矩阵中的每一个元素。

#### L2 (Euclidian) Distance

$d_2(I_1,I_2)=\sqrt{\displaystyle\sum_p(I_1^p-I_2^p)^2}$
![Fig. 1](.\notes_images\image.png)
> - $L1$对于坐标轴的变化敏感（以上的方形会变化），而$L2$则不。所以当输入特征的向量中某些值有特殊（具体的）意义，则可能采取前者会好。
> - 同理，$L1$的决策边界更倾向于和坐标轴同向，而后者的决策边界更自然。

### K-Nearest-Neighbor

就是找到$K$个与之相邻最近的点，然后根据这几个点的标签按分类投票得出结果。其Distance Metrics可以自行选择。

_特点：K越大，决策边界越平滑，对噪音的鲁棒性就更高；整体上对噪声较敏感；training时间短（$O(1)$），testing时间长($O(N)$)，而理想的算法是training时间长（训练充分），testing时间短（应用便捷）_

**为什么图像识别中不常用这一算法？**

> - testing time太长。
>
> - 视觉相似度不太适合用距离度量来表示。
>
> - 维度灾难（The Curse of the Dimensionality）：KNN需要数据在超平面上分布尽可能**稠密**才可能保证你的近邻和你实际相距不远，但这对于多维的数据来说会带来指数级的运算量增长，负担很重。
>
>   ![Fig. 2](.\notes_images\image-20250217122104928.png)

$K$和距离度量都是所谓**超参数 (Hyperparameters)**，你需要设定，而不能学习它们。

> 如何理解图像？**高维向量** or **高维超平面上的点**

## Training Strategies

- 划分`train` `valid` `test`三个集合，并确保`valid` `test`不重叠。
- **Cross Validation**，适用于小数据集，在**Deep Learning**上不常见（太消耗算力）。先划分训练集和测试集，然后将训练集分成好几个**folds**，每个**fold**轮流当验证集。

## Linear Classifier

![Fig. 3](.\notes_images\image-20250218173937843.png)

**KNN**没有参数，而**Linear Classifier**则有参数，属于**parametric approach**。

或者说相当于一种超平面划分。每一个图像好比是这个超平面直线上的一个点

![Fig. 4](.\notes_images\image-20250218175946610.png)