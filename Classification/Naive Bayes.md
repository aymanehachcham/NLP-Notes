## What is it?
* The most simple mode for text classification. 
* It's a navie bayes classifier. 
* More enhanced classifiers used the same core methodology as Naive Bayes.
* It uses Bag of words

### Steps for the Naive Bayes
* **Bag of Words** decomposition for each document. And use the resulting term frequency: $tf_{w, d}$.
![image](images/bow.png)
* **Use the Maximum apriori Naive Bayes**: $$c_{m} = argmax_{c \in C} P(c\,|\,tf_{m}) = argmax_{c \in C} P(tf_{m}\,|\,c)\cdot P(c)$$
* This is possible using Bayes Theorem. Therefore, to calcualte the prediction $c_{m}^{NB}$: $$ c_{m}^{NB} = argmax_{c \in C} P(c) \, \prod_{w \in W} P(w \,|\,c) $$
### Simplification on the Naive Bayes
* Add independence of prorbabilities for each class.
* Bag of Words: the order does not matter
* Use sum of logs instead of product of probabilities:$$ c_{m}^{NB} = argmax_{c \in C}\left( \log{P(c)} + \sum_{w \in W} \log{P(w\,|\, c)} \right) $$
### Estimation Problems
* What happens if there are values 0 for $tf_{w}$. Then, the probability would be zero. 
* We need to use **Laplace Smoothing** to prevent that: $$ P(w|c) = \frac{tf_{w|c} +1}{V + \sum_{w \in W} tf_{w|c}}$$
### Problems and practical implications
* unknown words (from training set) are discarded (from test set)
* stopwords are usually considered as features
* aim: dimension reduction while preserving information
