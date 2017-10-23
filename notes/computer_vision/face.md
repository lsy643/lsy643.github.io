---
layout: page
mathjax: true
permalink: /notes/computer_vision/face/
---

Face related algorithms


## Face Alignment
Face alignment is locating semantic facial landmarks such as eyes, nose,
mouth and chin.

Face shape: $$S = [x_1, y_1, ..., x_N_fp, y_N_fp]^T$$

## Face Verification


## Face Recognition

1. face detection
1. face alignment
1. face shape adjustment: 2d and 3d
1. face identification


## 人脸识别与通用识别的区别

1. 人脸为半刚体，容易做对齐
1. 细分类，关注细分类的差异
1. 类别数特别多， 100000+
1. 应用是为ZERO-SHOT
1. 特征对比，更类似于检索，找最相似的人

## 特征

LBP： 纹理特征

深度学习：训练一个分类网络，用进最后分类器之前的特征向量