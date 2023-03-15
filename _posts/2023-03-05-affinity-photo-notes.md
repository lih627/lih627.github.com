---
layout: article
title: Affinity Photo 笔记[WIP]
tags: tools
---

记录我学习 affinity photo 的过程. 
目前, 我主要通过 affinity photo 来处理 raw 图片, 因为在工作后, Lightroom 学生版没有办法继续使用. 
Affinity photo 兼顾 LR + PS 的功能, 对于照片的管理, 使用 bridge 存放到 NAS中, 这是后话. 

<!--more-->

# 在进入照片角色之前

Affinity photo 有四种模式, 常用的是照片角色(photo persona)和开发角色(develop persona). 
打开 raw 文件, affinity photo 会自动进入开发角色, 在开发角色中, 可以对原始图片做一些基本的处理, 例如调整对比度, 清晰度, 矫正畸变等.
注意修图过程中, 不应该把所有像对图片的更改都在开发角色完成, 只需要保证 **No clipping in a histogram**. 即图片没有丢失高光和阴影细节.
然后切换到 photo persona. 
一旦从 develop person 切换到 photo person, 将再也无法回到 develop persona 的原始状态, 因为这是破坏性调整(destructive edit).
在修图过程中要尽可能避免这一点.
例如, 图片黑白化不一定要在develop persona实现, 而是在 photo persona, 通过添加一个 adjustment layer实现, 添加 layer 是 non-destructive edit.

  
## 照片角色

### 图层(Layers)

打开的照片, 在 Layers中显示为 Background(Pixel), Pixel指像素图层,由于图层是按照一定顺序排列, 像素图层可以遮挡住它下面的图层. 选中图层,右键点击 duplicate 可以拷贝一份副本.

#### Adjustment Layers

>Layers are non-destructive which means we can turn them off and even delete them. :)

可以当前像素图层上添加的调整图层, 与像素图层不同的一点是, 调整图层不会覆盖下方的图层, 而是对下方所有图层的显示结果加一些修改. 我目前发现有两种方式可以添加: 点击 Layers 旁边的 Adjustment, 或者layer导航栏最下方的圆形图标. 如下图所示:

