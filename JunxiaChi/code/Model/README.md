feature.py:
Some information about the features.
feature: Feature name and class.
details: The detailed name and details and class of the feature.
cols_data:  Feature name.
all_model_10：The cross corresponding accuracy, recall, F1 and precision of each model
all_model_parm: Optimal parameters of all models.

Model.py:
import feature
Model cross validation selects the optimal parameters and carries out the classification prediction of the model

The accuracy, recall, accuracy and F1 value of the model were calculated

ROC-AUC further evaluates the model and draws Figure 12

ModlePre.py:
Import feature.py The purpose is to import the first line of the feature, which is the feature name

Reading Feature and model/ OptMfe.txt file

Reading Feature and model/ Optsample_ seq.fasta

Function: feature extraction and onehot coding

Write Feature and model/ All sample after processing_ 0314. CSV file

plot.py:
from feature import all_model_parm
Comparing the classification effect of the three models, the accuracy, recall, accuracy and F1 value of the selected optimal parameters are plotted respectively, and Figure 11 is drawn.