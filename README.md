# Owkin-Data-Challenge

Notebook for the data challenge proposed by Owkin: https://challengedata.ens.fr/participants/challenges/98/

The challenge proposed by Owkin is a weakly supervised binary classification problem: the aim is to predict, from a high-resolution histological slide, whether a patient has a PIK3CA gene mutation.

Feature vectors are extracted from each tile using a pre-trained resnet model.

Several architectures were compared: Random forest classifier, support vector classifier, neural network.
Considering the small size of the training set and the fact that the test set comes from a different distribution than the training set, it is important not to overfit. To achieve this, only certain features were selected. Several ways of selecting features were compared.
  - Average of the 2048 features over the 1000 tiles
  - Selection of dominant features in the PCA
  - Use of the correlation matrix to filter out the features most correlated with each other and the features least correlated with the target variable.

This last strategy, together with the use of a Random forest classifier, resulted in the best AUC.

After selecting the hyperparameters, the following parameters were chosen:
  - feature selection: corr_threshold = 0.8, target_corr_threshold = 0.1
  - Random forest classifier: n_estimators=200, max_depth=12
