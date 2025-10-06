# ChaosNet-IE - 基于神经网络优化混沌系统的图像加密器

[![English](https://img.shields.io/badge/Language-English-blue)](README.md) [![中文](https://img.shields.io/badge/语言-简体中文-red)](README_CN.md)

> 基于改进 Lorenz 混沌系统 + 神经网络优化的高安全性图像加密方案。

![Python](https://img.shields.io/badge/Python-3.7+-blue.svg) ![OpenCV](https://img.shields.io/badge/OpenCV-4.0+-green.svg) ![NumPy](https://img.shields.io/badge/NumPy-Latest-orange.svg) ![License](https://img.shields.io/badge/License-Academic-red.svg)

## 项目简介
ChaosNet-IE 实现论文《基于神经网络优化混沌系统的图像加密算法》中提出的核心算法：通过改进的 Lorenz 混沌系统生成高质量序列，再经 BP 神经网络优化，结合像素置乱与扩散完成加密。

## 核心特性
- 神经网络参与混沌序列质量提升
- 改进 Lorenz 系统增强随机性
- 双阶段：置乱 + 扩散
- 基于图像内容的 SHA-384 派生初始密钥，密钥敏感
- 加密后图像接近 8.0 熵值，抗统计与差分攻击

## 目录结构
```
ChaosNet-IE/
├── keys/                # 密钥与序列
│   ├── sequences.npz
│   └── initial_values.txt
├── output/              # 结果输出
│   ├── encrypted.png
│   └── decrypted.png
├── encrypt.py           # 加密脚本
├── decrypt.py           # 解密脚本
├── demo.py              # 演示脚本
├── lena.png             # 测试图像
└── README.md / README_CN.md
```

## 快速开始
### 安装依赖
```bash
pip install numpy opencv-python
```
### 一键演示
```bash
python demo.py
```
输出：自动完成加密→解密→统计分析。

### 仅加密
```bash
python encrypt.py
```
生成：`output/encrypted.png`、`keys/sequences.npz`、`keys/initial_values.txt`

### 仅解密
```bash
python decrypt.py
```
生成：`output/decrypted.png`

## 算法概要
1. 改进 Lorenz 方程生成混沌序列（含预热迭代）
2. 序列归一化并输入神经网络训练优化
3. 基于序列进行像素位置置乱
4. 分块扩散（与序列异或/加法/映射）
5. 输出加密图像

## 安全性指标（示例）
| 指标 | 原始 | 加密 | 说明 |
|------|------|------|------|
| 信息熵 | ~7.0 | ~8.0 | 接近随机 |
| 相关系数 | 高 | <0.001 | 相邻像素去相关 |
| 像素变化率 | 0% | >99% | 差分扩散充分 |
| 直方图 | 有规律 | 均匀 | 难以频率分析 |

## 密钥与序列处理
- SHA-384(原始图像字节) -> 解析为初始条件
- 预热迭代 1000 次保证进入混沌区
- 使用 BP 网络(隐藏层≈10)对序列做拟合/优化
- 置乱索引与扩散向量均来源于优化后序列

## 使用注意
1. `keys/` 内容为解密必需，请妥善保存
2. 目前主要针对灰度图；彩色支持可扩展为按通道处理
3. 若更换输入图像，需重新生成密钥文件

## 引用
- 论文：基于神经网络优化混沌系统的图像加密算法（计算机系统应用）
  https://www.c-s-a.org.cn/1003-3254/7578.html

## 许可证
仅供学术研究与教学，不用于商业。

---
如果你需要英文说明，请点击顶部 English 徽章。