* **Find discriminatory features**
* Features that are non-randomly distributed over target variable
* Different score to measure the importance of discriminatory features:

### Gini Impurity Index
* **Measuring the diversity of a dataset**
* Measures also the imbalance existing in the class distribution
We need firs to estimate the conditional probability: $P(c_{j}\,|\,f)$
and ensure that: $\sum_{j}^{J}P(c_{j}\,|\,f) = 1$.
The Gini index is as follows:$$G(f) = 1 - \sum_{j=1}^{J}P(c_{j}\,|\,f)^2$$
* The Goal is to have features that lower the Gini index.

### PMI as a filter Method
* **Measure the correlation between presence of features and class labels**
* Large values of PMI are the best.
* PMI average formula:$$ PMI_{avg}(f) = \sum_{j=1}^{J}\frac{\#c_{j}}{M}\log{\frac{P(c_{j}|f)}{P(c_{j})}} $$
* PMI max formula:$$ PMI_{max}(f) = max_{j}\log{\frac{P(c_{j}|f)}{P(c_{j})}} $$
### Mutual Information and Information Gain
* **They both result in the same order as conditional entropy**
* Mutual information:$$MI(f) = \sum_{j=1}^{J}\left( P(c_{j} \land f) \log{\frac{P(c_{j}|f)}{P(c_{j})}}  + P(c_{j} \land \bar{f}) \log{\frac{P(c_{j}|\bar{f})}{P(c_{j})}}\right)$$
* Where $P(c_{j} \land \bar{f})$ is the probability of class $j$ and not feature $f$.
* Information gain: $$ IG(f) = - \sum_{j=1}^{J} \frac{\#c_{j}}{M}\log{\frac{\# c_{j}}{M}} - E(f) $$
* The 0 refers to statistical independence between feature $f$ and class $c_{j}$.

### The Chi-squared statistic
* **Measures the difference between expected and observed frequencies under the assumption of independence**.
* Possible to use for discretized features.
* We obtain the $\chi^2$ statistic and compate in contigency tables (significance with p-value):$$ \chi^2(f) = \sum_{i=1}^{I}\sum_{j=1}^{J}\frac{(o_{ij} - e_{ij})^2}{e_{ij}} $$
* Where: $$o_{ij} = \# f_{i} \land c_{j}, \quad e_{ij}= \frac{\#f_{i}\#c_{j}}{M}$$
