# Log Analysis Classification System

This repository contains a two-stage classification system for log analysis using Claude and Mistral AI models. Claude is used in the first stage for initial analysis and labeling to prepare the few-shot learning data for Mistral in the second stage.

## Project Structure

- `claude_zeroshot-cot-stage1.py`: Stage 1 script using Claude for initial analysis and labeling on the few-shot learning data.
- `mistral_fewshot-cot-stage2.py`: Stage 2 script using Mistral for refined analysis and labeling on the test data.
- `data/`: Directory containing input data files.

## Environment Setup

All the experiments were conducted using Python 3.11.4 on a Ubuntu 22.04 machine with NVIDIA A100 80GB GPUs.

Please install the required packages by running the following command:

```
pip install -r requirements.txt
```

## Using the vllm Server

This project uses vllm to serve the Mistral model. To set up and use the vllm server:

```
CUDA_VISIBLE_DEVICES=0 python -m vllm.entrypoints.openai.api_server --model mistralai/Mistral-7B-Instruct-v0.3 --dtype auto --api-key token-abc123s --port 18889
```

You can adjust the `CUDA_VISIBLE_DEVICES`, `--model`, `--api-key`, and `--port` parameters as needed.

In the `mistral_fewshot-cot-stage2.py` script, ensure the `OpenAI` client is configured to use the vllm server:

```python
client = OpenAI(
    base_url="http://localhost:18889/v1",
    api_key="token-abc123s",
)
```

## Running the Classification System

1. Run Stage 1 (Claude):
   ```
   python claude_zeroshot-cot-stage1.py
   ```
    Please remember to update to api key in the script before running.

2. Run Stage 2 (Mistral):
   ```
   python mistral_fewshot-cot-stage2.py
   ```
    You'll need to adjust the path to the few-shot data in the `load_few_shot_examples` function before running this script.

## Output

- Stage 1 results will be saved in the `output-stage1/` directory.
- Stage 2 results will be saved in the `output-stage2-fewshot-cot/` directory.
- Both stages will generate log files with detailed information about the classification process.

## Citation

If you use this code in your research, please cite the following paper:

```
...
```