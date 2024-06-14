# ClassifyMill
对Mill工况故障数据分类
## 1.主线逻辑(难点：数据集小，易过拟合)
### 方案1
1. 一维向量使用STFT转二维时频图；(数据基本为正弦波)
2. 用预训练模型,冻结VGG16用于提取图片特征，使用DeepForest作为分类器，中间夹池化和展开；
  - 对于DeepForest的权重选择策略使用随机搜索；
  - DeepForest训练完后，解冻与DeepForest较近的两层VGG16的卷积层；
### 方案2
1. 一维向量直接作为训练数据；(考虑在方案3中体现尽可能保存原始信息的部分)
2. 直接使用RiLSTM训练；
  - 权重/层级的正则化；
  - 训练停止机制为vail的loss曲线与train的loss曲线相交时；
### 方案3
- 使用方案2与方案1的模型做集成学习，两者并行训练，最后结果加权求和；( 训练停止机制依然为vail的loss曲线与train的loss曲线相交时；)
## 2.anconda环境
打包环境
conda env export > environment.yml

加载环境
conda env create -f environment.yml

## 3.突出点
## 4.未完成事项
- 原始数据的作注；(2024/6/6)
