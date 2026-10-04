# BanglaLens: A Layer-Wise Mechanistic White-Box Analysis of Bangla Generation Failures in Multilingual Large Language Models

## Authors
### Raian Rashid · Choyon Sarker · Yumna Tasneem · Shanjida Alam · Md. Musfique Anwar | Department of Computer Science and Engineering, Jahangirnagar University, Bangladesh


## Overview

BanglaLens investigates *why* Bangla generation fails in multilingual LLMs, not just *that* it fails. Using logit lens, we analyze intermediate transformer layer states during generation to attribute Bangla generation failures to one of two internal stages: the reasoning/comprehension stage or the internal translation stage.

We evaluate two multilingual LLMs: **Llama-3.1-8B-Instruct** (English-centric) and **Qwen2.5-7B-Instruct** (genuinely multilingual), on a dataset of 1,000 common concept words across four experimental conditions combining two generation goals and two source language conditions.

## Key Findings
- **Llama-3.1-8B-Instruct** shows a **translation barrier** as the dominant failure mode. The model correctly identifies the target concept at intermediate layers 81.6% of the time but fails to produce it in Bangla at the final output layer (TLP = 84.36%).
- **Qwen2.5-7B-Instruct** exhibits a **cross-lingual routing failure**. Achieving 95.4% accuracy under Bangla source input but only 16.9% under English source input, indicating strong Bangla capability that is inaccessible from English input.
- **Romanized Bangla** collapses to near-zero accuracy across both models regardless of source language, indicating a training data absence failure categorically distinct from the translation barrier.
- Exact match evaluation **underestimates** Bangla generation performance by up to 21 percentage points relative to LaBSE-based semantic similarity evaluation.

## Dataset

The dataset contains 1,000 common, culturally neutral concept words balanced equally across four parts of speech: nouns, verbs, adjectives and adverbs (250 each). Each entry includes the English source word, the Bangla script source word, the Bangla script ground truth target and the Romanized Bangla ground truth target. Ground truth translations were obtained via the Google Translate API and verified by a native Bangla speaker.

The dataset is permanently archived on Zenodo with a citable DOI:

> **Dataset DOI:** [link]

## Experimental Conditions

| Condition | Source Language | Target Format | Ground Truth Column |
|---|---|---|---|
| G1-E | English | Bangla script | bangla_script_target |
| G1-B | Bangla | Bangla script | bangla_script_target |
| G2-E | English | Romanized Bangla | romanized_target |
| G2-B | Bangla | Romanized Bangla | romanized_target |

## Models

| Model | Parameters | Category |
|---|---|---|
| Llama-3.1-8B-Instruct | 8B | English-centric, no verified Bangla pretraining |
| Qwen2.5-7B-Instruct | 7B | Genuinely multilingual, confirmed Bangla pretraining |

Both models are loaded in 4-bit NF4 quantization using `bitsandbytes`. Experiments were run on two NVIDIA T4 GPUs (16 GB VRAM each) via the Kaggle free tier.

## Evaluation

Correctness is evaluated using two methods:

- **Exact match** - strict string comparison (case-insensitive for Romanized conditions)
- **Semantic similarity** - LaBSE cosine similarity at thresholds τ ∈ {0.75, 0.80, 0.85}

τ = 0.80 is the primary reporting threshold. Sensitivity analysis confirms findings are stable across all thresholds.
















