# DouHao 👋

<p align="left">
  哈尔滨工业大学硕士在读，研究方向为 <b>大模型算法 / 后训练 / 推理优化</b>
</p>

---

## 关于我

我目前在哈尔滨工业大学攻读硕士，主要关注大语言模型相关的算法研究与工程实践，兴趣集中在以下几个方向：

- Transformer 结构理解与改造
- 大模型后训练方法
- 推理阶段性能优化与问题排查
- 可复现实验设计与消融分析

我希望持续积累对模型结构、训练流程和推理系统的理解，重视实验结果的真实性、可复现性，以及研究结论的边界意识。

---

## 研究兴趣

- Transformer / RoPE / KV Cache / Residual Path
- Attention Residuals
- Pretraining / SFT / GRPO-style 后训练
- LoRA / QLoRA
- 大模型推理优化

---

## 代表项目

### 1. MiniMind AttnRes 模型结构改造与推理优化

- 基于 Attention Residuals 思路，在 MiniMind 后段层实现 Block AttnRes-lite
- 按 block 聚合前层 hidden states 形成 block memory，并通过额外 q/k/v 投影对历史 block summary 做注意力聚合
- 完成 Baseline、AttnRes-v1、AttnRes-v2 三组 Pretrain + SFT 对照实验
- 在训练阶段取得更优结果后，进一步排查生成阶段无限循环问题，并定位到 block memory 与 Hugging Face generate / KV Cache 路径不兼容
- 将结构调整为与 decode 路径兼容的版本后，实现正常生成
- 演示中推理速度由约 64 tok/s 提升到约 100 tok/s，去除冷启动样本后均值约 101.0 tok/s

**关键词：** Attention Residuals / MiniMind / KV Cache / Inference Optimization / Decode Compatibility

---

### 2. simple GRPO：GRPO-style 后训练消融实验

- 基于 Qwen2.5-7B-Instruct 与 GSM8K 搭建最小化 GRPO-style 后训练闭环
- 在 2×A100 40GB 环境下，使用 GPU0 进行 vLLM generation、GPU1 进行 DeepSpeed training
- 围绕 group size 与 KL 系数设计可解释消融实验
- 在共享训练区间比较中，gs=6 获得更优末段平均奖励，同时单步耗时更低
- 对 beta 相关实验现象保持审慎判断，认为当前日志指标不足以有效分离 KL 系数影响
- 提出补充逐 token KL、奖励分项与独立重跑的后续方案

**关键词：** GRPO-style / Post-training / Ablation Study / vLLM / DeepSpeed / Qwen2.5-7B

---

## 技术栈

### 训练与推理
PyTorch / DeepSpeed / vLLM / Hugging Face

### 微调与后训练
Pretraining / SFT / GRPO-style / LoRA / QLoRA / Unsloth / LLaMA-Factory

### 编程语言
Python / Golang

### 开发环境
Linux / 常用算法与数据结构

---

## 教育经历

- **哈尔滨工业大学**  
  硕士，2024.09 - 2027.06

- **中国地质大学（武汉）**  
  本科，2020.09 - 2024.06

---

## 个人风格

- 具备较强的学习与自驱能力，能够围绕新模型结构、后训练方法和推理问题快速完成论文整理、资料理解、实验搭建与结果复盘
- 做事细致，责任心较强，重视实验结果的真实性、可复现性和结论边界

---

## 联系方式

- GitHub: [forever-free1](https://github.com/forever-free1)
- Email: 17718676729@163.com

---

## 说明

这个主页主要用于展示我在大模型算法、后训练方法和推理优化方向的学习与实践。  
欢迎交流模型结构改造、训练实验设计、推理排障与性能优化相关内容。
