#### Tschannen, M., Mustafa, B., & Houlsby, N. (2023). CLIPPO: Image-and-Language Understanding From Pixels Only. In *Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition* (pp. 11006-11017).



---

#### 1. Motivation

<img src="2023 CLIPPO.assets/image-20230926204347949.png" alt="image-20230926204347949" style="zoom:67%;" />

Unification是多模态发展的趋势。

CLIP不同部分可能需要dataset-specific，task-specific的预训练，而且需要modality-specific的initial convolutions，tokenization algorithms，input embedding tables。这大大增加了工程复杂性

作者提出把所有modal data渲染成RGB，输入一个ViT作对比训练（大大减少了模型参数）



---

#### 2. Methods

