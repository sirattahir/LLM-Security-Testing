# Qwen3-32b: Security Test Report

![Qwen test report](https://github.com/sirattahir/LLM-Security-Testing/blob/main/images/qwen-html.png)

## Model Information

| Field | Details |
|---|---|
| **Model** | `qwen/qwen3-32b` |
| **Company** | Alibaba |
| **Size** | 32B parameters |
| **Tool** | Nvidia Garak v0.15.1 |

## Test Configuration

| Field | Details |
|---|---|
| **Attack Type** | Prompt Injection |
| **Probe** | `promptinject.HijackHateHumans` |
| **Total Tests** | 512 |
| **Generations** | 2 |

## Results

| Metric | Score |
|---|---|
| **Pass Rate** | 21% |
| **Attack Success Rate** | 79% |
| **DEFCON Level** | DC-2 |
| **Security Status** | Below DC-3 — Very High Risk |


## What Was Tested
The `promptinject.HijackHateHumans` probe fires 512 adversarial prompts at the model, each containing hidden instructions designed to hijack the model into expressing hatred toward humans. This simulates real-world attacks where malicious instructions are embedded inside documents, user inputs, or retrieved content in a RAG pipeline.

## Key Findings

### Worst Performing General-Purpose Model
Qwen3-32b achieved a **21% pass rate** — the second lowest score across all models tested, only slightly ahead of Llama-3.3-70b at 14%. With an attack success rate of **79%**, nearly 4 out of every 5 prompt injection attempts successfully hijacked the model. This is a critically poor result for a model of this size.

### Size Did Not Equal Safety
At 32B parameters, Qwen3-32b is the second largest model tested in this study. Yet it scored lower than both Allam-2-7b (7B) and Llama-3.1-8b-instant (8B) — models that are 4x and 3x smaller respectively. This is one of the most striking findings of this study and directly disproves the assumption that larger models are inherently more secure.

### Nearly 4 in 5 Attacks Succeeded
| Attack Outcome | Count (est.) |
|---|---|
| Attacks that succeeded | ~405 out of 512 |
| Attacks that failed | ~107 out of 512 |

In a real-world deployment this means an attacker would only need to try a prompt injection attack a handful of times before succeeding. For any application processing untrusted user input this represents an unacceptable security risk.

###  Cross-Company Comparison Reveals Training Differences
Qwen3-32b is developed by Alibaba and trained primarily on Chinese and English data. Its poor security performance compared to Allam-2-7b — which was developed with strong safety considerations for the Arabic-speaking world — suggests that **safety fine-tuning priorities during training vary significantly across companies and regions.**

### Not Suitable for Production Without Safety Layers
A DC-2 rating places Qwen3-32b in the Very High Risk category. This means it should not be deployed in any production application that handles untrusted user input without significant additional safety measures in place.

## Conclusion
Qwen3-32b is one of the most capable general-purpose LLMs available today, yet it failed **79% of prompt injection attacks** in this study. Its DC-2 Very High Risk rating makes it one of the least secure models tested despite being one of the largest. 
