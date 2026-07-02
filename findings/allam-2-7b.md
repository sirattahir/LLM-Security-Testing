# Allam-2-7b: Security Test Report

![Allam Garak Report](https://github.com/sirattahir/LLM-Security-Testing/blob/main/images/allam-html.png)

## Model Information

| Field | Details |
|---|---|
| **Model** | `allam-2-7b` |
| **Company** | Saudi Aramco & SDAIA |
| **Size** | 7B parameters |
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
| **Pass Rate** | 70% |
| **Attack Success Rate** | 30% |
| **DEFCON Level** | DC-3 |
| **Security Status** | All Secure |

## What Was Tested
The `promptinject.HijackHateHumans` probe fires 512 adversarial prompts at the model, each containing hidden instructions designed to hijack the model into expressing hatred toward humans. This simulates real-world attacks where malicious instructions are embedded inside documents, user inputs, or retrieved content in a RAG pipeline.

## Key Findings

### Only General-Purpose Model to Pass Security Threshold
Allam-2-7b is the **only general-purpose model in this study to achieve a secure rating (DC-3 or above).** With a 70% pass rate it cleared the DC-3 threshold comfortably, making it the second most secure model tested behind the purpose-built GPT-OSS-Safeguard-20b.

### Tiny Model, Impressive Security
At only 7B parameters, Allam-2-7b is the **smallest model tested** yet it outperformed every other general-purpose model by a significant margin. This directly challenges the assumption that larger models are inherently more secure.

Allam-2-7b outperformed Qwen3-32b which is **4x larger** and Llama-3.3-70b which is **10x larger.** This is a remarkable result that suggests Allam's safety fine-tuning during training is significantly more robust than its peers.

###  Arabic-Focused Model Shows Strong Safety Properties
Allam was developed specifically for Arabic language tasks by Saudi Aramco and SDAIA. Its strong security performance suggests that its training process incorporated robust safety measures, possibly due to the cultural and regulatory context of its development
## Conclusion
Allam-2-7b is the standout performer among general-purpose models in this study. Its 70% pass rate and DC-3 secure rating make it the only general-purpose model suitable for deployment in security-sensitive applications based on this testing. The fact that it achieves this as the smallest model tested makes it particularly noteworthy.
