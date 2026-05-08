
## ❗❗ For Reviewers

### Released Resources

- For the FrameRef dataset, click [here](dataset/frameref-split).
- For the dataset creation raw output, click [here](dataset/frameref-raw).
- For the trained model adapters, click [here](adapters).





# Stability Regimes for Framing-Sensitive Fine-Tuning in Language Models

AI systems increasingly shape how individuals access and evaluate information, intensifying concerns about misinformation. Computational simulation offers a controlled complement to direct empirical study, with fine-tuned LLMs enabling powerful agent-based simulations. However, fine-tuning often induces broad behavioral shifts including bias drift, degenerate heuristics, and loss of task competence, which undermine experimental validity. The central challenge is inducing localized decision shifts without global behavioral collapse. We study this through a stability analysis of supervised fine-tuning, attenuating loss on selected training slices to shift false-claim acceptance while preserving overall task competence. We introduce *FrameRef*, a large-scale dataset of semantically equivalent claims with controlled surface framings across five dimensions (Authoritative, Consensus, Emotional, Sensationalist, Prestige), with human validation confirming systematic framing effects on claim acceptance. We identify stability regimes in which targeted error shifts can be induced without degrading aggregate accuracy or calibration. A sequential exposure task over *FrameRef* shows that small framing-conditioned shifts compound into substantially different cumulative outcomes under feedback, but largely disappear when feedback is removed, confirming that interventions modify specific decision tendencies rather than global performance.



## Repository Structure

- `config/` — configuration files and experiment parameters
- `frameref/` — project source code
  - `dataset/` - dataset generation
  - `evaluation/` - model evaluation and scoring
  - `experiments/` - model training
  - `human_eval/` - human evaluation tools
- `utils/` — support tools


## Getting Started

Create a file `config/config.yaml` with data and models paths as shown below.

```yaml
paths:
  proj_store: "/data/to/data/" # Actual path to data
  models: "/data/to/models" # Actual path to models
```


### Dataset Generation

- Download the datasets using `python utils/download_data.py`. The script will download the following:
  - [FEVER](https://fever.ai/dataset/fever.html) (~36 MB unzipped)
  - [FEVEROUS](https://fever.ai/dataset/feverous.html) (~187 MB unzipped)
- `meta-llama/Llama-3.1-8B-Instruct` is available [here](https://huggingface.co/meta-llama/Llama-3.1-8B-Instruct/).
- `deepseek-ai/DeepSeek-R1-Distill-Llama-8B` is available [here](https://huggingface.co/deepseek-ai/DeepSeek-R1-Distill-Llama-8B).
- Follow the scripts on the `frameref/dataset/` folder for dataset generation.


### Model Training

- Define training settings in `config/training_params.yaml` and `config/accelerate_config.yaml`.
- Run a training experiment directly using `frameref/experiments/supervised_finetuning.py`
- `frameref/experiments/supervised_finetuning_large_models.py` is optimized for large models.

### Model Evaluation

- Evaluation logic and metrics are implemented in `frameref/evaluation/`.
- Scripts for running trajectories and evaluating them are included here.


## Typical Pipeline

- Fine-tune models: `frameref/experiments/supervised_finetuning.py`.
- Run diagnostic evaluations (sample size and $\alpha$): `frameref/evaluation/diagnostic_model_evaluate.py`.
- Run trajectory simulation: `frameref/evaluation/trajectory_model_evaluate.py`.



