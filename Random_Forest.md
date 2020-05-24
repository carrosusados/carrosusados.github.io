## Random Forest to Preditc Handwritten Digits

<p style="font-size:13px">Click <a href="https://github.com/andjimbon/Predicting-Handwritten_Digits-with-Random-Forest/blob/master/Predicting_Digits_with_Random_Forest.ipynb">Here</a> to see Code</p>

**Project Description:** The goal of this project is to predict handwritten digits using a Random Forest Classification Problem.

#### Decision Trees

They are structures that allows us to arrive at a certain decision by traversing through these nodes which are based on the responses garnered from to the parameters related to the nodes.

Generally, decision trees suffer from a problem of overfitting, otherwise speaking, to get a conclusion it is necessary add more and more nodes making it more complex. To fix this problem, Random Forest Approach uses an ensamble method, simply put, is made up of numerous decision trees. These decision trees are randomly constructed by selecting random features from the given dataset.

#### Load Data

we will use a Sci-kit Learn dataset that contains handwritten digits images in form of numeric values.  

<img src="images/digits1.png?raw=true"/>

Converting this images in 8x8 pixels we get the following plot for number zero:

<img src="images/digit.png?raw=true"/>

#### Model

For this project, we will use 360 handwritten numbers for testing and use 20 estimators (trees)

**Accuracy**

Once we train the model, we get a score of **~ 0.975**. Not bad.


#### Confusion Matrix

A confusion matrix is a table that used to describe the performance of a classification model on a set of test data for which the true values are known. It allows the visualization of the performance of an algorithm.
 
Plot the Matrix.

<img src="images/c_matrix.png?raw=true"/>

 
If we take the number three as an example, the model predicted correctly 42/44 observations. Only two observations were classified as 3 when actually they were a 9.


