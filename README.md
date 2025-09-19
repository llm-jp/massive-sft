# massive-sft

## Details of Evaluation Results

We evaluated over **1,000 models** on downstream tasks using [OpenCompass](https://github.com/open-compass/opencompass), an LLM evaluation tool.  
For details on the datasets and metrics, please refer to our paper.  

This repository provides a crawled and consolidated **dataframe** of the evaluation results.

### Dataframe Format

The dataframe consists of metadata about each evaluated model along with scores for downstream tasks:

- **`model_name`**: The name of the model family  
- **`data_name`**: The name of the dataset used for SFT.  
  - `all` refers to a merged dataset containing all 10 datasets  
- **`lora`**:  
  - `true`: LoRA tuning  
  - `false`: Full parameter tuning  
- **`epoch`**: The number of epochs each trained model was run on the dataset specified in `data_name`  
- **`data_size`**: The number of samples in the training dataset  
- **`lr_strategy`**: Indicates whether learning rate scheduling used  
  - `cosine` decay  
  - or was kept `constant`

## Estimated Evaluation Time

As you may know, we spent a tremendous amount of time on model evaluation.  
Unfortunately, due to unexpected runtime errors and GPU server failures, it is difficult to report the exact evaluation time.  
Therefore, this repository provides an **approximate estimation** instead.  

From our experience, evaluation time is largely affected by two factors:
1. The **model family**, and  
2. Whether inference uses a **LoRA adapter** or **not**.  

To better estimate this, we conducted additional verification by weight-merging LoRA-tuned and fully tuned models for each model family, thereby constructing representative models under each condition.  
By measuring the evaluation time of these representative models, we can approximate the expected runtime.

### Approximate Results (in seconds)

| Model Family        | 0-shot (full) | few-shot (full) | 0-shot (LoRA) | few-shot (LoRA) | Approx. Total (hours) |
|---------------------|---------------|-----------------|---------------|-----------------|------------------------|
| Chinese-Llama3 (8B) | 5407          | 36845           | 6648          | 38159           | 1,741,180 (484h)       |
| Chinese-Mistral (7B)| 10950         | 45861           | 7037          | 37715           | 2,031,260 (564h)       |
| Gemma2 (9B)         | 4171          | 16287           | 9790          | 63519           | 1,650,032 (458h)       |
| Llama3 (8B)         | 4890          | 26568           | 6473          | 37426           | 1,507,140 (419h)       |
| LLMjp-3 (7B)        | 2505          | 15366           | 7453          | 43886           | 4,761,819 (1323h)      |
| Mistral (7B)        | 5937          | 40976           | 174795        | OOM             | 4,434,160 (1232h)      |
| OLMo (7B)           | 2776          | 13565           | 34200*        | 120600*         | 6,674,679 (1854h)      |
| Qwen2.5 (7B)        | 1809          | 8032            | 6106          | 33204           | 2,842,969 (790h)       |
| Sarashina2 (7B)     | 2757          | 12163           | 7728          | 43305           | 1,319,060 (366h)       |
| Swallow-Mistral (7B)| 8451          | 26000           | 6669          | 36878           | 1,559,960 (433h)       |
| Yi1.5 (9B)          | 2888          | 11119           | 8693          | 53763           | 1,529,260 (425h)       |

\* For **OLMo (7B)**, LoRA values were estimated from logs since weight merging was not supported (evaluated without VLLM).  
OOM = Out of Memory.  

---

### Notes
- All times above are measured with **1 GPU** only.  
  In practice, evaluation can be accelerated by `#nodes × #GPUs`.  
- These results are **rough estimates** and are extremely difficult to reproduce in subsequent experiments.  

We hope this information will be useful as a reference.  
