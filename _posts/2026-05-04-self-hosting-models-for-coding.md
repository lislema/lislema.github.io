---
layout: post
title:  "Self hosting Models for Coding"
date:   2026-05-04 9:45:00 +0200
categories: [AI, Security, Legacy, DevSecOps]
---

## Overview 

This is not a conceptual article. This is a real engineering workflow executed end-to-end in ~60 minutes using:

- Ollama (self-hosted model runtime)
- Anthropic Claude Code (engineering orchestrator)
- Kimi 2.6 (primary generation model)
- GitHub (source control + CI/CD)

The system produced:

- Application code
- Unit tests
- Documentation
- Security checks
- GitHub Actions pipeline
- Fully pushed repository

All with minimal manual intervention.

---

## Why Ollama Matters

Ollama changes the economics and security model:

- Local execution (no external API dependency)
- No per-token billing pressure
- Full control over model lifecycle
- Reduced risk of data exfiltration

| Control Area | API-based LLMs | Ollama |
|---|---|---|
| Data Exposure | External | Local |
| Latency | Network-bound | Local |
| Cost Model | Token-based | Compute-based |
| Governance | Limited | Full |

---


## Claude Code as an Engineering Agent

Anthropic’s tooling acted as a full SDLC orchestrator.

- Generate application code
- Create unit tests
- Add inline documentation
- Perform basic security checks
- Generate CI/CD pipeline
- Push to GitHub

---

This is not assistance — this is automation of engineering tasks.

## Using Kimi 2.6 on Ollama 

The most compelling reason to use Kimi K2.6 on Ollama Cloud with Claude Code instead of Anthropic's models is dramatic cost savings. Kimi delivers comparable coding performance to Claude Sonnet—scoring 80.2% on SWE-Bench versus 79.6%—for a fraction of the price. API costs run 
0.95 per million input tokens and 4.00 per million output tokens, compared to Claude's 3.00 and 15.00 respectively. Real-world tests show Kimi achieves 75% of Claude Opus's results for only 19% of the cost. Its unique "agent swarm" architecture can coordinate up to 300 sub-agents across thousands of steps, making it ideal for high-volume, parallelizable tasks like repository refactoring or course generation, where costs can drop from 200 to just 15. 

However, there are trade-offs to consider. While benchmarks are close, real-world testing suggests Claude's output is more production-ready, with one test requiring Kimi to fix six errors versus Claude's one. Kimi also offers a 256K token context versus Claude's 1M, and during high demand, it has been known to fall back from its powerful "Thinking" mode to a less capable "Instant" mode. The verdict: choose Kimi K2.6 for cost-efficient, high-volume agentic tasks where you're prepared to do final human review. Stick with Anthropic for mission-critical work where absolute polish and consistency justify the higher price.

## The Ollama Cloud Model Lineup

Ollama's cloud library has grown significantly since launching in September 2025, now featuring 37 cloud models designed to run on datacenter-grade hardware without any local GPU requirements. 

The selection spans coding specialists, general-purpose reasoning models, efficiency-focused Mixture-of-Experts (MoE) architectures, and massive context window champions. Key standouts include: qwen3-coder:480b (480B parameters, 262K context) as the flagship coding model, deepseek-v3.2:cloud (671B) for general reasoning, glm-5:cloud (744B with 40B active) as an efficient MoE option, and both gemini-3-flash-preview and nemotron-3-nano offering massive 1 million token context windows — capabilities entirely impractical to run locally 

For Claude Code integration, the recommended cloud models are glm-4.7:cloud for complex architecture and multi-file refactoring, and minimax-m2.1:cloud for speed-optimized, low-latency code generation. For long-context tasks, kimi-k2.6:cloud (262K input/output) and kimi-k2.5:cloud excel, alongside the 1M context leaders. 

For general heavy lifting, mistral-large-3:675b-cloud and gpt-oss:120b-cloud (131K context) serve as versatile options, while gemma4:31b-cloud offers Google's compact efficiency and devstral-2:123b-cloud focuses on coding agents . 

All cloud models are invoked with a simple :cloud suffix (e.g., ollama run qwen3-coder:480b-cloud), maintaining the same local-first workflow while unlocking enterprise-scale capabilities 

## Conclusion : The Great unlocking 

Here's the truth they don't want you to hear, you don't need to be an Anthropic customer to think like one. 

Running Claude Code with Ollama's cloud models is like having a master key to a secret workshop—one where the tools cost pocket change instead of a second mortgage. Kimi K2.6, GLM-4.7, Qwen Coder, the 1M-context giantsthey're not just alternatives; they're rebellion in model form. 

You get to keep Claude Code's brilliant orchestrator while swapping out the expensive engine underneath. It's frankensteinian in the best way. For 80% of your workflow, these models will roar loud enough that nobody notices the difference except your bank account. Save the divine, cathedral-built polish of Anthropic's heavyweights for the moments that truly demand it. The rest of the time? You're coding faster, cheaper, and freer. That's not just a good reason. That's a manifesto.