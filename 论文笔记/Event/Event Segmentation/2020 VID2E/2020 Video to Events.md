#### Gehrig, D., Gehrig, M., Hidalgo-Carrió, J., & Scaramuzza, D. (2020). Video to events: Recycling video datasets for event cameras. In *Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition* (pp. 3586-3595).



---

#### 1. Motivation

Event重建video，并在object recognition（多物体分类），semantic segmentation等下游任务取得优秀结果，表明可以设计高效的End to end算法。

设计End to end算法主要的难题是，object recognition，semantic segmentation等下游任务缺乏labled event dataset。

采用event camera simulators的synthetic data泛化效果很差，所以作者提出一种新的Video to Events。

<img src="2020 Video to Events.assets/image-20230917192315953.png" alt="image-20230917192315953" style="zoom:50%;" />



---

#### 2. Methods

##### 2.1 Overall

a）使用自适应上采样技术（自适应选择帧率），将低帧率视频插帧为高帧率

b）使用事件相机模拟器ESIM来生成Event（正、负极性threshold $C_{p},C_{n}\sim U(0.05,0.5)$ 



##### 2.2 Object Recognition

a）采用N-Caltech101进行评估：

 - N-Caltech101是多类别分类数据集Caltech101的Event版本

b）still image转为video sequence：

 - 将still image放在2D平面上，虚拟相机在平面上进行扫视运动（平移），直接得到高帧率视频，而无需插帧

c）使用在ImageNet预训练的ResNet-34：

<img src="2020 Video to Events.assets/image-20230917202030984.png" alt="image-20230917202030984" style="zoom:67%;" />

- dataset extension指从网上收集额外图片生成Event数据，平衡长尾问题



##### 2.3 Semantic Segmentation

使用Ev-Seg，直接由grayscale video插值生成Event data。与real event data对比效果





