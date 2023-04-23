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

When the data is projected on the three V-modes 2,3 and 5 the different digits can be seen to form different clusters when 3D plotted. Although, the different digits clusters are very close to each other and have a lot of overlap. The 3D plot with different digits colored is shown in the figure below.

<p align="center">
  <img src="https://github.com/hhuynh000/EE399_HW3/blob/main/resources/3D.png" width="500"/>
</p>
<p align="center">
  Figure 7. V-Mode Projection 3D Plot
</p>

Starting with Linear Discriminate Analysis as the first classification model, test classifying two digits (1,8) and three digits (1,3,8):
<p align="center">
  Two digits Classification (1,8) Testing Accuracy: 0.979 <br>
</p>

<p align="center">
  Three digits Classification (1,3,8) Testing Accuracy: 0.958
</p>

Test two digits classification on all digit pairs, the easiest pair to serparate is is 6 and 9 and the hardest pair to separate is 5 and 8:
<p align="center">
 Digits pair most difficult to separate (5, 8) <br>
 Training Accuracy: 0.968 <br>
 Testing Accuracy: 0.951
</p>

<p align="center">
 Digits pair most easy to separate (6, 9) <br>
 Training Accuracy: 0.998 <br>
 Testing Accuracy: 0.996 <br>
</p>

Repeating the easiest and hardest digit pairs to serparate classification using the SVM and Decision Tree model with original data matrix projected onto the top 200 principal components:

<p align="center">
 Digits pair most difficult to separate (5, 8) <br>
</p>

<p align="center">
  SVM Classification <br>
  Training Accuracy: 0.997 <br>
  Testing Accuracy: 0.994
</p>

<p align="center">
 Decision Tree Classification <br>
 Training Accuracy: 1.0 <br> 
 Testing Accuracy: 0.923 <br> 
</p>

<p align="center">
 Digits pair most easy to separate (6, 9) <br>
</p>

<p align="center">
 SVM Classification <br>
 Training Accuracy: 0.9997 <br>
 Testing Accuracy: 0.9990 <br>
</p>

<p align="center">
 Decision Tree Classification <br>
 Training Accuracy: 1.0 <br>
 Testing Accuracy: 0.978
</p>

Finally, test classifcation of all 10 digits using LDA, SVM and Decision Tree:
<p align="center">
 LDA Classifier <br>
 Training Accuracy: 0.8714833333333334 <br>
 Testing Accuracy: 0.873
</p>

<p align="center">
 SVM Classifier <br> 
 Training Accuracy: 0.987 <br>
 Testing Accuracy: 0.978
</p>

<p align="center">
 Decision Tree Classifier <br>
 Training Accuracy: 1.0 <br>
 Testing Accuracy: 0.837
</p>

## Conclusion
In conclusion, given a data set with high dimensionality and hard to serparate like the Mnist dataset as shown in Figure 7, linearly separating the data with model like LDA is difficult. Classification of all 10 digits using LDA only result in a testing accuracy of 87.3%. While, SVD does significantly better with a testing accuracy of 97.8% by projecting the data into higher dimension and applying Cover Theorem. Decision Tree classifier struggle with a testing accuracy of 83.7%. Although, Decision Tree classifier might be over fitting the training data with a 100% accuracy. Perhap using Random Forest can improve the accuracy and prevent over fitting. In addititon, different digits are harder to distinguish than others as shown by the two digits classification testing. Digits like 5 and 8 have similar feature in handwriting making them difficult to separate. On the contrary, digits like 6 and 9 are flipped version of each other, making them easier to serparate. 
