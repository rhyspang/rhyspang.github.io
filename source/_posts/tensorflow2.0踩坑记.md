---
title: tensorflow2.0踩坑记
date: 2019-12-16 10:56:03
tags:
---
# 记录使用TensorFlow2.0遇到的问题和解决办法

## Resource not Exist
### 描述
自定义tf keras层继承自`tf.keras.layers.Layer`，自定义模型继承自`tf.keras.Model`，训练使用`model.fit`，报错

```
tensorflow.python.framework.errors_impl.FailedPreconditionError: 2 root error(s) found.
(0) Failed precondition:  Error while reading resource variable _AnonymousVar36 from Container: localhost. This could mean that the variable was uninitialized. Not found: Resource localhost/_AnonymousVar36/N10tensorflow3VarE does not exist.
```
提示某个variable 未初始化
### 解决方案
检查后发现是因为我自定义层的类里有一些变量没有绑定到self上，改后该报错消失

## 梯度为None
### 描述
报错信息
```
ValueError: Variable <tf.Variable 'request_model/context_modelling_layer/mr_dense1/kernel:0' shape=(7, 100) dtype=float32> has `None` for gradient. Please make sure that all of your ops have a gradient defined (i.e. are differentiable). Common ops without gradient: K.argmax, K.round, K.eval.
```
提示说某些variable的gradient为None导致value error。检查后发现模型中某些操作定义并使用了，但和最终计算的loss无关，所以loss对于这些variable没有梯度，去掉这些和最终loss无关的variable后报错消失。

## 初始化静态图内存暴涨
### 描述
将某些layer定义到了call方法里，建静态图时内存占用一直上升，未找到具体原因，将所有layer的初始化移到构造器中初始化后，内存异常的问题解决$\mathbb{R}$
