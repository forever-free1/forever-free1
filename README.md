<div align="center">

# Hao Dou · Forever-free1

[![Typing SVG](https://readme-typing-svg.demolab.com?font=JetBrains+Mono\&size=22\&duration=2600\&pause=700\&color=2F80ED\&center=true\&vCenter=true\&width=760\&lines=Multimodal+Foundation+Models;Vision-Language-Action;LLM+Post-training+%26+Reinforcement+Learning;Agents+%26+Reasoning;Efficient+Multimodal+Inference)](https://git.io/typing-svg)

**Multimodal Foundation Models · VLA · LLM Post-training · Reinforcement Learning**

<br>

![Python](https://img.shields.io/badge/Python-3.11-3776AB?style=flat-square\&logo=python\&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-2.x-EE4C2C?style=flat-square\&logo=pytorch\&logoColor=white)
![VLA](https://img.shields.io/badge/Research-VLA-2F80ED?style=flat-square)
![RL](https://img.shields.io/badge/RL-GRPO%20%2F%20DAPO%20%2F%20GSPO-6F42C1?style=flat-square)
![Research](https://img.shields.io/badge/Research-Reproducible-22863A?style=flat-square)

</div>

---

My recent work focuses on **VLA post-training, reinforcement learning for LLM agents, multimodal inference efficiency, and RL training systems**.

Current technical interests include **self-evolving post-training, rollout-based policy optimization, credit assignment, verifiable rewards, multimodal inference optimization, and efficient RL infrastructure**.

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

FIRE-VLA retains GRPO rollout learning while identifying unresolved failure groups from reward and rollout diversity. A frozen privileged teacher provides on-policy supervision for difficult samples, allowing the student policy and its failure distribution to evolve together across training rounds.

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

CIGPO studies a failure mode of outcome-only GRPO in multi-turn evidence-reading agents: as reward variance disappears, training can enter a **zero-advantage lock-in** and lose effective policy-gradient signals.

Instead of assigning credit only to the final answer, CIGPO estimates how much each newly observed piece of evidence increases confidence in the correct answer and converts this contextual information gain into process-level rewards.

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

A systems study of the **break-even point of visual-token reduction** in multimodal LLM inference.

The project measures not only LLM prefill and decoding, but also routing overhead, image preprocessing, vision encoding, and reusable computation to determine when reducing visual tokens actually improves end-to-end latency.

Experiments on Qwen2.5-VL-3B show up to **5.62% mean latency reduction on RTX 3090**, while demonstrating that removing more visual tokens does not necessarily result in larger latency savings.

[**Code**](https://github.com/forever-free1/visual-token-break-even) · [**Paper**](https://arxiv.org/abs/2608.03649)

---

### 🛠️ [rlite](https://github.com/forever-free1/rlite)

<div align="left">

![Scope](https://img.shields.io/badge/Scope-Single--node_RL-2F80ED?style=flat-square)
![Algorithms](https://img.shields.io/badge/Algorithms-GRPO_%2F_DAPO_%2F_GSPO-6F42C1?style=flat-square)
![Runtime](https://img.shields.io/badge/Runtime-Ray_%2B_vLLM-111111?style=flat-square)
![Sync](https://img.shields.io/badge/Sync-Versioned_LoRA-22863A?style=flat-square)

</div>

**A compact framework for understanding and reproducing LLM policy optimization**

`rlite` exposes the complete online-RL training path instead of hiding it behind a large distributed training stack:

**vLLM rollout → verifiable rewards → grouped experience → policy optimization → versioned LoRA synchronization**

It provides **GRPO, DAPO, and GSPO** objectives through a common algorithm interface, with Ray-based rollout/trainer actors, bounded experience buffering, Hugging Face and vLLM rollout backends, token-aware LoRA microbatch training, and explicit rollout-policy version consistency.

The framework also implements **versioned adapter synchronization** and guards against stale experience, policy-version mismatch, response-token misalignment, and cache reuse across policy updates.

Small-scale Qwen2.5-1.5B-Instruct experiments on GSM8K complete **200 GRPO / GSPO updates** on two RTX 3090 GPUs, serving as an end-to-end validation of the training runtime.

[**Code**](https://github.com/forever-free1/rlite)

---

## Other Projects

Some earlier research and engineering work:

* **[VeriSeek](https://github.com/forever-free1/veriseek)** — scientific evidence QA with **SFT + RL**, reaching **79.3% answer accuracy** on SciFact.
* **[tiny-r1](https://github.com/forever-free1/tiny-r1)** — a minimal and reproducible **SFT → GRPO** training pipeline.
* **[AutoPilot](https://github.com/forever-free1/Autopilot)** — a tool-using intelligent cockpit Agent built with Go, Python and Next.js.
* **[TideKV](https://github.com/forever-free1/TideKV)** — distributed KV storage implemented in Go with Bitcask, Raft and Bloom Filters.
* **[go-ai-copilot](https://github.com/forever-free1/go-ai-copilot)** — a RAG-based AI coding assistant with streaming dialogue and a complete Web backend.

---

## Technical Focus

<div align="center">

`Vision-Language-Action` · `Multimodal LLMs` · `LLM Post-training` · `Policy Optimization`

`GRPO` · `DAPO` · `GSPO` · `Agent RL` · `Credit Assignment`

`Self-Evolution` · `vLLM` · `LoRA` · `Efficient Inference`

</div>
