# [Competition](https://www.kaggle.com/competitions/ai-mathematical-olympiad-prize/overview)
The ability to reason mathematically is a critical milestone for AI. Mathematical reasoning is the foundation for solving many complex problems, from engineering marvels to intricate financial models. However, current AI capabilities are limited in this area.

The AI Mathematical Olympiad (AIMO) Prize is a new $10mn prize fund to spur the open development of AI models capable of performing as well as top human participants in the International Mathematical Olympiad (IMO).
This competition includes 110 problems similar to an intermediate-level high school math challenge. The Gemma 7B benchmark for these problems is 3/50 on the public and private test sets.

The assessment of AI models' mathematical reasoning skills faces a significant hurdle, the issue of train-test leakage. Models trained on Internet-scale datasets may inadvertently encounter test questions during training, skewing the evaluation process.

To address this challenge, this competition uses a dataset of 110 novel math problems, created by an international team of problem solvers, recognizing the need for a transparent and fair evaluation framework. The dataset encompasses a range of difficulty levels, from simple arithmetic to algebraic thinking and geometric reasoning. This will help to strengthen the benchmarks for assessing AI models' mathematical reasoning skills, without the risk of contamination from training data.

This competition offers an exciting opportunity to benchmark open AI models against each other and foster healthy competition and innovation in the field. By addressing this initial benchmarking problem, you will contribute to advancing AI capabilities and help to ensure that its potential benefits outweigh the risks.

Join us as we work towards a future where AI models’ mathematical reasoning skills are accurately and reliably assessed, driving progress and innovation across industries.

# Starter Code

starter code is forked from https://www.kaggle.com/code/abdurrafae/improved-code-interpretation

# Directory Structure
- Root/
  - Kaggle/
    - Input/
        - ai-mathematical-olympiad-prize/
            - test.csv
            - train.csv
        - deepseek-math/
            - model
            - config.json
            - tokenizer.json
    - Working/
        - submission.csv
  - updated-code-interpretation-n-repetitions-17.ipynb


# Model

This notebook applied zero-shot MMOS-DeepSeekMath-7B with self-consistency and generated code reasoning evaluation.

Self-consistency is a modification of the standard greedy decoding in reasoning pipelines via sampling several diverse answers followed by aggregation, e.g., most common answer ([SC-CoT paper](https://arxiv.org/pdf/2203.11171.pdf)).

In this kernel, we will consider MMOS-DeepSeekMath-7B RL-tuned backbone; in my experiments, this model produces more consistent code reasoning and the code block execution will allow us to decrease arithmetic hallucinations.