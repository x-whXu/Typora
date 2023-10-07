#### Weng, W., Zhang, Y., & Xiong, Z. (2023). Event-Based Blurry Frame Interpolation Under Blind Exposure. In *Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition* (pp. 1588-1598).



---

#### 1. Motivation

##### 1.1 Background

Blurry frame interpolation（BFI）旨在从模糊的低帧率视频中恢复清晰的高帧率视频。



在EDI模型中，简单地假设exposure为已知常数。但是在in the wild时，由于以下原因，曝光时间通常是unknown的：

- 不同video seq曝光时间不一样
- 同一video seq不同frame之间曝光时间不一样
- 帧间还包括data readout时间



面对blind exposure，BFI works很难根据相邻帧估计出exposure time。因此，作者引入Event data辅助：

- 因为**图像的模糊效果是由motion speed和exposure time共同决定的**，所以仅依靠blurry frame不足以估计exposure time。而Event data数量正好record了motion speed信息，可以由此帮助估计出exposure time
- Event data本身高时间分辨率特点，可以帮助FI



---

#### 2. Methods

##### 2.1 Exposure Estimation

##### <font color=Crimson>估计Exposure Time</font>

a）通过对Blurry frame进行dark channel或者Laplacian function操作，来获得一个模糊的Blurry prior（Blurry level），表示模糊程度

b）Event stream以ECM $\in  \mathbb{R} ^{B\times 2 \times H\times W}$的形式作为input

c）Exposure Prior是一个值： $T_{ex} / (T_{ex} + T_{re})$

<img src="2023 Event-based BFI.assets/image-20230910173916967.png" alt="image-20230910173916967" style="zoom:50%;" />



---

##### 2.2 Temporal-exposure Control

##### <font color=Crimson>根据arbitrary timestamp和Exposure Prior作为两个控制系数，调整Event feature</font>

仿照image synthesis的方法框架

<img src="2023 Event-based BFI.assets/image-20230910174204298.png" alt="image-20230910174204298" style="zoom:50%;" />



---

##### 2.3 Sharp Frame Reconstruction

##### <font color=Crimson>根据Controlled <u>Event feauture</u>和Blurry <u>image feature</u>进行<u>align</u>（VI）</font>

a）用KPN（就是Dynamic Conv）进行align

b）

<img src="2023 Event-based BFI.assets/image-20230910174410982.png" alt="image-20230910174410982" style="zoom:67%;" />

c）sharp Feature后续通过一个decoder重建为initial sharp frame，再通过一个UNet细化成final sharp frame



---

##### 2.4 Loss function

a）Laplacian pyramid loss：

<img src="2023 Event-based BFI.assets/image-20230910174816556.png" alt="image-20230910174816556" style="zoom:50%;" />

b）census loss：避免L1 loss的过度约束

<img src="2023 Event-based BFI.assets/image-20230910174847408.png" alt="image-20230910174847408" style="zoom:50%;" />

Dis(·)是soft Hamming distance，Cen(·)是census transform
