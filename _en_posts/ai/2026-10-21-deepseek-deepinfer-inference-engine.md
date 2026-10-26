---
title: "DeepSeek Releases Its DeepInfer Inference Engine — 155 Trillion Tokens a Day"
description: "What DeepSeek released when it open-sourced DeepInfer, the inference engine behind its own service, under Apache 2.0, and the serving components left out of this release"
date: 2026-10-21
category: AI
subcategory: News
tags: [deepseek, deepinfer, inference-engine, open-source, moe]
image: /assets/og/en-2026-10-21-deepseek-deepinfer-inference-engine.png
---

DeepSeek has released **DeepInfer**, the inference engine that runs its own service
It is the very code DeepSeek said in 2025 it would not release as a whole engine

The license is **Apache 2.0**, and the repository's first commit is dated October 20, 2026
It passed <mark>9,500</mark> GitHub stars within a day of release

![DeepSeek logo](/assets/images/ai/deepseek-deepinfer-inference-engine/01-deepseek-logo-color.webp)
*DeepSeek logo*

## What was released

![Architecture diagram of the DeepSeek V4.1 Flash inference system](/assets/images/ai/deepseek-deepinfer-inference-engine/02-photo.webp)
*Architecture diagram of the DeepSeek V4.1 Flash inference system — Source: DeepSeek*

DeepInfer is an inference framework for serving **DeepSeek-V4.1-Flash** at scale
Inference is the stage where a trained model produces answers

This release covers offline inference
The README says three components needed to run the actual service were <u>left out of this release</u>

| Type | Contents |
| :--- | :--- |
| Included | Optimized kernels, expert parallelism |
| Included | DSpark speculative decoding |
| Included | Structured output (JSON schema) |
| Included | Deterministic sampling (NVIDIA only) |
| Left out | **KV cache system** |
| Left out | Disaggregated prefill and decode |
| Left out | Load balancing across replicas |

DeepSeek said the KV cache and load balancing <mark>depend heavily on internal infrastructure</mark>, so it could not release all of them yet
Instead, it explained the design of the two components in its deployment Q&A document and a Zhihu post

**deepseek-recipe**, released alongside it, is a module that converts API requests into tokens
It handles three API formats (Chat Completions, Responses, Messages)

## What changed since the 2025 announcement

After its 2025 Open Source Week, DeepSeek published a post putting off the engine release
It gave three reasons

[A vLLM fork over a year old]
Heavily modified for DeepSeek models, hard to extend for general use

[Tied to internal infrastructure]
Depends on cluster management tools, needing large changes for external deployment

[Not enough people to maintain it]
A small research team without the capacity to maintain a large open-source project

The alternative at the time was to split off and release only the reusable components
That is how kernel libraries such as **FlashMLA**, **DeepGEMM**, and **DeepEP** came out

This time, the engine itself that ties these components together has been released
The README says DeepInfer is built <mark>on top of vLLM</mark>

It also says it took ideas from SGLang and TensorRT-LLM

The second reason, <u>dependence on internal infrastructure</u>, has not been resolved yet

## Operating figures in the published documents

![Card of operating figures for the DeepSeek V4.1 Flash inference service](/assets/images/ai/deepseek-deepinfer-inference-engine/en/03-chart.webp)
*Card of operating figures for the DeepSeek V4.1 Flash inference service — Source: self-rendered based on DeepSeek's deployment Q&A*

According to the deployment Q&A, a single cluster processes <mark>155 trillion tokens</mark> a day

Revenue per GPU-hour is about **$38 (₩53,200)** at off-peak discount pricing
The SSDs holding the KV cache total about 100 PiB, with retention of 3 days for agents and 7 days for chatbots

The **KV cache** is stored data for context that has already been computed
When the same prefix is asked again, the duplicate computation is skipped, cutting cost and processing time

### 📈 Decode throughput

![Graph of decode throughput per GPU versus speed per user](/assets/images/ai/deepseek-deepinfer-inference-engine/04-photo.webp)
*Graph of decode throughput per GPU versus speed per user — Source: DeepSeek*

In a 64-GPU setup, handling 256 requests at once per GPU produced about **26,000 tokens** per second
In exchange, the speed each user gets drops to a little over 100 tokens per second

Cutting it to 8 requests pushes per-user speed past <mark>320 tokens</mark> per second
Total throughput per GPU falls accordingly, to about 2,600 tokens per second

### ⚡ DSpark variable-length verification

![Bar chart of throughput change from variable-length verification](/assets/images/ai/deepseek-deepinfer-inference-engine/en/05-chart-dspark.webp)
*Bar chart of throughput change from variable-length verification — Source: self-rendered based on DeepSeek's deployment Q&A*

**DSpark** first drafts tokens with a small model, then has the main model verify them
DeepInfer predicts how likely each draft is to be right and changes the number of tokens to verify

Verified tokens fell by about 30% compared with a fixed 5
Around 60 concurrent requests, the range used in actual operation, throughput rose <mark>4–7%</mark>

At 16 concurrent requests it actually fell 1.5%

## Where it can run in Korea

Two kinds of hardware are supported: **NVIDIA SM100 GPUs** and Huawei **Ascend 950** NPUs
SM100 refers to Blackwell data center GPUs in the B200 family

Earlier generations such as H100 and H200 are <u>not on the support list</u>
It also needs CUDA 13, Python 3.12, and GCC 13 or later

The minimum scale DeepSeek gives for efficient operation is <mark>128</mark> GPUs
That is 64 for prefill plus 64 for decode

In Korea, the Ministry of National Defense, the Ministry of Foreign Affairs, the Ministry of Trade, Industry and Energy, and others blocked access to DeepSeek in February 2025
Those measures targeted the app and web service DeepSeek runs

Running the weights on your own servers with DeepInfer means inputs do not go to DeepSeek's servers
Self-hosting still has to pass each organization's own security review

## What to watch next

- DeepSeek said it will keep putting <u>inference code for its next models</u> into DeepInfer
- The deployment Q&A is a document that keeps being updated as questions come in
- Once the **KV cache and load balancing** code is released, it will be a complete serving setup
- How much of the V4.1 Flash optimization gets reflected in vLLM and SGLang is another thing to check

The earlier V4.1-Flash-1017 release is covered in the post below

🔗 Link - https://blog.naver.com/rottensweetpotato/224446055227

## Sources

- [[GitHub] deepseek-ai/DeepInfer README (support scope, hardware, license)](https://github.com/deepseek-ai/DeepInfer)
- [[GitHub] DeepSeek V4.1 Flash Inference Deployment Q&A (operating figures, DSpark table)](https://github.com/deepseek-ai/DeepInfer/blob/main/doc/inference_deployment_qa.md)
- [[GitHub] open-infra-index, OpenSourcing DeepSeek Inference Engine (2025 reasons for holding back)](https://github.com/deepseek-ai/open-infra-index/tree/main/OpenSourcing_DeepSeek_Inference_Engine)
- [[Daum News] Defense, foreign affairs, and industry ministries block DeepSeek access (2025-02-05)](https://v.daum.net/v/20250205211948335)
- Exchange rate: converted at $1 ≈ ₩1,400
