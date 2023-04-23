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

Support vector machine take advatnage of Covers Theorem, which state if data is projected to infinity, the data can be perfectly serparated by a hyperplane. Therefore, if data is projected onto higher dimension than the data can be separated with little errors. An example of SVM is shown in the figure below.
<p align="center">
  <img src="https://github.com/hhuynh000/EE399_HW3/blob/main/resources/Screenshot%202023-04-21%20at%201.15.45%20PM.png" width="500"/>
</p>
<p align="center">
  Figure 1. SVM Example
</p>

Decision tree goes through all feature space axis and find the best axis to split the data, repeat till all resulting splits contain only one class. An example of a decision tree is shown below.
<p align="center">
  <img src="https://github.com/hhuynh000/EE399_HW3/blob/main/resources/sphx_glr_plot_iris_dtc_002.png" width="500"/>
</p>
<p align="center">
  Figure 2. Decision Tree Example
</p>

## Implementation
The Scikit-learn package is used to implement all the classification models: LDA, SVM and Decision Tree. In order to evaluate the accuracy the Scikit-learn
accuracy score metric is used. The code used to split the data to only two specific digits and three specific digits is shown the figure below.
<p align="center">
  <img src="https://github.com/hhuynh000/EE399_HW3/blob/main/resources/Code.png" width="600"/>
</p>
<p align="center">
  Figure 3. Digits Split Code
</p>

## Results
Performing SVD on the data matrix X where each columns is one image from the Mninist dataset. Based resutling singular values the top 200 ranks capture most of the data variance and are enough to get a good image reconstruction. The resulting singular values spectrum and the reconstructed images using the top 200 ranks are shown in the figure below.
<p align="center">
  <img src="https://github.com/hhuynh000/EE399_HW3/blob/main/resources/svs.png" width="500"/>
</p>
<p align="center">
  Figure 4. Singular Value Spectrum
</p>

<p align="center">
  <img src="https://github.com/hhuynh000/EE399_HW3/blob/main/resources/recon.png" width="500"/>
</p>
<p align="center">
  Figure 5. Reconstruction with Top 200 Ranks
</p>

Given that input data matrix X has each images as columns the resulting matrix U after SVD is a 784x784 matrix, where its columns contain the principal components of the original data matrix. The top six principal components capture the features of the digits and are shown in the figure below.

<p align="center">
  <img src="https://github.com/hhuynh000/EE399_HW3/blob/main/resources/pc.png" width="500"/>
</p>
<p align="center">
  Figure 6. Top 6 Principal Components
</p>

The 784x784 diagonal matrix $/Sigma$ contains the singular value corresponding to the principal components ordered in descending value. The singular value can be seen in Figure 4 above. The 784x70000 matrix $V^{T}$ in combination with $/Sigma$ represent the original projected onto the principal components U:
<p align="center">
  $$X^{T} = (U\Sigma V^{T})^{T}$$
</p>
<p align="center">
  $$X^{T} = V\Sigma U^{T}$$
</p>
<p align="center">
  $$X^{T}U = V\Sigma$$
</p>

When the data is projected on the three V-modes 2,3 and 5 the different digits can be seen to form different clusters when 3D plotted. The 3D plot with different digits colored is shown in the figure below.

<p align="center">
  <img src="https://github.com/hhuynh000/EE399_HW3/blob/main/resources/3D.png" width="500"/>
</p>
<p align="center">
  Figure 7. V-Mode Projection 3D Plot
</p>
