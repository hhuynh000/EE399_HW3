# Classical Machine Learning Classification Methods
### Huy Huynh

## Abstract
This page explores the classification of hand written digits from the Mnist dataset using methods like linear discriminant analysis (LDA), support vector machine (SVM) and Decision Tree. Based on the results compare the advatanges and disadvantages of each classification methods.

## Introduction
To start off, use SVD to reduce the dimensionality of the data and create a feature space of the dataset to use as inputs for the classification model. Then train and test LDA, SVM and Decision Tree on the classification of all ten digits. Diving deeper into which digit is giving the classifier a hard time to separate, train a LDA model as a base case to separate any two/three digits. From the two digits classifier LDA model find which two digits pair is the hardest to serparate and the easiest to separate. Train and test SVM and Decision Tree to classify the two hardest and easiest to separate digits pair, then compare the results.

## Background 
Singular value decomposition extract the principal components and reduce the dimensionality of the original data matrix X.
<p align="center">
 $X = U \Sigma V^{T}$
</p>
