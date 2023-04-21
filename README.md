# Classical Machine Learning Classification Methods
### Huy Huynh

## Abstract
This page explores the classification of hand written digits from the Mnist dataset using methods like linear discriminant analysis (LDA), support vector machine (SVM) and Decision Tree. Based on the results compare the advatanges and disadvantages of each classification methods.

## Introduction
To start off, use SVD to reduce the dimensionality of the data and create a feature space of the dataset to use as inputs for the classification model. Then train and test LDA, SVM and Decision Tree on the classification of all ten digits. Diving deeper into which digit is giving the classifier a hard time to separate, train a LDA model as a base case to separate any two/three digits. From the two digits classifier LDA model find which two digits pair is the hardest to serparate and the easiest to separate. Train and test SVM and Decision Tree to classify the two hardest and easiest to separate digits pair, then compare the results.

## Background 
Singular value decomposition extract the principal components and reduce the dimensionality of the original data matrix X:
<p align="center">
 $X = U \Sigma V^{T}$
</p>

Linear discriminate analysis project the data onto principal components that maximizes the variance between classes and minimizes the variance within classes. If there are C distinct classes, m is the mean of all data points and $m_{i}$ is the mean of a class, then $S_{w} gives the scatter within class and $S_{b}$ gives the scatter between class:
<p align="center">
 $$S_{k} = \sum_{x(n)\in C_{i}}(x(n)-m_{i})(x(n)-m_{i})^{T}$$
</p>

<p align="center">
 $$S_{w} = \sum_{k=1}^{C} S_{k}$$
</p>

<p align="center">
 $$S_{b} = \sum_{i=1}^{C}N_{i}(m_{i}-m)(m_{i}-m)^{T}$$
</p>

Then the principal components that maximize and minimize variance between classes and the variance within classes respectively is given by:
<p align="center">
 $$W = eig(S_{w}^{-1}S_{b})$$
</p>

On the projected data to classify data point use the linear score function, where $m_{k}$ is class means for k class and $\Sigma$ is determinant of covariance matrix:
<p align="center">
 $$\delta_{k}(x) = x^{T}\Sigma^{-1}m_{k} - \frac{1}{2}m_{k}^{T}\Sigma^{-1}m^{k}+logpi_{k}$$
</p>

Support vector machine take advatnage of Covers Theorem, which state if data is projected to infinity, the data can be perfectly serparated by a hyperplane. Therefore, if data is projected onto higher dimension than the data can be separated with little errors.

Decision tree is 
