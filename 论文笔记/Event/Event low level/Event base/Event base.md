#### 1. Event principle

- 对于每个pixel，每当Brightness的log intensity变化大于threshold时，便记录一个Event（x, y, t, p）
- reset，将当前当前intensity作为下次比较的对象



---

#### 2. Event mathematical model

- 极性：$\sigma$
- threshold：$c$
- $\mathbf{L}_{xy}(t)$：(x, y) 位置 t 时刻的瞬时intensity
- $t_{ref}$是上一次触发的时间
- ${\LARGE \tau  } (d,c)$是截断函数

<img src="../../../论文笔记/Event other/2019 EDI/2019 EDI.assets/image-20230915173332513.png" alt="image-20230915173332513" style="zoom: 67%;" />                                <img src="Event base.assets/image-20230915173245129.png" alt="image-20230915173245129" style="zoom: 67%;" />                             

最终，记录Event data四元组（$x,y,t,\sigma$）



---

#### 3. Event cameras优点

1. **高时间分辨率：**每个像素独立工作，无需等待全局曝光时间，Event一触发就传输
   - 可以捕捉高速移动，不易像frame-based cameras产生**动态模糊**
2. **低延迟：**无需等待全局曝光时间
3. **低功耗：**Event只来自发生Change的pixel，不记录冗余
4. **高动态范围：**每个pixel的感光器以对数尺度运行

适用于HDR（low light）、high speed、edge-case scenarios环境



---

#### 3. Event的Representation

##### 3.1 Event count map（ECM）：

<img src="Event base.assets/image-20230917163002332.png" alt="image-20230917163002332" style="zoom:50%;" />

- Kronecker delta function $\delta(x,y)$：$x=y$ 时为1，否则为0
- $W$是time window，$N$是期间发生的event总数

因此，最终ECM$\in \mathbb{R} ^{H\times W\times2} $，2 channel分别表示time window期间 (x, y) 位置上positive和negative event的**计数**。



##### 3.2 Time surfaces（TS）：

<img src="Event base.assets/image-20230917163611046.png" alt="image-20230917163611046" style="zoom: 50%;" />

因此，最终TS$\in \mathbb{R} ^{H\times W\times2} $，2 channel分别表示time window期间 (x, y) 位置上positive和negative**最新**的Event**时间戳**。

TS比ECM考虑了temporal information



##### 3.3 6-channel representation

最终为$\mathbb{R} ^{H\times W\times6} $，其中2个channel为ECM，4个channel分别表示time window期间 (x, y) 位置上positive和negative的Event**时间戳**的均值和标准差

比TS考虑了Event沿时间分布，而不只是最新Event的时间戳



##### 3.4 Voxel

a)  将stream of event按每N个一组进行划分

b)  按该组最大时间差ΔT均匀量化为B (10) 份

- 把 $t{i}$ 从 $[t_{N-1},t_{0}]$ normalize到 $[0.B-1]$ 范围得到 $t{i}^{*}$
- 根据 $t{i}^{*}$ ，每个Event将极性贡献到最近的两个量化电平上

<img src="Event base.assets/image-20230917165059405.png" alt="image-20230917165059405" style="zoom:50%;" />

<img src="Event base.assets/image-20230917165114281.png" alt="image-20230917165114281" style="zoom:50%;" />
