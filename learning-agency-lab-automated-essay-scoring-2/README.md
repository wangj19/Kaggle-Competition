# Competition Introduction
The first automated essay scoring competition to tackle automated grading of student-written essays was twelve years ago. How far have we come from this initial competition? With an updated dataset and light years of new ideas we hope to see if we can get to the latest in automated grading to provide a real impact to overtaxed teachers who continue to have challenges with providing timely feedback, especially in underserved communities.

The goal of this competition is to train a model to score student essays. Your efforts are needed to reduce the high expense and time required to hand grade these essays. Reliable automated techniques could allow essays to be introduced in testing, a key indicator of student learning that is currently commonly avoided due to the challenges in grading.

Competition Link: https://www.kaggle.com/competitions/learning-agency-lab-automated-essay-scoring-2

# Directory Structure
- Root/
  - Kaggle/
    - Input/
        - learning-agency-lab-automated-essay-scoring/
          - test.csv
          - train.csv
        - essay-embedding-v1/
          - Model1-embedding/
          - Model2-embedding/
          - ...
        - Download HuggingFace Model/
          - Model1/
          - Model2/
          - ...

    - Working/
        - submission.csv
  - playground.ipynb

# Code Starter
I draft my code from two open-source notebook. One notebook implements feature engineering based on the texts to expand features, including paragraph, sentence, and word-based features. It also contains character and word TFIDF features. All of these feature augmentation finally provides over 3800 features for the ***LGBM regressor*** to generate predictions with 5-fold train and validation datasets. The original notebook link: https://www.kaggle.com/code/deepaksingh47/feature-engineeing-lgbm

The second notebook employed 6 LLM models to process text embedding and concatenate these 6 sets of embeddings together as features. However, the original auther applies a model called ***RAPIDS SVR*** developed by Nvidia while the author is affiliated with Nvidia. The starter code link：https://www.kaggle.com/code/cdeotte/rapids-svr-starter-cv-0-830-lb-0-804. However, for easier application and higher performance, I chose to change the final model to MLP model. The MLP model link: https://www.kaggle.com/code/innotechryan/rapids-svr-starter-cv-0-830-lb-0-800/notebook. The dataset is folded 10 time to generate 10 models and their corresponding predictions.

There are 15 predictions generated from two types of models while LGBM models generate floats and MLP model dense to integer, I finally compute the avarage and round it as my final prediction.