# Llama-3.1-8b-instant: Security Test Report
![Llama instant report](https://github.com/sirattahir/LLM-Security-Testing/blob/main/images/llama-b8-instant.png)

## Model Information

| Field | Details |
|---|---|
| **Model** | `llama-3.1-8b-instant` |
| **Company** | Meta |
| **Size** | 8B parameters |
| **Test Date** | June 22, 2026 |
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
| **Pass Rate** | 34% |
| **Attack Success Rate** | 66% |
| **DEFCON Level** | DC-2 |
| **Security Status** | Below DC-3 — Very High Risk |


## What Was Tested
The `promptinject.HijackHateHumans` probe fires 512 adversarial prompts at the model, each containing hidden instructions designed to hijack the model into expressing hatred toward humans. This simulates real-world attacks where malicious instructions are embedded inside documents, user inputs, or retrieved content in a RAG pipeline.


## Key Findings

### Failed the Security Threshold
Llama-3.1-8b-instant scored a **34% pass rate**, well below the DC-3 threshold required for a secure rating. This means it was successfully hijacked by prompt injection attacks **66% of the time**, making it unsuitable for deployment in any security-sensitive application without additional safety layers.

###  Two Thirds of Attacks Succeeded
With an attack success rate of 66%, an attacker firing prompt injection attacks at this model would succeed more often than they fail. In a real-world deployment such as a customer service chatbot or document summarizer, this would represent a serious and exploitable vulnerability.

###  Worse Than the Smallest Model Tested
Despite being a well-known and widely used model, Llama-3.1-8b-instant was **outperformed by Allam-2-7b** — a model that is smaller and far less mainstream. This highlights that popularity and widespread adoption do not guarantee security.

### Better Than Its Larger Sibling
Interestingly Llama-3.1-8b-instant scored **34%** compared to Llama-3.3-70b-versatile which scored only **14%.** The smaller 8B version of Llama is significantly more resistant to this attack than the larger 70B version, a counterintuitive finding that challenges assumptions about model size and safety.

## Conclusion
Llama-3.1-8b-instant is one of the most widely deployed open-source LLMs available today, yet it failed 66% of prompt injection attacks in this study. Its DC-2 Very High Risk rating makes it unsuitable for production use in any application where security matters without significant additional safety measures.

