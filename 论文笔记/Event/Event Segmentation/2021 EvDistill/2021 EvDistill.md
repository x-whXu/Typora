#### Wang, L., Chae, Y., Yoon, S. H., Kim, T. K., & Yoon, K. J. (2021). Evdistill: Asynchronous events to end-task learning via bidirectional reconstruction-guided cross-modal knowledge distillation. In *Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition* (pp. 608-619).



---

#### 1. Motivation

a）Ev-SegNet使用pesudo-labels质量低下

b）无监督学习方法大多是针对low-level

c）E2VID重建video，仍需要video的GT

提出采用cross-modal KD，通过从使用有标记图像数据训练的teacher network中提取知识，在**unlabeled且unpaired**的事件数据上学习student network

**KD直接利用image modal的监督信号，训练出<u>以Event为输入的End-task network</u>，不用制作什么新数据集**

<img src="2021 EvDistill.assets/image-20230917214822849.png" alt="image-20230917214822849" style="zoom:67%;" />



---

#### 2. Methods

##### 2.1 BMR

<img src="2021 EvDistill.assets/image-20230918144715214.png" alt="image-20230918144715214" style="zoom:67%;" />

使用CycleGAN结构，获得unpaired 生成能力



##### 2.2 DA