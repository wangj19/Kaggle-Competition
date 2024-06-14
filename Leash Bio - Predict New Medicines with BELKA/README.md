# [Competition Introduction](https://www.kaggle.com/competitions/leash-BELKA/overview)
## Overview
In this competition, you’ll develop machine learning (ML) models to predict the binding affinity of small molecules to specific protein targets – a critical step in drug development for the pharmaceutical industry that would pave the way for more accurate drug discovery. You’ll help predict which drug-like small molecules (chemicals) will bind to three possible protein targets.

## Description
Small molecule drugs are chemicals that interact with cellular protein machinery and affect the functions of this machinery in some way. Often, drugs are meant to inhibit the activity of single protein targets, and those targets are thought to be involved in a disease process. A classic approach to identify such candidate molecules is to physically make them, one by one, and then expose them to the protein target of interest and test if the two interact. This can be a fairly laborious and time-intensive process.

The US Food and Drug Administration (FDA) has approved roughly 2,000 novel molecular entities in its entire history. However, the number of chemicals in druglike space has been estimated to be 10^60, a space far too big to physically search. There are likely effective treatments for human ailments hiding in that chemical space, and better methods to find such treatments are desirable to us all.

To evaluate potential search methods in small molecule chemistry, competition host Leash Biosciences physically tested some 133M small molecules for their ability to interact with one of three protein targets using DNA-encoded chemical library (DEL) technology. This dataset, the Big Encoded Library for Chemical Assessment (BELKA), provides an excellent opportunity to develop predictive models that may advance drug discovery.

Datasets of this size are rare and restricted to large pharmaceutical companies. The current best-curated public dataset of this kind is perhaps bindingdb, which, at 2.8M binding measurements, is much smaller than BELKA.

This competition aims to revolutionize small molecule binding prediction by harnessing ML techniques. Recent advances in ML approaches suggest it might be possible to search chemical space by inference using well-trained computational models rather than running laboratory experiments. Similar progress in other fields suggest using ML to search across vast spaces could be a generalizable approach applicable to many domains. We hope that by providing BELKA we will democratize aspects of computational drug discovery and assist the community in finding new lifesaving medicines.

Here, you’ll build predictive models to estimate the binding affinity of unknown chemical compounds to specified protein targets. You may use the training data provided; alternatively, there are a number of methods to make small molecule binding predictions without relying on empirical binding data (e.g. DiffDock, and this contest was designed to allow for such submissions).

Your work will contribute to advances in small molecule chemistry used to accelerate drug discovery.

# [Data](https://www.kaggle.com/competitions/leash-BELKA/data)
## Overview
[train/test].[csv/parquet] - The train or test data, available in both the csv and parquet formats.

**id** - A unique example_id that we use to identify the molecule-binding target pair.
**buildingblock1_smiles** - The structure, in SMILES, of the first building block
**buildingblock2_smiles** - The structure, in SMILES, of the second building block
**buildingblock3_smiles** - The structure, in SMILES, of the third building block
**molecule_smiles** - The structure of the fully assembled molecule, in SMILES. This includes the three building blocks and the triazine core. Note we use a [Dy] as the stand-in for the DNA linker.
**protein_name** - The protein target name
**binds** - The target column. A binary class label of whether the molecule binds to the protein. Not available for the test set.
sample_submission.csv - A sample submission file in the correct format

## Competition data
All data were generated in-house at Leash Biosciences. We are providing roughly 98M training examples per protein, 200K validation examples per protein, and 360K test molecules per protein. To test generalizability, the test set contains building blocks that are not in the training set. These datasets are very imbalanced: roughly 0.5% of examples are classified as binders; we used 3 rounds of selection in triplicate to identify binders experimentally. Following the competition, Leash will make all the data available for future use (3 targets * 3 rounds of selection * 3 replicates * 133M molecules, or 3.6B measurements).

## Target
Proteins are encoded in the genome, and names of the genes encoding those proteins are typically bestowed by their discoverers and regulated by the Hugo Gene Nomenclature Committee. The protein products of these genes can sometimes have different names, often due to the history of their discovery.

