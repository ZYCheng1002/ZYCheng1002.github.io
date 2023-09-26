---
layout: page
title:  "FAST LIO"
subtitle: "FAST LIO NOTED"
date:   2023-09-26 20:25:21 +0530
categories: ["general"]
---

ieskf 初始化  
状态量按照代码中的顺序[位置, 姿态, 外参R, 外参t, 速度, 陀螺仪零偏, 加速度计零偏, 重力],表示为
$$  x \doteq \begin{bmatrix} p_{GI}^T & R_{GI}^T & R_{IL}^T & t_{IL}^T & v_{GI}^T & b_g^T & b_a^T & g_G^T \end{bmatrix}^T $$
其中$R_{GI}$,$R_{IL}$为李代数$SO(3)$]

运动输入参数为陀螺仪和加速度计,表示为:
$$  u \doteq \begin{bmatrix} w_{m}^T & a_{m}^T \end{bmatrix}^T $$
测量噪声表示为:
$$  w \doteq \begin{bmatrix} n_{g}^T & n_{a}^T
& n_{bg}^T & n_{ba}^T \end{bmatrix}^T $$

运动方程:
连续时间状态变量导数相对于观测量的关系
$$\dot{p_t}=v_t$$
$$\dot{R}=R(w_{m_t}-b_{g_t}-n_{t}) $$
$$\dot{v_t} = R_t(a_{m_t} - b_{a_t}-n_{a_t}) + g_t$$
$$\dot{b_g}=n_{bg_{i}}$$
$$\dot{b_a}=n_{ba_{i}}$$
$$\dot{g}=0$$