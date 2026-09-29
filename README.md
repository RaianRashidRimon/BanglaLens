# BanglaLens: A Layer-Wise Mechanistic White-Box Analysis of Bangla Generation Failures in Multilingual Large Language Models

## Authors
### Raian Rashid · Choyon Sarker · Yumna Tasneem · Shanjida Alam · Md. Musfique Anwar | Department of Computer Science and Engineering, Jahangirnagar University, Bangladesh

## Overview

BanglaLens investigates *why* Bangla generation fails in multilingual LLMs, not just *that* it fails. Using logit lens, we analyze intermediate transformer layer states during generation to attribute Bangla generation failures to one of two internal stages: the reasoning/comprehension stage or the internal translation stage.

We evaluate two multilingual LLMs: **Llama-3.1-8B-Instruct** (English-centric) and **Qwen2.5-7B-Instruct** (genuinely multilingual), on a dataset of 1,000 common concept words across four experimental conditions combining two generation goals and two source language conditions.
