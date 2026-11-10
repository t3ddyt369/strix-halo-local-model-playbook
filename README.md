# Strix Halo Local-Model Playbook

An open-source benchmark and configuration harness for Lemonade Server and llama.cpp on AMD Ryzen AI Max (Strix Halo) hardware.

## What this is

This project runs a fixed suite of tasks (coding, summarisation, tool-calling, long context) across models, quantizations and backends (GPU, NPU, hybrid) on Ryzen AI Max hardware, using Lemonade Server and llama.cpp. For every run it records:

- Output quality against the task suite's checks
- Tokens per second and time to first token
- Memory use
- Power draw

The output is a **validated configuration for each model** — exact server flags, quantization, context size and backend — so other developers can reproduce the result on day one instead of re-running the search themselves. The harness includes an OpenAI-compatible endpoint check, so the same suite can test any local server, not just Lemonade and llama.cpp.

## Why

Strix Halo's 128 GB of unified memory makes it one of the most interesting local-inference platforms available, but published results are scattered, hard to compare, and rarely reproducible: different tasks, different flags, no power or memory figures. This playbook fixes that with one fixed task suite, one recording format, and published configs that are known to work.

## Deliverables

- This repository: the harness, the task suite, and the per-model validated configs
- Results tables: quality, tokens/sec, time-to-first-token, memory and power per model / quantization / backend
- A short write-up of findings per model tested

## Benchmarking approach

- Benchmarks of open-weight models on Strix Halo: quality against speed against memory across quantizations (Q4_K_M to Q8), context sizes and backends (Vulkan / ROCm)
- Head-to-head A/B tests of models of the same size on the same task sets (first pair: a 27B reasoning model against Qwen3.8-27B)
- Every result lands in a reproducible per-model playbook entry: exact server flags, measured tokens per second, power draw

## Reference hardware

- GMKtec EVO-X2 — AMD Ryzen AI Max+ 395, 128 GB unified memory, Fedora, llama.cpp server
- Proxmox VE host (~20 LXC containers) for supporting services and CI

## Background

This project comes out of the Thomas Stack, a self-hosted, local-first AI platform: a Proxmox server running Git hosting (Forgejo with CI runners), observability (Prometheus, Grafana, Langfuse, Gatus), secrets management, an LLM gateway (LiteLLM) and backups, with the EVO-X2 serving open-weight models locally. Runtime data never leaves the hardware. The playbook is the public, reproducible record of what actually works on this hardware.

## Status

Initial project scaffold for the AMD Lemonade Developer Challenge. Harness code and the first results tables land here as they are built; no benchmark numbers are published until they are measured with the harness itself.

## Licence

Apache-2.0 — see [LICENSE](LICENSE).
