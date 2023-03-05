---
layout: article
title: Affinity Photo 笔记[WIP]
tags: tools
---

记录我学习 affinity photo 的过程. 目前, 我主要通过 affinity photo 来处理 raw 图片, 因为在工作后, Lightroom 学生版没有办法继续使用. Affinity photo 兼顾 LR + PS 的功能, 对于照片的管理, 使用 bridge 存放到 NAS中, 这是后话. 

<!--more-->

### 在进入照片角色之前

Affinity photo 有四种模式, 常用的是照片角色(photo persona)和开发角色(develop persona). 打开 raw 文件, affinity photo 会自动进入开发角色, 在开发角色中, 可以对原始图片做一些基本的处理, 例如调整对比度, 清晰度, 矫正畸变等. 注意修图过程中, 不应该把所有像对图片的更改都在开发角色完成, 只需要保证 **No clipping in a histogram**. 即图片没有丢失高光和阴影细节. 然后切换到 photo persona. 一旦从 develop person 切换到 photo person, 将再也无法回到 develop persona 的原始状态, 因为这是破坏性调整(destructive edit). 在修图过程中要尽可能避免这一点. 例如, 图片黑白化不一定要在develop persona实现, 而是在 photo persona, 通过添加一个 adjustment layer实现, 添加 layer 是 non-destructive edit.


### References

- 我目前根据Youtube的视频教程学习, [Affinity Photo for Beginers](https://www.youtube.com/playlist?list=PLUyadHduIq2f6YMErTU9_P5CIDIo15yq1)
