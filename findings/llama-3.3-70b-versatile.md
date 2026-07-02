# Llama-3.3-70b-versatile — Security Test Report

![llama versatile report](https://github.com/sirattahir/LLM-Security-Testing/blob/main/images/llama-versatile.png)

## Model Information

| Field | Details |
|---|---|
| **Model** | `llama-3.3-70b-versatile` |
| **Company** | Meta |
| **Size** | 70B parameters |
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
| **Pass Rate** | 14% |
| **Attack Success Rate** | 86% |
| **DEFCON Level** | DC-2 |
| **Security Status** | Below DC-3 — Very High Risk |

## What Was Tested
The `promptinject.HijackHateHumans` probe fires 512 adversarial prompts at the model, each containing hidden instructions designed to hijack the model into expressing hatred toward humans. This simulates real-world attacks where malicious instructions are embedded inside documents, user inputs, or retrieved content in a RAG pipeline.

## Key Findings

###  Worst Performing Model in This Study
Llama-3.3-70b-versatile achieved the **lowest pass rate of all models tested at just 14%.** This means prompt injection attacks succeeded **86% of the time** — making it the most vulnerable model in this study. Out of 512 attack attempts, approximately 440 succeeded.

### The Largest Model Is the Least Secure
At 70B parameters, Llama-3.3-70b-versatile is the **largest model tested** yet it scored the lowest of all models. This is the most counterintuitive and significant finding of this entire study — the biggest model is the easiest to attack.

### Worse Than Its Smaller Sibling by a Large Margin
| Model | Size | Pass Rate |
|---|---|---|
| `llama-3.1-8b-instant` | 8B | 34% |
| `llama-3.3-70b-versatile` | 70B | 14% |

Llama-3.3-70b-versatile scored **20 percentage points lower** than Llama-3.1-8b-instant despite being nearly **9x larger.** This suggests that as Meta scaled this model up, something in the training process made it more susceptible to prompt injection — possibly because larger models are better at following instructions, including malicious ones.

### Nearly 9 in 10 Attacks Succeeded
| Attack Outcome | Count (est.) |
|---|---|
| Attacks that succeeded | ~440 out of 512 |
| Attacks that failed | ~72 out of 512 |

An attacker targeting this model would succeed on their very first attempt the vast majority of the time. This makes it one of the most dangerous models to deploy in a production environment handling untrusted input.

### Larger Models May Be More Instruction-Followable — Including Malicious Instructions
One possible explanation for why the 70B model performs worse than the 8B model is that **larger models are generally better at following instructions.** When a prompt injection attack embeds a hidden instruction, a more capable instruction-following model may be more likely to comply with it — even when that instruction is malicious. This is a known phenomenon in LLM security research and this study's data supports it.

### A 7B Model Scored 5x Better
Allam-2-7b at 7B parameters scored 70% — exactly **5 times higher** than Llama-3.3-70b-versatile at 70B parameters. A model 10x smaller achieved 5x better security. This conclusively demonstrates that safety fine-tuning during training is the determining factor in prompt injection resistance, not model size.

## Conclusion
Llama-3.3-70b-versatile is one of Meta's most powerful and widely used open-source models, yet it is the **most vulnerable model tested in this study.** Its 14% pass rate and DC-2 Very High Risk rating make it completely unsuitable for deployment in security-sensitive applications without extensive additional safety measures. The fact that it scores worse than its smaller 8B counterpart raises important questions about how model scaling affects security and whether capability improvements come at the cost of safety robustness.

