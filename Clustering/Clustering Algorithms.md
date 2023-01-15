## Hierarchical Agglomerative Clustering
* Initially all the data points are singleton clusters
* Compute the distance or similarity matrix
	* Distance matrix -> min(a, b)
	* Similarity matrix -> max(a,b)
* Joint points with the minimum distance or maximum similarity
* Recompute the distance matrix based on the following linkages
	* Single Link: min_dist(a,b)
	* Complete Link: max_dist(a,b)
	* Average Link: $\frac{1}{2} \sum{dist(a, b)}$
	* Centroid Link: $||\mu_{a} - \mu_{b}||^2$ 
* Compute the Dendogram

### Examples
#### Single Link
Compute the distance matrix -> using Euclidean distance
![image](pics/distance.jpg)

First iteration -> take the min value: 0.14 $P_{2}P_{5}$
![image](pics/sing_f.jpg)

Calculate the following distances:
* $dist({P_{1}, (P_{2}P_{5})}) \,\, \rightarrow \,\, min((P_{1}, P_{2}), (P_{1}, P_{5})) = 0.23$
* $dist({P_{3}, (P_{2}P_{5})}) \,\, \rightarrow \,\, min((P_{3}, P_{2}), (P_{3}, P_{5})) = 0.15$
* $dist({P_{4}, (P_{2}P_{5})}) \,\, \rightarrow \,\, min((P_{4}, P_{2}), (P_{4}, P_{5})) = 0.20$
* Take the min value of the distance matrix $0.15$
![image](pics/sing.jpg)
Second iteration
Since $dist({P_{3}, (P_{2}P_{5})}) \,\, \rightarrow \,\, min((P_{3}, P_{2}), (P_{3}, P_{5})) = 0.15$ is the smallest value, we group a new cluster: $P_{3}P_{2}P_{5}$ and we calculate the following distances:
* $dist({P_{1}, (P_{3}P_{2}P_{5})}) \,\, \rightarrow \,\, min((P_{1}, (P_{2}P_{5})), (P_{1}, P_{3})) = 0.22$
* $dist({P_{4}, (P_{3}P_{2}P_{5})}) \,\, \rightarrow \,\, min((P_{4}, (P_{2}P_{5})), (P_{4}, P_{3})) = 0.15$
We pick the min again, and it is 0.15
 ![image](pics/pre-final.jpg)
Final iteration, we assemble the big cluster
Thi big cluster is: $((((P_{2}P_{5})P_{3})P_{4})P_{1})$
![image](pics/final_s.jpg)

## Agglomerative Nesting: AGNES
* Uses Lance_Williams formulas
![image](pics/lance.png)
* The same as above but using the following formulas instead:
	* Single Link: -> $\alpha_{1}dist(A,C)+\alpha_{2}dist(B,C)+\beta dist(A,B) +\gamma |dist(A,C) - dist(B,C)|$

#### Complexity of Hierarchical Clustering
* Total $O(n^3)$ in time and $O(n^2)$ in memory

#### Benefits and Limitations
* Very general, any distance can work with it
* Gives a hierarchical resutl and easy to interpret
* Gives a dendogram for visualization

* Scalability is the main issue
* Unbalanced cluster sizes

## K-means and Shperical K-meas
* The objective is to divide the set of all data points into $K$ subsets.
![image](pics/cluster.png)
* Each cluster $k$, defined as $w_{k}$ groups together all documents that are similar and that are close to the cluster centroid $\mu_{k}$.
* The centroid $\mu_{k}$ is defined as the mean vector of the documents inside the same cluster: $$\mu_{k} = \frac{1}{|w_{k}|}\sum_{\vec{x} \in w_{k}} \vec{x}$$
* K-means minimizes the **RSS**, which is the residual sum of squares between all document and their cluster centroid: $$RSS_{k} = \sum_{\vec{x} \in w_{k}}(\vec{x} - \mu_{k})^2$$
* If we detail the **RSS** for each document in the cluster $\vec{x} \in w_{k}$ component by component (over the vectors's dimension) $m=1,...,M$, and then we sum over all clusters $k=1,...,K$ we have the following: $$RSS = \sum_{k=1}^{K}\left(\,\, \sum_{\vec{x} \in w_{k}}\,\,\sum_{m=1}^{M} (x_{m} - \mu_{k,m})^2)\right) = \sum_{k=1}^{K} RSS_{k} $$
#### Algorithm
* **Step 1**: Select $K$ random cluster centers: $\mu_{1},...,\mu_{k}$ from the set of data points.
* **Step 2**: Calculate the RSS between all points $\vec{x_{1}},...,\vec{x_{n}}$ and the cluster centers $\mu_{1},...,\mu_{k}$.
* **Step 3**: Assign each point $\vec{x_{n}}$ to the closest cluster $\mu_{k}$ based on the RSS.
* **Step 4**: Recompute the cluster center $\mu_{k}$ based on the new assignment: $\mu_{k}' = \frac{1}{|w_{k}'|}\sum \vec{x}$
* **Step 5**: Repeat **step3** and **step4** till stop criterion attained.

