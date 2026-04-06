---
layout: default
---

<div align="center">

# Agent-as-Annotators (A3)

| [**💾 Code**](https://github.com/McGill-NLP/agent-as-annotators) | [**📄 Paper**](https://arxiv.org/abs/TODO) |
| :--: | :--: |
| [**🤗 Dataset**](https://huggingface.co/datasets/McGill-NLP/A3-Synth) | [**🤖 Model**](https://huggingface.co/McGill-NLP/A3-Qwen3.5-9B) |

<br>

[**Structured Distillation of Web Agent Capabilities Enables Generalization**](https://arxiv.org/abs/TODO)

*[Xing Han Lu](https://xinghanlu.com),
[Siva Reddy](https://sivareddy.in)*
<br>
*McGill University & Mila*

</div>

![Agent-as-Annotators pipeline](/assets/fig1.png)

## Abstract

Frontier LLMs can navigate complex websites, but their cost and reliance on third-party APIs make local deployment impractical. We introduce **Agent-as-Annotators**, a framework that structures synthetic trajectory generation for web agents by analogy to human annotation roles, replacing the Task Designer, Annotator, and Supervisor with modular LLM components. Using Gemini 3 Pro as teacher, we generate 3,000 trajectories across six web environments and fine-tune a 9B-parameter student with pure supervised learning on the 2,322 that pass quality filtering. The resulting model achieves **41.5% on WebArena**, surpassing closed-source models such as Claude 3.5 Sonnet (36.0%) and GPT-4o (31.5%) under the same evaluation protocol, and **nearly doubling** the previous best open-weight result (Go-Browse, 21.7%). Capabilities transfer to unseen environments, with an **18.2 percentage point gain on WorkArena L1** (an enterprise platform never seen during training) and consistent improvements across three additional benchmarks.

## Key Results

| Benchmark | A3-Qwen3.5-9B | Qwen3.5-9B (base) | GPT-4o | Claude 3.5 Sonnet |
|-----------|:-:|:-:|:-:|:-:|
| **WebArena** (in-domain) | **41.5%** | 27.8% | 31.5% | 36.0% |
| **VisualWebArena** | **33.9%** | 28.5% | -- | -- |
| **WorkArena L1** (OOD) | **51.5%** | 33.3% | -- | -- |
| **WorkArena++ L2** (OOD) | **9.7%** | 2.2% | -- | -- |
| **MiniWoB** (OOD) | **69.0%** | 63.2% | -- | -- |

## Installation

```bash
git clone https://github.com/McGill-NLP/agent-as-annotators.git
cd agent-as-annotators
pip install -e .
```

## Quick Start

Serve the model with vLLM and run evaluation:

```bash
# Serve
vllm serve McGill-NLP/A3-Qwen3.5-9B --tensor-parallel-size 2 --max-model-len 65536 --enforce-eager --dtype bfloat16

# Evaluate on WebArena
python run_webarena.py --benchmark webarena_test --model A3-qwen3.5-9b
```

## Dataset

Download the A3-Synth training dataset from HuggingFace:

```python
from huggingface_hub import snapshot_download
snapshot_download("McGill-NLP/A3-Synth", repo_type="dataset", local_dir="./data")
```

The dataset includes:
- **16,353 SFT training examples** from 2,322 successful trajectories
- **3,000 task configurations** across 6 WebArena environments
- **250 generated personas** for diverse task intent synthesis
- **Raw trajectory JSONs** with step-by-step screenshots

## Models

| Model | Parameters | HuggingFace |
|-------|:---------:|-------------|
| A3-Qwen3.5-9B | 9B | [McGill-NLP/A3-Qwen3.5-9B](https://huggingface.co/McGill-NLP/A3-Qwen3.5-9B) |
| A3-Qwen3.5-4B | 4B | [McGill-NLP/A3-Qwen3.5-4B](https://huggingface.co/McGill-NLP/A3-Qwen3.5-4B) |
| A3-Qwen3.5-2B | 2B | [McGill-NLP/A3-Qwen3.5-2B](https://huggingface.co/McGill-NLP/A3-Qwen3.5-2B) |

## Citation

```bibtex
@inproceedings{lu2026agent,
  title={Structured Distillation of Web Agent Capabilities Enables Generalization},
  author={Lu, Xing Han and Reddy, Siva},
  booktitle={Conference on Language Modeling (COLM)},
  year={2026}
}
```
