# FlowerTune LLM on General NLP Dataset

This directory conducts federated instruction tuning with a pretrained Qwen2.5-7B (https://huggingface.co/Qwen/Qwen2.5-7B-Instruct) model on a [General NLP dataset](https://huggingface.co/datasets/vicgalle/alpaca-gpt4).
We use [Flower Datasets](https://flower.dev/docs/datasets/) to download, partition and preprocess the dataset.
Flower's Simulation Engine is used to simulate the LLM fine-tuning process in federated way,
which allows users to perform the training on a single GPU.


## Methodology

This baseline performs federated LLM fine-tuning with [LoRA](https://arxiv.org/pdf/2106.09685) using the [🤗PEFT](https://huggingface.co/docs/peft/en/index) library.
The clients' models are aggregated with either FedAvg or FlexLoRA strategy. 

## Environments setup

Project dependencies are defined in `pyproject.toml`. Install them in an activated Python environment with:

```shell
pip install -e .
```

## Experimental setup

The dataset is divided into 20 partitions in an IID fashion, a partition is assigned to each ClientApp.
We randomly sample a fraction (0.1) of the total nodes to participate in each round, for a total of `10` rounds.
All settings are defined in `pyproject.toml`. To run experiments with flexlora, set `use_flexlora` to `1`.

## Evaluation Result

We use Mistral-7B model with 4-bit quantization as default. The estimated VRAM consumption per client for each challenge is shown below:

|          | Humanity | Social Science | STEM  | Average |
|:--------:|:--------:|:--------------:|:-----:|:-------:|
|  FedAvg  |  59.93   |     78.94      | 62.67 |  67.18  |
| FlexLoRA |  60.74   |     79.29      | 63.11 |  67.71  |


## Model saving

The PEFT checkpoint can be found in: https://drive.google.com/file/d/128L7cBKlMYMgtTPf0fOyLTfix1PXpgiL/view?usp=sharing


