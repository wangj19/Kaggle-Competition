# Competition
## Overview
We plan to continue in the spirit of previous playgrounds, providing interesting an approachable datasets for our community to practice their machine learning skills, and anticipate a competition each month.

**Your Goal**: The goal of this competition is to predict academic risk of students in higher education.

## Dataset
The dataset for this competition (both train and test) was generated from a deep learning model trained on the Predict Students' Dropout and Academic Success dataset. Feature distributions are close to, but not exactly the same, as the original. Feel free to use the original dataset as part of this competition, both to explore differences as well as to see whether incorporating the original in training improves model performance. Please refer to the original dataset for feature feature explanations.

The target is categorical variable about students' graduate status with three unique values: Graduate, Dropout, Other. There are 36 features about students' conditions: Marital status, Application mode, Application order, Course, Daytime/evening attendance, Previous qualification, Previous qualification (grade), Nacionality, Mother's qualification, Father's qualification, Mother's occupation, Father's occupation, Admission grade, Displaced, Educational special needs, Debtor, Gender, Scholarship holder, Age at enrollment, International, Curricular units 1st sem (enrolled), Curricular units 1st sem (evaluations), Curricular units 1st sem (approved), Curricular units 1st sem (grade), Curricular units 1st sem (without evaluations), Curricular units 2nd sem (credited), Curricular units 2nd sem (enrolled), Curricular units 2nd sem (evaluations), Curricular units 2nd sem (approved), Curricular units 2nd sem (grade), Curricular units 2nd sem (without evaluations), Unemployment rate, Inflation rate, GDP.



# Model
I applied three models and made 10 folds for each. There are avarage score of 10 fold for each model below.

**Random Forest**: 0.826799

**HistGradientBoosting model**: 0.833634

**XGBClassifier**: 0.834104

I also employed RF feature importance method in ***Data Process*** session, and if we only selected the top 15 important features, the score won't be affected to much.

**Random Forest of top 15 features**: 0.820343

**HistGradientBoosting model of top 15 features**: 0.826890

**XGBClassifier of top 15 features**: 0.826524
