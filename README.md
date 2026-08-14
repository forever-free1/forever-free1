<div align="center">

# forever-free1

[![Typing SVG](https://readme-typing-svg.demolab.com?font=JetBrains+Mono\&size=22\&duration=2600\&pause=700\&color=2F80ED\&center=true\&vCenter=true\&width=760\&lines=Multimodal+Foundation+Models;Vision-Language-Action;LLM+Post-training+%26+Reinforcement+Learning;Agents+%26+Reasoning;Efficient+Multimodal+Inference)](https://git.io/typing-svg)

I work on **multimodal foundation models and LLM post-training**,
with a focus on **VLA, reinforcement learning, agents, and efficient inference**.

<br>

![Python](https://img.shields.io/badge/Python-3.11-3776AB?style=flat-square\&logo=python\&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-2.x-EE4C2C?style=flat-square\&logo=pytorch\&logoColor=white)
![VLA](https://img.shields.io/badge/Research-VLA-2F80ED?style=flat-square)
![RL](https://img.shields.io/badge/RL-GRPO%20%2F%20DAPO-6F42C1?style=flat-square)
![Research](https://img.shields.io/badge/Research-Reproducible-22863A?style=flat-square)

</div>

---

I enjoy starting from concrete failure modes, designing small and testable interventions, and validating what actually changes through reproducible experiments.

My recent work mainly explores **self-evolving VLA post-training, reinforcement learning for multi-turn agents, multimodal inference efficiency, and lightweight RL infrastructure**.

## Selected Work

### 🔥 [FIRE-VLA](https://github.com/forever-free1/FIRE-VLA)

<div align="left">

![Task](https://img.shields.io/badge/Task-VLA_Post--training-2F80ED?style=flat-square)
![Method](https://img.shields.io/badge/Method-Self--Evolution-111111?style=flat-square)
![RL](https://img.shields.io/badge/RL-GRPO-6F42C1?style=flat-square)
![Avg L2](https://img.shields.io/badge/Avg_L2-0.6421_%E2%86%92_0.6023-22863A?style=flat-square)

</div>

**Failure-Informed Self-Evolution for Vision-Language-Action Models**

A self-evolving post-training framework for driving VLA models.

FIRE-VLA retains GRPO rollout learning while identifying unresolved failure groups from reward and rollout diversity. A frozen privileged teacher then provides on-policy supervision for these difficult samples, allowing the student policy and its failure distribution to evolve together across training rounds.

**Avg L2 improves from `0.6421 → 0.6023`** over standard GRPO, while severe long-error rollouts are reduced from **81 → 50** under G=4 evaluation.

[**Code**](https://github.com/forever-free1/FIRE-VLA) · [**Paper**](https://arxiv.org/abs/2608.13395)

---

### 🧠 [CIGPO](https://github.com/forever-free1/CIGPO)

<div align="left">

![Task](https://img.shields.io/badge/Task-Multi--turn_Agent-2F80ED?style=flat-square)
![Method](https://img.shields.io/badge/Method-Information_Gain-111111?style=flat-square)
![Base F1](https://img.shields.io/badge/Base_F1-0.252-666666?style=flat-square)
![CIGPO F1](https://img.shields.io/badge/CIGPO_F1-0.518-22863A?style=flat-square)

</div>

**Contextual Information-Gain Policy Optimization for Multi-Turn Evidence-Reading Agents**

CIGPO starts from a failure mode of outcome-only GRPO: as reward variance disappears, multi-turn agents can enter a **zero-advantage lock-in**, causing the policy gradient to vanish.

Instead of assigning credit only to the final answer, CIGPO estimates how much each newly read piece of evidence increases confidence in the correct answer and turns this information gain into a process-level learning signal.

On HotpotQA with Qwen2.5-3B, standard F1 improves from **`0.252 → 0.518`**, while the GRPO baseline eventually collapses to **0.000**.

[**Code**](https://github.com/forever-free1/CIGPO) · [**Paper**](https://arxiv.org/abs/2607.16244)

---

### ⚡ [visual-token-break-even](https://github.com/forever-free1/visual-token-break-even)

<div align="left">

![Topic](https://img.shields.io/badge/Topic-Multimodal_Inference-2F80ED?style=flat-square)
![Model](https://img.shields.io/badge/Model-Qwen2.5--VL--3B-111111?style=flat-square)
![System](https://img.shields.io/badge/System-End--to--End_Latency-6F42C1?style=flat-square)
![Latency](https://img.shields.io/badge/RTX_3090-%E2%86%93_5.62%25-22863A?style=flat-square)

</div>

**When Do Fewer Visual Tokens Actually Accelerate Multimodal Inference?**

Reducing visual tokens does not necessarily make multimodal inference faster.

This project studies the real **break-even point of visual-token reduction**, measuring not only LLM prefill and decoding but also policy overhead, image preprocessing, vision encoding, and reusable computation.

Experiments on Qwen2.5-VL-3B show up to **5.62% mean latency reduction on RTX 3090**, while also demonstrating an important systems effect:

> Removing more visual tokens can save less latency when the reduction happens after expensive operators have already executed.

[**Code**](https://github.com/forever-free1/visual-token-break-even) · [**Paper**](https://arxiv.org/abs/2608.03649)

---

### 🛠️ [rlite](https://github.com/forever-free1/rlite)

<div align="left">

![Framework](https://img.shields.io/badge/Framework-Lightweight-2F80ED?style=flat-square)
![RL](https://img.shields.io/badge/RL-GRPO_%2F_DAPO-6F42C1?style=flat-square)
![Design](https://img.shields.io/badge/Design-Plugin--based-22863A?style=flat-square)
![Purpose](https://img.shields.io/badge/Purpose-Fast_Iteration-111111?style=flat-square)

</div>

**A lightweight plugin-based LoRA-GRPO / DAPO framework**

`rlite` is a lightweight RL post-training framework built for quickly testing new tasks, reward functions, and training ideas.

Instead of covering every large-scale training scenario, it keeps **task, reward, training configuration, and evaluation logic** modular so that small verifiable RL experiments can be built and iterated quickly.

[**Code**](https://github.com/forever-free1/rlite)

---

## Other Projects

Some earlier research and engineering work:

* **[VeriSeek](https://github.com/forever-free1/veriseek)** — scientific evidence QA with **SFT + RL**, reaching **79.3% answer accuracy** on SciFact.
* **[tiny-r1](https://github.com/forever-free1/tiny-r1)** — a minimal and reproducible **SFT → GRPO** training pipeline.
* **[AutoPilot](https://github.com/forever-free1/Autopilot)** — a tool-using intelligent cockpit Agent built with Go, Python and Next.js.
* **[TideKV](https://github.com/forever-free1/TideKV)** — distributed KV storage implemented in Go with Bitcask, Raft and Bloom Filters.
* **[go-ai-copilot](https://github.com/forever-free1/go-ai-copilot)** — a RAG-based AI coding assistant with streaming dialogue and a complete Web backend.

These projects reflect some of my earlier work in **LLMs, agents, distributed systems, backend engineering, and building systems from scratch**.

---

## Current Interests

<div align="center">

`Vision-Language-Action` · `Multimodal LLMs` · `LLM Post-training` · `GRPO`

`Agent RL` · `Credit Assignment` · `Self-Evolution` · `Efficient Inference`

</div>

---

<div align="center">

**Small, complete, and verifiable problems over large but vague stories.**

</div>
