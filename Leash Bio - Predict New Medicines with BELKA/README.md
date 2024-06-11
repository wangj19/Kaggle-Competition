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

# Directory Structure
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
  - Working Jupyter.ipynb

# Model
