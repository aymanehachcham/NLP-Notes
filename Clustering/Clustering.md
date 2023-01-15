## What is Clustering
* Unsupervised technique that groups a set of documents into clusters that are cohesive and very similar internally and highly different externally between each other.
* Documents inside the same cluster share high similarity, and documents from different clusters are highly dissimilar.
* The task is to assign to each document a cluster without knowing beforehand its label / class. From the given data performing an iterative process we're able to group documents together in a set of clusters. 

##### The data distribution -> will makeup the cluster membership.

#### Cluster Hypothesis
* Documents in the same cluster have almost the same relevancy when it comes to a query of information need. Which means, that they share a same topic.

#### Problem Statement
* The goal is to map a set of documents $D = \{ d_{1},...,d_{n}\}$ to a set of clusters $K = \{k_{1},...,k_{p}\}$ by minimizing an objective function or criterion: $$\gamma: D \rightarrow \{k_{1},...,k_{p}\}$$
* $\gamma$ should also be surjective -> that no cluster $k$ should be empty.
* The objective function $\gamma$ is defined in terms of distance or similarity between documents.
	* Distances of Objects:
		* Euclidean: $d_{Euclidean}(x,y) = \sqrt{(x_{1}-y_{1})^2+(x_{2}-y_{2})^2+...+(x_{m}-y_{m})^2}$
		* Manhattan: $d_{Manhattan}(x,y) = |x_{1}-y_{1}|+|x_{2}-y_{2}|+...+|x_{m}-y_{m}|$
		* Small values -> indicate better clustering
	* Similarity of Objects
		* Cosine Similarity: on Normalized vectors $cos(x, y) = \sum_{i=1}^{m} x_{i} \cdot y_{i}$  
		* Large values -> indicate better clustering

#### Finding the number of Clusters: Cardinality
* The problem with clustering is that we need to determine before hand the "optimal" number of clusters that minimize the objective function $\gamma$ and keeps an acceptable model complexity (number of parameters in the model).
* We can't determine the perfect number of clusters -> infeasible for $N$ documents and $K$ clusters we have $\frac{K^N}{K!}$ possible partitions.
* Usually there is no direct solution -> Often we use heuristics or domain knowledge.

## Applications of Clustering
* Customer Segmentation
* Web search optimization -> Search by category or topic
* Data reduction or Aggregation -> represent a whole set of points with one representative
* Topic modeling -> Group a set of documents into a topic

## Types of Clustering
#### Flat Clustering
* Creates a flat set of clusters -> without internal structure
* Two types of Clustering : Hard Clustering and Soft Clustering
**Hard Clustering**
	* **K-means** -> assings to each document one and only one cluster
**Soft Clustering** -> assigns multiple clusters to each document
	* **Model-based Clustering** -> EM Algorithm

##### Hierarchical Clustering
* Creates a hierarchy of clusters
	* **Hierarchical Agglomerative Clustering**
