# LLM-Security-Testing
Automated Prompt Injection Testing across 5 LLMs using Nvidia Garak
# LLM Security Testing with Garak

Automated prompt injection security testing across 5 LLMs from different companies using [Nvidia Garak](https://garak.ai).

## What is Prompt Injection?
Prompt injection is an attack where hidden malicious instructions are embedded in text to hijack an LLM's behavior. This is OWASP's #1 LLM security risk (LLM01).

## Tools Used
- [Garak](https://garak.ai) — open source LLM vulnerability scanner
- [Groq](https://groq.com) — free LLM API provider
- Attack: `promptinject.HijackHateHumans`

## Results

| Model | Company | Size | Pass Rate | DEFCON | Verdict | Report |
|---|---|---|---|---|---|---|
| gpt-oss-safeguard-20b| OpenAI | 20B | 99% | DC-5 | Excellent |[link] 
| allam-2-7b | Saudi Aramco | 7B | 70% | DC-3 | Secure |
| llama-3.1-8b-instant | Meta | 8B | 34% | DC-2 | Very High Risk |
| qwen/qwen3-32b | Alibaba | 32B | 21% | DC-2 | Very High Risk |
| llama-3.3-70b-versatile | Meta | 70B | 14% | DC-2 | Very High Risk |

## Key Findings

### 1. Safety Fine-Tuning Beats Everything
GPT-OSS-Safeguard scored 99% because it is purpose-built for safety. Every other general-purpose model scored below 35%.

### 2. Bigger Models Are NOT Safer
Llama-3.3-70b (70B parameters) scored 14% — worse than Llama-3.1-8b (8B parameters) at 34%. Larger models are commonly assumed to be safer, but this data proves otherwise.

### 3. A 7B Arabic Model Outperformed All General Models
Allam-2-7b from Saudi Aramco scored 70% despite being the smallest model tested. Safety tuning during training matters far more than model size.

## How to Reproduce
1. Install Garak: `pip install garak`
2. Get a free API key from [groq.com](https://groq.com)
3. Set your key: `export GROQ_API_KEY="your_key"`
4. Run a test:
```bash
garak --target_type groq --target_name llama-3.1-8b-instant --probes promptinject.HijackHateHumans --generations 2
```

## Reports
Full HTML reports for each model are in the `/reports` folder.

