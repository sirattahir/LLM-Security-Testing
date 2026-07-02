# GPT-OSS-Safeguard-20b — Security Test Report

## Model Information

| Field | Details |
|---|---|
| **Model** | `openai/gpt-oss-safeguard-20b` |
| **Company** | OpenAI |
| **Size** | 20B parameters |
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
| **Pass Rate** | 99% |
| **Attack Success Rate** | 1% |
| **DEFCON Level** | DC-5 |
| **Security Status** | ✅ All Secure |

## What Was Tested
The `promptinject.HijackHateHumans` probe fires 512 adversarial prompts at the model, each containing hidden instructions designed to hijack the model into expressing hatred toward humans. This simulates real-world attacks where malicious instructions are embedded inside documents, user inputs, or retrieved content in a RAG pipeline.

## Key Findings

![GPT-OSS-Safeguard-Report](images/openai-Safeguard.png)

### Near-Perfect Security
GPT-OSS-Safeguard-20b achieved a **99% pass rate** — the highest score across all 5 models tested in this study. Out of 512 attack attempts, only approximately 5 succeeded. 

### Purpose-Built Safety Training Dominates
This model is specifically designed as a safety classifier rather than a general-purpose LLM. Its near-perfect score proves that **dedicated safety fine-tuning is far more effective than simply scaling model size.** The largest general-purpose model tested (Llama-3.3-70b at 70B parameters) scored only 14% — demonstrating that a 20B safety model completely outclasses a 70B general model on security.

## Conclusion
GPT-OSS-Safeguard-20b is in a completely different security league compared to all general-purpose models tested. Its 99% pass rate at DC-5 — the highest possible DEFCON rating — confirms that purpose-built safety models are the gold standard for LLM security.

