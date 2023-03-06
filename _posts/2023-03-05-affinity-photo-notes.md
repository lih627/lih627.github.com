---
layout: article
title: Affinity Photo 笔记[WIP]
tags: tools
---

记录我学习 affinity photo 的过程. 
目前, 我主要通过 affinity photo 来处理 raw 图片, 因为在工作后, Lightroom 学生版没有办法继续使用. 
Affinity photo 兼顾 LR + PS 的功能, 对于照片的管理, 使用 bridge 存放到 NAS中, 这是后话. 

<!--more-->

### 在进入照片角色之前

Affinity photo 有四种模式, 常用的是照片角色(photo persona)和开发角色(develop persona). 
打开 raw 文件, affinity photo 会自动进入开发角色, 在开发角色中, 可以对原始图片做一些基本的处理, 例如调整对比度, 清晰度, 矫正畸变等.
注意修图过程中, 不应该把所有像对图片的更改都在开发角色完成, 只需要保证 **No clipping in a histogram**. 即图片没有丢失高光和阴影细节.
然后切换到 photo persona. 
一旦从 develop person 切换到 photo person, 将再也无法回到 develop persona 的原始状态, 因为这是破坏性调整(destructive edit).
在修图过程中要尽可能避免这一点.
例如, 图片黑白化不一定要在develop persona实现, 而是在 photo persona, 通过添加一个 adjustment layer实现, 添加 layer 是 non-destructive edit.

  
### 照片角色

#### 图层(Layers)

打开的照片, 在 Layers中显示为 Background(Pixel), Pixel指像素图层,由于图层是按照一定顺序排列, 像素图层可以遮挡住它下面的图层. 选中图层,右键点击 duplicate 可以拷贝一份副本.

#### Adjustment Layers

>Layers are non-destructive which means we can turn them off and even delete them. :)

可以当前像素图层上添加的调整图层, 与像素图层不同的一点是, 调整图层不会覆盖下方的图层, 而是对下方所有图层的显示结果加一些修改. 我目前发现有两种方式可以添加: 点击 Layers 旁边的 Adjustment, 或者layer导航栏最下方的圆形图标. 如下图所示:

![Add adjustment layers in affinity photo](/imgs//affinity%20photo%20tools/add-adjustment-layers.png){:height="50%" width="50%"} 

调整图层非常多,初学者只需要掌握少数几个.

##### Levels Adjustment

![levels layer](/imgs/affinity%20photo%20tools/levels-layer.png){:height="50%" width="50%"} 

用来截断亮度. 当前状态 RGB Master 表示对明度进行截断.
点击 Master 可以选择对R/G/B单独一个通道截断. 可是尝试向右移动Black Level的滑块, 意味着明度小于对应值的像素都会被截断成0. 画面变暗. White Leve同理. Gamma 表示 Gamma-Compensation function `x ^ (1 / gamma)` 含义是:

1. 对每个像素明度乘补偿系数
2. 补偿后结果截断到 `[0, 255]`

因此 gamma 大于 1, 明度整体降低, 反之变亮. Level调整图层结束后直接关闭就好. 可在Layers下面看到添加并调好参数的level 图层. Opacity 表示该图层影响的强度. 调整为 0% 等价于删除对应图层,

##### Vibrance Adjustment

![vibrance layer](/imgs/affinity%20photo%20tools/vibrance-layer.png){:height="50%" width="50%"}

> Saturation intensifies all the colors in your images.
>
> Vibrance is more specific and its effect is focused on the mid-tones of an image.

如图, 包含 vibrance 和 saturation 两个滑块. 其实对应的是鲜艳度和饱和度, saturation 对所有颜色进行增强或衰减, 但 vibrance只针对中间色调. 所以多数情况使用vibrance滑块即可. 对初学者需要注意的是: **这个layer不要用来生成黑白照片, 黑白照片使用 black&white adjustment.**

##### Black & White Adjustment

![black and white layer](/imgs/affinity%20photo%20tools/black-white-layer.png){:height="50%" width="50%"}

显示图像上的不同颜色在黑白下的明暗程度, 例如可以吧红色部分变暗或者变亮. 在这种模式下, 点击 picker, 然后点击图片, 鼠标会变成一个尺子, 按住鼠标选择想要变亮/暗的位置, 然后想左右拉动鼠标, 就会自动向左右移动受影响颜色的滑块. Opacity 也可以用于此 layer, 让图片重新有色彩.

##### 其他重要操作:

**Ground/UnGrounp**:
1. Shift + 点击头尾全选图层
2. Cmd + 点击想要合成的图层
点击 Grounp layers 即可

**Merge Visible**:
这个操作**非常重要**, 是将多个被勾选的图层合并成一个**像素图层**. 例如勾选原始的像素图层+所有调整图层, `Cmd+Opt+Shift+E` 可以将更改生成一个新的像素图层.

#### Essential Tools

![Photo persona tools](/imgs/affinity%20photo%20tools/photo-persona-tools.png){:height="50%" width="50%"}

在照片角色的左栏是工具栏, 双击后可以把它从主界面分离, 如上图.


### References

- 我目前根据Youtube的视频教程学习, [Affinity Photo for Beginers](https://www.youtube.com/playlist?list=PLUyadHduIq2f6YMErTU9_P5CIDIo15yq1)
- Question on the Gamma(mid-tone) value in levels adjustment layer. [Link](https://community.adobe.com/t5/photoshop-ecosystem-discussions/question-on-the-gamma-mid-tone-value-in-levels-adjustment-layer/td-p/10869779)
