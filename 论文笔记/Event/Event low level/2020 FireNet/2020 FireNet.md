#### Scheerlinck, C., Rebecq, H., Gehrig, D., Barnes, N., Mahony, R., & Scaramuzza, D. (2020). Fast image reconstruction with an event camera. In *Proceedings of the IEEE/CVF Winter Conference on Applications of Computer Vision* (pp. 156-163).

------

#### 1. Motivation

为了充分利用Event camera低功耗的特点，部署在嵌入式设备、物联网应用，他们提出了一个比E2VID更小（38k vs 10M），更少内存（0.16MB vs 43MB），更少FLOPs（12.6G vs 147.2G），更快（10ms vs 30ms）

<img src="2020 FireNet.assets/image-20230831164836480.png" alt="image-20230831164836480" style="zoom:50%;" />



#### 2. Methods

##### 2.1 Input representation

a)  与E2VID同样，通过trilinear voting，将每个Event的极性贡献给最近的两个temporal bins，得到voxel tensor

b)  将voxel tensor中非零条目normalize成零均值、单位范数，减轻 OFF/ON threshold不同 和 pixel threshold不同的影响



##### 2.2 Model architecture

a）输入的voxel tensor为 H × W × B，temporal bins为5

b）H是 3*3 kernel，16channel，1stride，1pad的Conv2D + ReLU

c）G1,G2是3*3 kernel，16channel，1stride，1pad的Conv2D + ReLU + **GRU**

d）R1就是ResNet的Residual block，两个3*3 kernel，16channel，1stride，1pad的Conv2D，中间有ReLU，两头有skip connection

e）P是1 channel的1*1 Conv2D

<img src="2020 FireNet.assets/image-20230831165427983.png" alt="image-20230831165427983" style="zoom: 67%;" />



##### 2.3 Loss function

与E2VID 2一样：

a）LPIPS loss

b）temporal consistency loss



