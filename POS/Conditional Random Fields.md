## Condition Probability VS Joint Probability
* The HMMs model the joint probability between the observables $x_{1},x_{2},...x_{n}$ and the hidden states $y_{1},y_{2},...y_{n}$ in a given sequential fashion. Therefore, the ultimate goal in HMM is to find the the joint probability $P(x_{1},x_{2},...x_{n} \,,\, y_{1},y_{2},..._{n})$.
* In the CRF the goal is to model the conditional probability: $P(x_{1},x_{2},...x_{n} \,|\, y_{1},y_{2},..._{n})$. More specifically, we want to find the probability that maximises the likelihood of the observed data: $$argmax_{y^{(1)},y^{(2)},...,y^{(t)}}\,\, P(x_{1},x_{2},...x_{n} \,|\, y_{1},y_{2},..._{n})$$
* HMMs are **generative models**, they give a framework to explain and determine how the observed data got generated at the first place give the hidden states. The CRFs are discriminative

### Limitations of the HMMs
* The probabilities of the HMM, transition and emission matrices $A, B, \pi$ are static. The probabilities are defined based on the transition from state to state, and for the observables under a current state. They are not modified according to the position on the sequence or to any other external variable.
* HMMs have limited dependencies. The arrows between states are unidirectional and according to the Markov property they are only dependent from $s_{t} \rightarrow s_{t+1}$. There is no other option. Also the observables directly depend only on the current state. Therefore the dependencies between observables and states are very limited 

![image](images/depend.png)
### From HMMs to CRF
* CRF is a more general framework to capture the dependencies from observables and hidden states. HMMs are a specific part of CRFs where the connections are restricted to Markov Chains.
* CRFs are **discriminative models**, the try to model the conditional probability of $Y=y_{1},...,y_{n}$ given the set of observables $x_{1},x_{2},...x_{n}$. Therefore CRFs rely on **Maximum Entropy Markov Models** modeling $P(y^{(*)}|x^{(*)})$.  
* CRFs with a lot of connections might cause a serious strain on the material resources, a lot of computations. Therefore, we use a lighter version called Linear Chain CRFs.

### Linear Chain CRFs
* Only connecting states that are sequential to each other. The only allowed connections between hidden states are in terms of: $y^{(t)}, y^{(t+1)}$.  But the other connections between observables and hidden states are allowed to be as wild as we want.

#### Linear Chain CRFs use Feature Functions
* Feature functions are functions used to create meaningful features from the sequential data. There are tools to encode arbitrary features that would help the model learn about relevant sequential dependencies in the model.
* Feature functions take as input: $f(X, y^{(i)}, y^{(i+1)}, i)$ the set of all observed data $x_{1},x_{2},...x_{n}$, the previous and current state $y^{(i)}, y^{(i+1)}$ and the index of the time in the sequence. Which means, that feature functions can give different results for similar patterns between $x^{(*)}, y^{(*)}$ captured in different time steps in the sequence. 
* Feature functions can be based on any mathematical logic and can output any real or binary values. In fact, embeddings can be used as feature functions in a CRF model to help learn the dependencies between observed and hidden states.

![image](images/features.png)

* Setting up the features functions into a specific way and restricting the possible connections between $x$ and $y$ yields back and HHM.

### Maximum Entropy Markov Models
* The set of all the feature functions used in our CRF model is defined by: $F(X, y^{(i)},y^{(i+1)},i )$ , that indicates the weighted sum of all our feature functions: $$F(X, y^{(i)},y^{(i+1)},i ) = \sum_{k} \lambda_{k} \,\, f_{k}(X, y^{(i)},y^{(i+1)},i )$$
* The CRF model will train on sequential data in order to determine the weights $\lambda_{k}$ associated to the feature functions $f_{k}$. Typically, using gradient descent. 
* Finally, the way to compute the conditional probability: $P(y^{(*)}|x^{(*)})$ is given by the following formula: $$P(y^{(*)}|x^{(*)}) = \frac{1}{Z(x^{(*)})} \exp{\left(\sum_{t} f_{k}(X, y^{(i)},y^{(i+1)},i ) \right)}$$
![image](images/expec.png)

#### Finding the max probability
* Once the weights $\lambda_{k}$ of our CRF model are trained we can figure out which combination of hidden states is maximum for a particular set of unseen observed data. Then, we could apply Viterbi algorithm to quickly find the max probability given all possible hidden states.