![Add adjustment layers in affinity photo](/imgs//affinity-photo-tools/add-adjustment-layers.png){:height="50%" width="50%"} 

调整图层非常多,初学者只需要掌握少数几个.

###### Levels Adjustment

![levels layer](/imgs/affinity-photo-tools/levels-layer.png){:height="50%" width="50%"} 

用来截断亮度. 当前状态 RGB Master 表示对明度进行截断.
点击 Master 可以选择对R/G/B单独一个通道截断. 可是尝试向右移动Black Level的滑块, 意味着明度小于对应值的像素都会被截断成0. 画面变暗. White Leve同理. Gamma 表示 Gamma-Compensation function `x ^ (1 / gamma)` 含义是:

1. 对每个像素明度乘补偿系数
2. 补偿后结果截断到 `[0, 255]`

因此 gamma 大于 1, 明度整体降低, 反之变亮. Level调整图层结束后直接关闭就好. 可在Layers下面看到添加并调好参数的level 图层. Opacity 表示该图层影响的强度. 调整为 0% 等价于删除对应图层,

###### Vibrance Adjustment

![vibrance layer](/imgs/affinity-photo-tools/vibrance-layer.png){:height="50%" width="50%"}

> Saturation intensifies all the colors in your images.
>
> Vibrance is more specific and its effect is focused on the mid-tones of an image.

如图, 包含 vibrance 和 saturation 两个滑块. 其实对应的是鲜艳度和饱和度, saturation 对所有颜色进行增强或衰减, 但 vibrance只针对中间色调. 所以多数情况使用vibrance滑块即可. 对初学者需要注意的是: **这个layer不要用来生成黑白照片, 黑白照片使用 black&white adjustment.**

##### Black & White Adjustment

![black and white layer](/imgs/affinity-photo-tools/black-white-layer.png){:height="50%" width="50%"}

显示图像上的不同颜色在黑白下的明暗程度, 例如可以吧红色部分变暗或者变亮. 在这种模式下, 点击 picker, 然后点击图片, 鼠标会变成一个尺子, 按住鼠标选择想要变亮/暗的位置, 然后想左右拉动鼠标, 就会自动向左右移动受影响颜色的滑块. Opacity 也可以用于此 layer, 让图片重新有色彩.

#### 其他重要操作:

**Ground/UnGrounp**:

1. Shift + 点击头尾全选图层
2. Cmd + 点击想要合成的图层
点击 Grounp layers 即可

**Merge Visible**:

这个操作**非常重要**, 是将多个被勾选的图层合并成一个**像素图层**. 例如勾选原始的像素图层+所有调整图层, `Cmd+Opt+Shift+E` 可以将更改生成一个新的像素图层.

**Fit image to the available preview area**

双击 Background Layer 可以直接让图片适合当前的可视区域.

#### Dive into Layers

〉[Best Layers Advice For Beginners: Affinity Photo Course(lesson 5)](https://www.youtube.com/watch?v=TJSZL-bGyxQ)

View->Studio->layers 可以可视化 layer studio. Background 是像素图层, 通常覆盖整个画面, 但存在像素缺失的区域, 被称作 Transparent Area. 像素非透明区域图层会遮盖住下面的图层. 一些注意点:

- 图层的顺序十分重要, 例如调整图层实际上是对其下面所有图层做数学上的计算, 来达到设置的效果.
- 图层被用来做 non-destructive op. 例如, 使用 Healing Brush Tool 时, 先新建像素图层, 在笔刷工具选择作用范围 'Current layer & Below', 可以在当前空白像素图层上, 绘制像素, 达到移除物体的效果.
- 新添加的layer最好使用一个有意义的名字(双击layer即可添加名字)
- 要学会使用Grounp将图层合理分组. 例如按照图层的效果
- 对于调整图层, 右键 -> Mask to Below 图层的效果会仅作用于其下的第一个图层. 或者鼠标按住拖动调整图层到像素图层, 当像素图层变成蓝色框时松手.
- 对于 Grounp 内, 调整图层的作用域是同一个 Group 并在它下面的图层.
- 图层Opacity用来表示作用强度, 比如对于 S-Cruve, 可以通过Opacity来调整对比度, 而不是再 refine 曲线.

**Blending**:

通常, 混合模式时Normal. 例如对于风景照片的S取消, 除了Opacity, 可以再加上 soft light的混合模式, 后者会同事提高色彩饱和度.

**Layer Effects(fx图标)**
有个更多的图层效果, 例如可以添加阴影, 比如对于只有文字的图层.

### Essential Tools

〉 **Don't** try to learn **ALL**  the tools. Learn esstntial tools.

![Photo persona tools](/imgs/affinity-photo-tools/photo-persona-tools.png){:height="10%" width="10%"}

在照片角色的左栏是工具栏, 双击后可以把它从主界面分离, 如上图. View->Custom tools 可以定制化工具栏. 把鼠标放到工具图标上, 会显示工具的名字和快捷键. 工具右下方灰色小三角表示这是一个工具组, 点击可以展开.

#### View Too [H]

鼠标会变成手的形状, 点按可以让显示区域在画布上移动. 适合在100%显示的时候, 拖动显示区域以关注细节. 



#### Move Tool [V]

![move tool](/imgs/affinity-photo-tools/move-tool.jpeg){:height="50%" width="50%"}

打开后会有一些控制点, 用来调整目标的大小. 目前是**x** 的状态, 因为 layer -> background layers 显示锁定的状态. 点击layer对应的🔒解锁即可. 解锁后, 可以通过新状态来调整形状, 也可以通过按住鼠标拖动移动目标.

#### Crop Tool [C]

用来裁剪图片, non-destructive op.

- Darken 表示被舍弃的区域变暗, Reveal 可以可视化被裁剪掉的的区域(所以 non-destructive)

#### Paintbrush Tool [B]

brush-based tool 基本都有相同的模块, 建议开启 preferences -> show brush previews, 它可以在画布上预览笔刷. 笔刷工具都是 destructive tool, 最好 `Shit+Cmd+N` 在新建的图层上绘制.

![brush-tool](/imgs//affinity-photo-tools/brush-opacity-flow-hardness.png){:height="50%" width="50%"}

通常, 一条线由 N 个笔画构成:

- opacity: 控制这条线最大的不透明度. 
- flow: 控制单条笔画的不透明度, 比如 flow = 100, 在绘制一条线的时候, 无论如何重合, 线条的不透明度都是opacity.
- width: 控制使用笔触的粗细, 快捷键 '[' 和 ‘]', 通过快捷键方便直接在画布看大小.
- hardness: 控制笔画边缘的硬度, 越低边缘虚化越强.

**如何调整笔画的颜色**:

通过 Swatches 或 Colour studio选取颜色

![brush-color](/imgs/affinity-photo-tools/color-studio.png){:height="50%" width="50%"}

- Swatches studio: 选取色块, 有一些配置, 比如 Grey/Colours/Apple等.
- Colour studio: 有很多种模式, wheel/slider 等.


#### Clone[S] & Healing[J] Brush

用来去掉照片上不要想的目标.

Clone[S] Brush Tool: 印章图案

1. 新建像素图层
2. 注意选择采样区域为 `current layer & below`
3. 设定采样区域, Opt + 点选
4. 找到想要被覆盖的区域, 鼠标涂抹即可

Clone brush tool 使用时注意不断选择合适的采样点.

Healing[J] Brush Tool: 创可贴图案, 与 Clone brush 不同的是, 它会尝试混合当前区域与采样区域, 而不是生硬的覆盖.

### Filters & Live Filters

#### Filters (destructive)

与 adjustment layer 不同, Filter 是 destructive edit, 作用于像素图层或者 **Mask layer**. 在 菜单栏->Filters 打开, 应用于当前选中的像素图层. Filter会提供多种预览选项, 一旦被应用到对应的图层, 将无法恢复到原来的状态.

 如果选中一个调整图层, 添加filter, 将看不到效果, 因为调整图层没有像素. 调整图层作用范围可以通过 Opt+鼠标左键 点击对应的图层显示, 通常是全白色. Filter 可以和 layer mask 结合, 更加动态改变调整图层对下面元素的影响. 例如:

 首先通过 rectangle marquee tool[M] 在调整图成选择矩形框. Cmd+I 可以反转像素, 对调整图层来说, 矩形框内的像素将不会被处理. 此时 Opt+鼠标左键选择调整图层, 白色画布中出现黑色色块.

 ![layer-mask](/imgs/affinity-photo-tools/layer-mask.png)

可以将Filter作用于此时的调整图层, 效果如下图, 滤镜将调整图层 {0, 255} 像素分布变为 [0, 255], 调整图层作用强度将是非线性变化的:

![filter-layer-mask](/imgs/affinity-photo-tools/filter-layer-mask.jpeg)

#### Live Filters (non-destructive)

> Live Filers = Filter + Adjustment Layer

![live-filter-layer](/imgs/affinity-photo-tools/live-filter-layer.png)

通过 菜单栏->Layer->New Live Filter Layer 添加, 他会附着在所选定的图层下面. 与普通的 filter 不同点:

- Live filter 在设置的时候不会有取消项.
- 对应的图层有Opacity选项
- 并不是所有的Filter都有对应的 live filter

#### 如何防止破坏性修图

**Shift+Opt+Cmd+E** 创建一个合并的增强像素图层, 在它上面进行破坏性修图.

### Masks

Mask其实就是图层的作用范围.

调整图层 **Opt+左键点选** 就会显示Mask, 对于调整图层, Mask默认时整个图层. Retangular marquee tool[M] 选择举行, Cmd+I 可以反转作用像素. 可以通过菜单栏->Select->Deselect 取消选择矩形框.

可以用 retangular marquee tool[M] 选择调整图层一般区域, 然后 flood fill tool[G] 填入需要的灰度控制对应区域的强度. 如下图

![flood-fill-with-mask](/imgs/affinity-photo-tools/flood-fill-with-mask.jpeg){:height="50%" width="50%"}

Mask 如何使用:
- 对于风景照片, 想增加特定区域对比度, 加入调整图层, Mask设置为全黑, 然后用笔刷在图层上针对想要调整的部分, 刷上白色. 注意调整笔刷hardness, opacity 和 flow.
- 菜单栏->Select->Select Sampled Color, 调整好弹出的tolerance滑块, 然后再背景图层选择想要调整的颜色. 然后点击Apply 可以发现生成多个mask.(如果没有打开菜单栏->View->Show Pixel Selection). 然后选中调整图层, 用笔刷绘制, 就可以针对对应的Mask增加效果.
- Selection 是暂时的, 但是Mask 可以保存, 在 Channel 里面可以找到 Pixel Selection, 右键 Create Spare Channel 可以将mask保存为channel, 起一个好名字. 然后右键-> Load to pixel selection 就可以重新加载对应的masks
- 先选 mask, 然后添加的 adjustment layer 将只作用于mask, 除非 Deselection.


![channel](/imgs/affinity-photo-tools/channel.png){:height="50%" width="50%"}




### References

- 我目前根据Youtube的视频教程学习, [Affinity Photo for Beginers](https://www.youtube.com/playlist?list=PLUyadHduIq2f6YMErTU9_P5CIDIo15yq1)
- Question on the Gamma(mid-tone) value in levels adjustment layer. [Link](https://community.adobe.com/t5/photoshop-ecosystem-discussions/question-on-the-gamma-mid-tone-value-in-levels-adjustment-layer/td-p/10869779)
- [如何理解笔刷工具的 flow 和 opacity?](https://forum.affinity.serif.com/index.php?/topic/20014-helpful-explanation-of-the-difference-between-brush-flow-and-brush-opacity/)
 