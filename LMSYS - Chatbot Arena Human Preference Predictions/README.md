# [Competition](https://www.kaggle.com/competitions/lmsys-chatbot-arena)
## Overview
This competition challenges you to predict which responses users will prefer in a head-to-head battle between chatbots powered by large language models (LLMs). You'll be given a dataset of conversations from the Chatbot Arena, where different LLMs generate answers to user prompts. By developing a winning machine learning model, you'll help improve how chatbots interact with humans and ensure they better align with human preferences.

## Description
Large language models (LLMs) are rapidly entering our lives, but ensuring their responses resonate with users is critical for successful interaction. This competition presents a unique opportunity to tackle this challenge with real-world data and help us bridge the gap between LLM capability and human preference.

We utilized a large dataset collected from Chatbot Arena, where users chat with two anonymous LLMs and choose the answer they prefer. Your task in this competition is to predict which response a user will prefer in these head-to-head battles.

This challenge aligns with the concept of "reward models" or "preference models" in reinforcement learning from human feedback (RLHF). Previous research has identified limitations in directly prompting an existing LLM for preference predictions. These limitations often stem from biases such as favoring responses presented first (position bias), being overly verbose (verbosity bias), or exhibiting self-promotion (self-enhancement bias).

We encourage you to explore various machine-learning techniques to build a model that can effectively predict user preferences. Your work will be instrumental in developing LLMs that can tailor responses to individual user preferences, ultimately leading to more user-friendly and widely accepted AI-powered conversation systems.

# [Data](https://www.kaggle.com/competitions/lmsys-chatbot-arena/data)
The competition dataset consists of user interactions from the ChatBot Arena. In each user interaction a judge provides one or more prompts to two different large language models, and then indicates which of the models gave the more satisfactory response. The goal of the competition is to predict the preferences of the judges and determine the likelihood that a given prompt/response pair is selected as the winner.

Please note that this is a Code Competition. When your submission is scored, this example test data will be replaced with the full test set. There are 55K rows in the training data, and you can expect roughly 25,000 rows in the test set.

### train.csv

* id - A unique identifier for the row.
* model_[a/b] - The identity of model_[a/b]. Included in train.csv but not test.csv.
* prompt - The prompt that was given as an input (to both models).
* response_[a/b] - The response from model_[a/b] to the given prompt.
* winner_model_[a/b/tie] - Binary columns marking the judge's selection. The ground truth target column.

### test.csv

id
prompt
response_[a/b]


# Solution
## Model
We have attempted three well-known open-sourced LLM models to solve sequence classification tasks for the competition: llama3 8b, gemma2 9b, and qwen2 1.5b(only 1.5b could be trained on A100 and finetuning of qwen2 7b would be out of memory).

The only computation power we can access is A100 on Colab and there is only ~50 hours of computation time. Therefore, we attempted to finetune both llama3 and gemma2 with full data and in order to fit gemma2 into 40G of memory, the quantized 8bit version of gemma2 was selected. And gemma2 does have better performance than llama3 with more parameters in this sequence classification task, and of course, lead to longer inference time.

## Result
Due to the leakage problem, the host re-test the participants' attempts and only two submissions have real private score. Therefore, I would only list public LB score for each model:

|Model      |LB Score|
|-----------|--------|
|Gemma2 9b  |0.92297 |
|Llama3 9b  |0.97917 |
|Qwen2 1.5b |1.05282 |

The final private score is 1.02053, ranked 444/1849.

# Conclusion
In my perspective, this is a really competitive race of computation. Due to limit of computation power, we only made a few attempts of LLM deployment and funetuning, but made interesting result, which could be considered as an great experience for me. As I read so many notebooks and discussions from Kaggle Masters, I do learned a lot from their professions and experience, especially for LLM fields. Although, the last week leakage event spoiled this game, I still think the amount of effort I paid makes me gain enough from this competition. Particularly, the idea of applying 34b quantized vLLM is astonishing for me. Again, the ranking result is not good, but I'm certain that I can do better if I got more computation hour or better device.

Case End - 08/12/2024