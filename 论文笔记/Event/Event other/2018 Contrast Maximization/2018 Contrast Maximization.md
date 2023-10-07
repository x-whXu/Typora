#### A Unifying Contrast Maximization Framework for Event Cameras, with Applications to Motion, Depth, and Optical Flow Estimation

------

#### 1. Motivation

a）当没有additional data时（比如grayscale images），**“从Event data中提取信息” 等同于 “寻找Event data之间的data association”**。

b）Event data association：相机相对物体移动时，moving edges在图像平面上形成point trajectories，**作者认为Event data就是沿着该point trajectories触发的**。

c）因此，可以反过来推导，利用Event data association，估计出moving edges的point trajectories，以帮助完成**motion, depth and optical flow estimation**。

------



#### 2. Methods

##### 2.1 什么是Optical Flow？

 - <font color=Crimson>**optical flow就是velocity vector/偏移量**</font>

 - optical flow是在无穷小的时间内测量的。因此，point trajectories近似直线，可以由平移公式描述：
   $$
   \mathbf{x} (t)=\mathbf{x} (0)+\mathbf{v} t,x\doteq (x,y)^{T}
   $$



##### 2.2 Contrast Maximization Framework for Optical Flow Estimation

a）根据平移motion model和candidate velocity vector，warp所有Event到$t_{ref}$:
$$
\mathbf{x} '_{k} =\mathbf{x} _{k}-(t_{k}-t_{ref}  )\mathbf{v } 
$$
b）对于每个pixel location $x$，**求和**所有warp到该location的Event的polarity（沿point trajectories求和Event），得到histogram of warped events **H**
$$
H(\mathbf{x};\mathbf{v})\doteq \sum_{k=1}^{N_{e} }p_{k}\delta (\mathbf{x}-\mathbf{x'_{k} }  )
$$
​	$	\delta(·)$是冲激函数

c）使用 梯度上升或牛顿法 最大化**H**的空间方差（方差越大，Contrast越大，清晰度越好，velocity vector估计得越准确）

d）搜索出的最佳velocity vector就是Optical Flow Estimation结果

<img src="2018 Contrast Maximization.assets/image-20230903215229365.png" alt="image-20230903215229365" style="zoom:50%;" />

左图是velocity vector **v** 的搜索图，右图是左图中的三个candidate velocity vector，可见optimal velocity vector $\theta _{2} $对比度最大，最清晰