We screened three protein targets for this competition: ***EPHX2 (sEH)***, ***BRD4***, ***ALB (HSA)***



# [Model 1 - 1D CNN model](https://www.kaggle.com/code/ahmedelfazouan/belka-1dcnn-starter-with-all-data/notebook)
This "belka-1dcnn-starter-with-all-data" employed 1D-CNN model for prediction. There are 142 encoded features used as input and the model finally denses to 3 as prediction of bind. Due to the huge size of dataset, I built the train set into 15 fold and selected 3 of them for model-training and 10 epochs for each fold, which means only 1/5 data was used for training. The final score of average prediction of 3 folds on LeaderBoard is 0.400.

## Directory Structure
- Root/
  - Kaggle/
    - Input/
        - leash-predict-chemical-bindings/
          - test.csv
          - test.parquet
          - train.csv
          - train.parque
          - sample_submission.csv 
    - Working/
        - submission.csv
        - model-0.h5
        - model-1.h5
        - model-2.h5
  - belka-1dcnn-starter-with-all-data.ipynb


  # [Model 2 - Xgb model](https://www.kaggle.com/code/ricopue/leashbio-xgb-ecfp-10m-sample-rows)
  This notebook employs encoded [ECFP](https://www.kaggle.com/code/ricopue/leashbio-create-10m-sample-data-and-ecfp) features (approximately 2000 features), and applys ***VarianceThreshold*** from sklearn package to filter them into 1300 features. The simple XGB model is applied without tunning and GPU usage. All of 9.5M data are used and 3000 iterations are planned for training. The original code reaches LB score of 0.369 and this original submission are used for my ensembling.

## Directory Structure
- Root/
  - Kaggle/
    - Input/
        - leash-predict-chemical-bindings/
          - test.csv
          - test.parquet
          - train.csv
          - train.parque
          - sample_submission.csv
        - [LeashBio - Create 10M Sample Data and ecfp](https://www.kaggle.com/code/ricopue/leashbio-create-10m-sample-data-and-ecfp)/
          - test_ecfp.npz
          - train-ecfp.npz
    - Working/
        - submission.csv
  - leashbio-xgb-ecfp-10m-sample-rows.ipynb

  # [Model 3 - AutoML](https://www.kaggle.com/code/mehrankazeminia/5-belka-submission-autogluon-frag1-2-3)
  The author of [these notebooks](https://www.kaggle.com/datasets/mehrankazeminia/belka-frag-1/code) attempted many models including XGB, LGBM and KNN. For this particular notebook, autogluon machine learning model is employed. And due to the large size of dataset, train set are split into three folds and predictions of three autoML models are combined. This notebook also did ensembling process to merge results of XGB and LGBM models, which I didn't include but considered for future improvement. The "sub_auto.csv" file are used for my ensembling process which only has the AutoML prediction results.

 ## Directory Structure
- Root/
  - Kaggle/
    - Input/
        - leash-predict-chemical-bindings/
          - test.csv
          - test.parquet
          - train.csv
          - train.parque
          - sample_submission.csv
        - **Private Dataset**/
          - auto_1.csv
          - auto_2.csv
          - auto_3.csv
        - LeashBio - Create 10M Sample Data and ecfp/
          - submission(xgb).csv
        - BELKA - Competion Submission [LGBM]
          - submission(lgbm).csv
    - Working/
        - submission.csv
  - 5-belka-submission-autogluon-frag1-2-3.ipynb

# Ensembling
I combine all these models with particular weights(1D-CNN - 0.72, XGB - 0.18, AutoML - 0.10) to build my final predictions. These weights will be further experimented for better score and the current LB score is 0.437.

# Visualization
I include a [Chemspace-visualization](https://www.kaggle.com/code/hideakiogasawara/chemspace-visualization) notebook in this repository, which illustrate that in the chemical space, molecules binding to each protein exhibited distinct patterns, which is promising. However, test molecules with non-triazine cores appeared isolated from other molecules, particularly in t-SNE. This observation may explain why they pose significant challenges.