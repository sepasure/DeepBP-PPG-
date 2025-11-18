# 🏥 DeepBP: 基于 PPG 信号的深度学习无创连续血压预测系统

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-1.12%2B-orange)](https://pytorch.org/)
[![License](https://img.shields.io/badge/license-MIT-green)](./LICENSE)

> **项目简介**：本项目是一个基于深度学习的医疗信号处理系统，旨在利用光电容积脉搏波（PPG）信号实现无创、连续、高精度的血压（SBP/DBP）预测。核心模型采用 **1D-CNN + Bi-LSTM** 架构，并在 UCI/MIMIC-II 数据集上验证，部分样本预测误差符合 AAMI 医疗标准（MAE < 5 mmHg）。

---

## 🚀 核心功能与亮点

* **📈 深度特征提取**：结合 **CNN**（提取波形形态学特征）与 **Bi-LSTM**（捕捉心动周期时序依赖），有效处理 PPG 信号的非线性特征。
* **🧠 破解“平均值陷阱”**：通过引入 **标签归一化 (Label Normalization)** 和 **动态学习率调度**，解决了回归任务中模型倾向于预测均值的痛点，大幅提升了预测精度。
* **⚡ 信号预处理流水线**：集成了带通滤波（Butterworth）、异常值去除和 Z-Score 标准化，有效抗击工频干扰和基线漂移。
* **📱 轻量化设计**：支持 PyTorch 动态量化（Dynamic Quantization），模型权重可压缩至 INT8 格式，适配移动端/嵌入式部署。

---

## 🏗️ 模型架构

```mermaid
graph LR
    A[原始 PPG 信号] --> B(预处理: 滤波+标准化)
    B --> C[1D-CNN 层]
    C -->|提取形态特征| D[Bi-LSTM 层]
    D -->|提取时序特征| E[全连接层 FC]
    E --> F[输出: SBP / DBP]