##### Important Note
K-means converges because for each iteration the **RSS** decreases monotonically, basically for two reasons:
* **Assignment Step**: Assigning the points $\vec{x_{n}}$ to the cluster center with the lowest **RSS**.
* **Recopmutation Step**: Compute the new cluster center $\mu_{k}'$ based on the new assignment.

The computation of the cluster center $\mu_{k}$ contributes to minimize the **RSS**: $$RSS_{k} = \sum_{\vec{x} \in w_{k}}(\vec{x} - \mu_{k})^2$$
$$\frac{\partial RSS_{k}}{\partial \mu_{k}} = 0 \rightarrow \frac{1}{|w_{k}|} \sum_{\vec{x} \in w_{k}} \vec{x}$$
#### Choice of initial Centroids
* Ideally find centroids $\mu_{k}$ from each different cluster, but the number of ways (combinations) to choose one centroid for each cluster are very hight: $\frac{k!}{k^k}$
* Generate $k$ clusters from a normal distribution
* Randomly generate $k$ clusters
* Run few k-means iterations on a small sample then use the cetroids from the sample test

#### Stop criterion choice
* Choose a number of maximum iterations $I$: Affects the quality of the clustering
* Assignment of documents does not change with new iterations: Huge runtime needed
* Centroids $\mu_{k}$ do not change with new iterations: Huge runtime needed.
* Terminate when **RSS** falls under a specific threshold $\theta$: We need to determine a small $\theta$ and also control the runtime.

#### Determine $K$: Cluster Cardinality, choice of Heuristics
* Heuristic mostly used is the *Elbow Method*:
	* Run k-means with different initializaitions and different number of $K$ clusters ($K=\{1,2,...,n\}$) and we compute the respective RSS for each $k$. When the notice a *knee* in the curve (succesive decreases in RSS become noticeably smaller) that's the optimal number of clusters $k$.
* Other Heuristics try use *AIC* or *BIC* to model the tradeoff between RSS optimality and model complexity (too much parameters -> centroids $\{\mu_{1},...,\mu_{k}\}$): $$AIC: K = argmin[-2L(K) + 2q(K)]  $$ where $2L(K)$ is the equivalent of $RSS$ and $2q(K)$ measure model complexity. AIC And BIC penalizes models with high complexity. 

#### Spherical k-means
* Used to apply clustering k-means on textual data. *Spherical* because the documents are vectors of lenght 1 (normalized) and therefore each cluster ideally should be a perfect sphere of radius 1 containing all documents that are similar.
* **Procedure**:
	* Vectorize the documents using TF-IDF, (Bag of Words) + (Create vocab) + (Stop words removal) + (DTM Matrix) +(TF-IDF).
	* Normalize the documents, each document $\vec{x_{n}}$ should have norm $||\vec{x_{n}}|| = 1$. 
	* Initalize cluster centers randomly from the set of documents: $\{\mu_{1},...,\mu_{k}\}$
	* Copmute the **assignment** step based on similarity (lookig for high similarity), using cosine similarity: $$cos(\vec{x_{1}}, \vec{x_{2}}) = \sum_{m=1}^{m}x_{1,m} \cdot x_{2,m}$$
	* Documents with high similarity are clustered together.
	* Recopmute the cluster centers $\{ \mu_{1},\mu_{2},...,\mu_{n} \}$ based on the new assignment.
	* Return the assignment when criterion is attained.

#### Example with Code:
* Needs explanation !!!

#### Complexity:
* Initialization: $O(k)$
* Assignment step: $O(N \cdot k \cdot d) \cdot i$ for each iteration $i$
* Mean computation: $O(N \cdot d) \cdot i$ for each iteration $i$
* Total: $O(N \cdot k \cdot d \cdot i)$: much better than $O(n^2)$

#### Benefits and Limitations
* Very fast algorithm
* Can be run multiple times to get different results

* Difficult the optimal K.
* Can not be used with any distances, only Euclidean and consine similarity.
* Sensitive to outliers.
* Cluster sizes can be unbalanced.

## Model-based Clustering
* K-means is a hard clustering and can not handle well clusters with different radius. 
* We can use a more general form of K-means which lead to a softer clustering. We then use a generative model like Gaussian Mixtures.

### Gaussian Mixture Model
* We assume that the data got generated from $k$ multivariate gaussians. We use the EM algorithm to refine the model parameters and maximise the likelihood of the data points under the different gaussian clusters.
* Steps from EM:
#### Initialisation
* Initialise the model parameters randomly:$$\theta = (w_{1}\mu_{1}\Sigma_{1},w_{12}\mu_{2}\Sigma_{2},...,w_{k}\mu_{k}\Sigma_{k})$$ ![image](pics/em.png)

* The probabilities are calculated as follows:

![image](pics/params.png)
### Downsides
* Gaussian mixtures can not be used with text for the following reasons:
	* text is not Gaussian distributed.
	* text is discrete and sparse, Gaussians are continuous.
	* covariance matrixes have $O(d^2)$ entries, and text has very high dimensionalities.
* EM can be used with other discrete distributions like Bernoulli.

