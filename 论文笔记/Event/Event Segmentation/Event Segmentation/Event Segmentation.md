#### 1. Object recognition Dataset

##### 1.1 N-MNIST

MNIST的Event版本

将图片显式在LCD上，ATIS放在电机上自动平移

（与现实数据有差别，物体运动受限）



##### 1.2 N-Caltech101

Caltech101的Event版本（101类别的分类数据集）

将图片显式在LCD上，ATIS放在电机上自动平移



##### 1.3 MNIST-DVS

MNIST的Event版本

图片在LCD上平移显式，DVS固定拍摄



##### 1.4 CIFAR10-DVS

CIFAR10的Event版本

图片在LCD上平移显式，DVS固定拍摄



##### 1.5 N-CARS

现实场景拍摄，二元分类数据集：12336张有车Event stream，11693张没车Event stream，均持续100ms





---

#### 2. Semantic segmentation Dataset

##### 2.1 Ev-Seg

为**只以Event作为输入**的semantic segmentation task准备的数据集



a）以DDD17 datast为基础

- DDD17：40个seq，提供同步的**grayscale image**和event data，但是不提供semantic lablels

b）制作过程：

- 在Cityscapes Dataset（需要转为grayscale image），训练一个Model
- trained Model为DDD17其中的6个seq，生成pseudo-labels

c）缺陷：

- pseudo-labels质量低，label正确率有限
- 只能在不太暗，不太亮环境生成pseudo-labels，无法突出Event的优势
- 因为不同数据集domain-shift，多个label被聚合，label粒度低
- DDD17的DAVIS分辨率低



---

#### 3. Related work