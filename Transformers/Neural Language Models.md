* Neural Language Models are based on Deep Neural Networks.
* The Advantage is that Hidden Layers improve performance of the general model
* Hidden Layers allow for non-linear interactions between features.
* No need for feature engineering, features are automatically detected by the Model.

## Current Approach
* Most of the techniques like CBOW or Skip-Gram use Feed Forwad neural netwoks

![image](images/ff.png)
## Example of Neural Language Model

The task is to predict the next word using a sliding window
* It uses in the output layer a Softmax to extract probabilites of next word.
![image](images/nnm.png)
### Advantages of n-gram LM
* Finds similarities between embeddings
* Handles unseen data 
* Is able to generalize and predict, able to predict dog after fed.

### How to train NNs
* We take a training pair of features and target variable: $(\vec{x}, y)$
* FF step to find the estimated target $\hat{y}$ according to current params
* Use the loss function $L(\theta, \hat{y})$  to calculate the loss
* Update the weights according to the loss
