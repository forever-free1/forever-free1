<div align="center">

# forever-free1

[![Typing SVG](https://readme-typing-svg.demolab.com?font=JetBrains+Mono\&size=22\&duration=2600\&pause=700\&color=2F80ED\&center=true\&vCenter=true\&width=760\&lines=LLM+Post-training;Verifiable+Reasoning;Evidence-seeking+Agents;RL+for+Scientific+QA;Small+Models%2C+Complete+Experiments)](https://git.io/typing-svg)

</div>

---

最近主要在做一些和 **大模型后训练、可验证推理、证据阅读 Agent、RL 训练稳定性** 有关的项目。

我更喜欢把一个问题做完整：先找到事情到底哪里出了问题，再去理解和复现当前比较好的方法，然后设计一个足够简单的干预方式，最后用可复现的实验说明它到底提升了多少。对我来说，项目的重点不是把故事讲得很大，而是尽量把真实存在的问题解决得更清楚一些。

<div align="center">

![Python](https://img.shields.io/badge/Python-3.11-3776AB?style=flat-square\&logo=python\&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-2.x-EE4C2C?style=flat-square\&logo=pytorch\&logoColor=white)
![LLM](https://img.shields.io/badge/LLM-Post--training-111111?style=flat-square)
![RL](https://img.shields.io/badge/RL-GRPO%20%2F%20DAPO-6F42C1?style=flat-square)
![Research](https://img.shields.io/badge/Research-Reproducible-22863A?style=flat-square)

</div>

---

## 最近的几个项目

### [VeriSeek](https://github.com/forever-free1/veriseek)

<div align="left">

![Task](https://img.shields.io/badge/Task-Scientific_QA-2F80ED?style=flat-square)
![Model](https://img.shields.io/badge/Base-Qwen3--4B--Thinking-111111?style=flat-square)
![Accuracy](https://img.shields.io/badge/Accuracy-79.3%25-22863A?style=flat-square)
![Evidence F1](https://img.shields.io/badge/Evidence_F1-0.377_%E2%86%92_0.406-6F42C1?style=flat-square)

</div>

很多科学问答任务里，模型只给出一个判断其实不够。尤其是论文结论真伪判断，真正重要的是模型能不能说明：这个结论为什么被支持、为什么被反驳，或者为什么当前证据不足。

围绕这个问题，我基于 **Qwen3-4B-Thinking** 做了一套科学证据问答后训练流程，让模型在输出 `SUPPORTS / REFUTES / NOT_ENOUGH_INFO` 的同时，也返回对应的论文证据。项目中对比了 Base、RL-only、SFT、SFT + RL 几条路线，并设计了面向答案正确性、证据命中和格式稳定性的确定性奖励。

最终，**SFT + RL** 在 SciFact dev set 上达到 **79.3% accuracy**；证据 F1 从 **0.377 提升到 0.406**。相比单纯监督微调，RL 带来的提升不算夸张，但能看到模型在证据选择上的进一步改善。

---

### [CIGPO](https://github.com/forever-free1/cigpo)

<div align="left">

![Task](https://img.shields.io/badge/Task-Multi--turn_Evidence_Reading-2F80ED?style=flat-square)
![Method](https://img.shields.io/badge/Method-Information_Gain_Reward-111111?style=flat-square)
![Base F1](https://img.shields.io/badge/Base_F1-0.252-666666?style=flat-square)
![CIGPO F1](https://img.shields.io/badge/CIGPO_F1-0.518-22863A?style=flat-square)
![Gain](https://img.shields.io/badge/Relative_Gain-%2B105%25-6F42C1?style=flat-square)

</div>

这个项目来自一个很具体的失败现象：在多轮证据阅读任务里，普通 GRPO 前期看起来能训练，但后期很容易因为格式错误累积、奖励无差异，最终让训练信号消失，甚至直接崩到不可用。

我把问题收紧到 **多轮 evidence-reading agent 的 credit assignment** 上：模型每一轮读到的证据，到底有没有让它离正确答案更近？基于这个思路，我设计了 **Contextual Information-Gain Policy Optimization**，用参考模型评估每轮证据读取带来的信息增益，把原本只发生在最终答案处的稀疏反馈，拆成更稳定的过程级奖励。

在 HotpotQA 风格任务上，Base Qwen2.5-3B 的 standard F1 为 **0.252**；CIGPO 在 step 200 达到 **0.518**，相对提升约 **105%**。同时，普通 GRPO 在同阶段崩溃到 **0.000 F1**，而 CIGPO 仍能保持稳定。

---

### [rlite](https://github.com/forever-free1/rlite)

<div align="left">

![Framework](https://img.shields.io/badge/Framework-Lightweight-2F80ED?style=flat-square)
![RL](https://img.shields.io/badge/RL-GRPO_%2F_DAPO-6F42C1?style=flat-square)
![Design](https://img.shields.io/badge/Design-Plugin--based-22863A?style=flat-square)
![Purpose](https://img.shields.io/badge/Purpose-Fast_Iteration-111111?style=flat-square)

</div>

做后训练实验时，我经常遇到一个问题：很多框架很完整，但也很重。对于只想验证一个奖励函数、一个任务格式或者一个训练稳定性问题的小实验来说，启动成本偏高，任务、奖励和评估逻辑也不够容易拆开改。

所以我写了 **rlite**，一个更轻量的 LoRA-GRPO / DAPO 风格实验框架。它不追求覆盖所有大规模训练场景，而是把任务、奖励、训练配置和评估逻辑拆得更清楚，方便快速搭建可验证的小实验。

目前它更像是一个实验骨架：适合继续接入新的任务插件、reward 插件和自动评估脚本。相比 VeriSeek 和 CIGPO，它暂时还不是一个完整论文型项目，而是我用来加速后续实验迭代的基础设施。

---

### 还在整理中

除了大模型后训练，我也保留了一些 Go、Rust、Python 和 Web 相关的小项目。

这些项目不一定直接对应论文，但会记录一些从零实现、系统拆解和工程化训练的过程。对我来说，研究项目最后能不能落下来，很大程度上也取决于这些更基础的工程能力。

主页里暂时只放能说明问题的项目，不打算把所有仓库都堆上来。

---

## 当前关键词

<div align="center">

`LLM Post-training` · `GRPO` · `DAPO` · `Verifiable Reward` · `Scientific QA` · `Evidence Retrieval` · `Reasoning Agent` · `RL Stability`

</div>

---

<div align="center">

小而完整，比大而模糊更重要。

</div>
