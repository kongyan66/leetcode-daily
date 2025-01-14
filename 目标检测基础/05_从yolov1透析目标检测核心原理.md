# 从yolov1透析目标检测核心原理

## 1.前言

笔者也看了很多关于YOLO系列解读，大多数讲解YOLO网络结构和代码，也出现很多很好的教程，但笔者认这并没有深入阐明检测的本质，故笔者以YOLO为引子去洞悉检测网络究竟为何能实现检测，一张图片送入检测网络中究竟经历了什么？网络最终得到的是什么？后续又做了什么？我想只有把这些问题弄懂，我们才算真正进入检测原理的核心世界，更大点说，如果把图像换成其他数据，我们也以这种思维去思考，我们对深度学习的核心也会有更深刻的理解。本文着重于对检测思想的把握，代码部分会作为次要分析。

—2021.11.26

## 2.基础原理



## 3.网络结构

24 卷积层+2 全连接层 。YOLO v1没有Neck，Backbone是GoogLeNet，属于Dense Prediction

<img src="https://raw.githubusercontent.com/kongyan66/Img-for-md/master/img/v2-3af308f7096bda4c621c077302b90533_r.jpg" alt="preview" style="zoom:80%;" />

## 4.输出解析

### **损失函数**

看懂一个网络的输出，看懂它的损失函数就好，下面就是其损失函数：

<img src="https://raw.githubusercontent.com/kongyan66/Img-for-md/master/img/v2-f81c565d41b681263689626331325ac3_r.jpg" alt="preview" style="zoom:80%;" />

> 前2行计算前景的geo_loss，即位置损失， $\lambda_{coord}$表示位置损失惩罚系数
>
> 第3行计算前景的confidence_loss，统称置信度损失。
>
> 第4行计算背景的confidence_loss，$\lambda_{noobj}$表示背景置信度损失惩罚系数。
>
> 第5行计算分类损失class_loss，即分类损失。
>

仔细观察下损失函数的求和符号的上下限，我们可以看出需要对每个bbox计算**位置损失**、**前景的置信度损失**以及**背景的置信度损失**，对每个一个网格计算**分类损失**（这也就说明一个网格只能预测一类目标，该网格的两个bbox的类别必然相同）。

### **标签的输出**

有什么样的标注，就有什么样的网络输出。如果说标注是一个模子，初始的网络就是一坨稀泥，在训练过程中，这坨泥巴越捏越像模子，最终无限接近（完全相等当然是不可能的）。所以我们需要先设计好一个模子的样子，网络的训练才有参考。

那么接下来我们就需要清晰的理解输出参数的计算过程，上面提到了



### 网络的输出



## 5.代码结构

![image-20221003193712272](https://raw.githubusercontent.com/kongyan66/Img-for-md/master/img/image-20221003193712272.png)

## 6.代码理解



## 7.总结

致谢



