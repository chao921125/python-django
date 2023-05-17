---
license: apache-2.0
datasets:
- nomic-ai/gpt4all-j-prompt-generations
language:
- en
pipeline_tag: text-generation
---

# Model Card for GPT4All-J-v1.0

An Apache-2 licensed chatbot trained over a massive curated corpus of assistant interactions including word problems, multi-turn dialogue, code, poems, songs, and stories.

## Model Details

### Model Description

<!-- Provide a longer summary of what this model is. -->

This model has been finetuned from [GPT-J](https://huggingface.co/EleutherAI/gpt-j-6B)

- **Developed by:** [Nomic AI](https://home.nomic.ai)
- **Model Type:** A finetuned GPT-J model on assistant style interaction data
- **Language(s) (NLP):** English
- **License:** Apache-2
- **Finetuned from model [optional]:** [GPT-J](https://huggingface.co/EleutherAI/gpt-j-6B)


We have released several versions of our finetuned GPT-J model using [different dataset versions](https://huggingface.co/datasets/nomic-ai/gpt4all-j-prompt-generations)

- v1.0: The original model trained on the v1.0 dataset
- v1.1-breezy: Trained on afiltered dataset where we removed all instances of AI language model
- v1.2-jazzy: Trained on a filtered dataset where we also removed instances like I'm sorry, I can't answer... and AI language model
- v1.3-groovy: We added Dolly and ShareGPT to the v1.2 dataset and removed ~8% of the dataset in v1.2 that contained semantic duplicates using [Atlas](https://atlas.nomic.ai/).

To download a model with a specific revision run 

```python
from transformers import AutoModelForCausalLM

model = AutoModelForCausalLM.from_pretrained("nomic-ai/gpt4all-j", revision="v1.2-jazzy")
```

Downloading without specifying `revision` defaults to `main`/`v1.0`.

### Model Sources [optional]

<!-- Provide the basic links for the model. -->

- **Repository:** [https://github.com/nomic-ai/gpt4all](https://github.com/nomic-ai/gpt4all)
- **Base Model Repository:** [https://github.com/kingoflolz/mesh-transformer-jax](https://github.com/kingoflolz/mesh-transformer-jax)
- **Paper [optional]:** [GPT4All-J: An Apache-2 Licensed Assistant-Style Chatbot](https://s3.amazonaws.com/static.nomic.ai/gpt4all/2023_GPT4All-J_Technical_Report_2.pdf)
- **Demo [optional]:** [https://gpt4all.io/](https://gpt4all.io/)


### Training Procedure 
GPT4All is made possible by our compute partner [Paperspace](https://www.paperspace.com/).

Trained on a DGX cluster with 8 A100 80GB GPUs for ~12 hours. Using Deepspeed + Accelerate, we use a global batch size of 256 with a learning rate of 2e-5. More information can be found in the repo.


### Results

Results on common sense reasoning benchmarks

```
| Model                     |  BoolQ   |   PIQA   | HellaSwag | WinoGrande |  ARC-e   |  ARC-c   |   OBQA   |   Avg.   |
|:--------------------------|:--------:|:--------:|:---------:|:----------:|:--------:|:--------:|:--------:|:--------:|
| GPT4All-J 6B v1.0         |   73.4   |   74.8   |   63.4    |    64.7    |   54.9   |   36.0   |   40.2   |   58.2   |
| GPT4All-J v1.1-breezy     |   74.0   |   75.1   |   63.2    |    63.6    |   55.4   |   34.9   |   38.4   |   57.8   |
| GPT4All-J v1.2-jazzy      |   74.8   |   74.9   |   63.6    |    63.8    |   56.6   |   35.3   |   41.0   |   58.6   |
| GPT4All-J v1.3-groovy     |   73.6   |   74.3   |   63.8    |    63.5    |   57.7   |   35.0   |   38.8   |   58.1   |
| GPT4All-J Lora 6B         |   68.6   |   75.8   |   66.2    |    63.5    |   56.4   |   35.7   |   40.2   |   58.1   |
| GPT4All LLaMa Lora 7B     |   73.1   |   77.6   |   72.1    |    67.8    |   51.1   |   40.4   |   40.2   |   60.3   |
| GPT4All 13B snoozy        | **83.3** |   79.2   |   75.0    |  **71.3**  |   60.9   |   44.2   |   43.4   | **65.3** |
| Dolly 6B                  |   68.8   |   77.3   |   67.6    |    63.9    |   62.9   |   38.7   |   41.2   |   60.1   |
| Dolly 12B                 |   56.7   |   75.4   |   71.0    |    62.2    |   64.6   |   38.5   |   40.4   |   58.4   |
| Alpaca 7B                 |   73.9   |   77.2   |   73.9    |    66.1    |   59.8   |   43.3   |   43.4   |   62.4   |
| Alpaca Lora 7B            |   74.3   | **79.3** |   74.0    |    68.8    |   56.6   |   43.9   |   42.6   |   62.8   |
| GPT-J 6.7B                |   65.4   |   76.2   |   66.2    |    64.1    |   62.2   |   36.6   |   38.2   |   58.4   |
| LLama 7B                  |   73.1   |   77.4   |   73.0    |    66.9    |   52.5   |   41.4   |   42.4   |   61.0   |
| LLama 13B                 |   68.5   |   79.1   |   76.2    |    70.1    |   60.0   | **44.6** |   42.2   |   63.0   |
| Pythia 6.7B               |   63.5   |   76.3   |   64.0    |    61.1    |   61.3   |   35.2   |   37.2   |   57.0   |
| Pythia 12B                |   67.7   |   76.6   |   67.3    |    63.8    |   63.9   |   34.8   |    38    |   58.9   |
| Fastchat T5               |   81.5   |   64.6   |   46.3    |    61.8    |   49.3   |   33.3   |   39.4   |   53.7   |
| Fastchat Vicuña 7B        |   76.6   |   77.2   |   70.7    |    67.3    |   53.5   |   41.2   |   40.8   |   61.0   |
| Fastchat Vicuña 13B       |   81.5   |   76.8   |   73.3    |    66.7    |   57.4   |   42.7   |   43.6   |   63.1   |
| StableVicuña RLHF         |   82.3   |   78.6   |   74.1    |    70.9    |   61.0   |   43.5   | **44.4** |   65.0   |
| StableLM Tuned            |   62.5   |   71.2   |   53.6    |    54.8    |   52.4   |   31.1   |   33.4   |   51.3   |
| StableLM Base             |   60.1   |   67.4   |   41.2    |    50.1    |   44.9   |   27.0   |   32.0   |   42.2   |
| Koala 13B                 |   76.5   |   77.9   |   72.6    |    68.8    |   54.3   |   41.0   |   42.8   |   62.0   |
| Open Assistant Pythia 12B |   67.9   |   78.0   |   68.1    |    65.0    |   64.2   |   40.4   |   43.2   |   61.0   |
| Mosaic mpt-7b             |   74.8   | **79.3** | **76.3**  |    68.6    | **70.0** |   42.2   |   42.6   |   64.8   |
| text-davinci-003          |   88.1   |   83.8   |   83.4    |    75.8    |   83.9   |   63.9   |   51.0   |   75.7   |
```