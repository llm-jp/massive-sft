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
