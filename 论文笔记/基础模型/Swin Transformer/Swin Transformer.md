### Swin Transformer: Hierarchical Vision Transformer using Shifted Windows

#### 1. Motivation

**VIT存在如下诟病：**

a) 一直对16倍下采样map处理，缺少多尺度特征

b) 对所有patch计算self-attention，随图片大小O(n^2^)复杂度，计算量大

<img src="Swin Transformer.assets/image-20230830135000093.png" alt="image-20230830135000093" style="zoom: 50%;" />

<center>注：灰色是patch（基本单元），红色是window（self-attention范围）</center>

**Swin Transformer的改进：**

a) 只在window内计算self-attention，随图片大小O(n)复杂度，计算量小（利用CNN中“局部冗余（语义相近物体大概率位置相近）”先验）

b) 为了确保全局建模能力，提出*shifted window*来实现cross window connection

<img src="Swin Transformer.assets/image-20230830140401099.png" alt="image-20230830140401099" style="zoom:50%;" />

c) 利用patch merging（类似pooling）得到多尺度特征



​	