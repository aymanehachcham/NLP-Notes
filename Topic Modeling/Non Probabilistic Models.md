## Latent Semantic Analysis
* Unsupervised Machine learning technique to find *latent* (hidden) features in the textual corpus or collection of documents. 
* The idea is to find hidden factors or concepts, topics in our case, that can represent the documents in lower dimension. Since the documents $d_{i} \in R^V$ have a dimension $V$ (the set of words in the vocabulary), we need to reduce the dimension to $k << V$ finding latent features that explain the document without using all the words in $V$.
* These latent features are the actual topics $\{\theta_{1},...,\theta_{k}\}$ that contain multiple words.
* **Latent Semantic Analysis** is dimensionality reduction technique like **PCA**.

### How to implement
* We implement **LSA** using Singular Value Decomposition, **SVD**. 
* Having a document-term matrix $A$ of shape (n x m), we can decompose it in the following way: $$A = U \cdot \Sigma \cdot V^T$$
* Where $U$: is an orthogonal matrix of shape (n x k) the document-topic matrix
	* Each column of $U$ has Euclidean length 1 -> $\sqrt{u_{i}^2, ..., u_{n}^2} = 1$
* $\Sigma$: is the Diagonal matrix of shape (k x k) with singular **positive** values sorted in decrease order: $\sigma_{1} >= \sigma_{2} >= \sigma_{3},...$ The singular values represent the Topic Importance.
* $V^T$:  is an orthogonal matrix of shape (k x m)
	*  Each column of $V^T$ has Euclidean length 1 -> $\sqrt{u_{i}^2, ..., u_{n}^2} = 1$
	* The dot product of $U \cdot V^T = 0$, because they are orthogonal. 

![image](pics/svd.png)
### Interpretation
* $U$: Represents the distribution of the documents $d_{i}$ across the topics $\{\theta_{1},...,\theta_{k}\}$
* $\Sigma$: Represents the importance of each topic, the strength. Last singular values $\sigma_{k-2}, \sigma_{k-1}$ will have lower importance and ca be considered as noise. 
* $V^T$: Represents the distribution of terms $w_{1},...,w_{m}$ across the topics $\{\theta_{1},...,\theta_{k}\}$. 

### Example
```
def lsi(tfidf, k):
    """Latent Semantic Indexing. Return the factors, document assignment, and factor weights"""
    from sklearn.decomposition import TruncatedSVD

    # We use TruncatedSVD to return the U, Sigma and V_t matrices
    # The assignment: => document-topic matrix shape (num_docs, k)
    # The factors: => topics-words matrix shape (k, num_words)
    # The weights: => The wights for each topic, shape (1, k)
    lsi_object = TruncatedSVD(n_components=k, n_iter=100, random_state=42)

    assignment = lsi_object.fit_transform(tfidf)
    factors = lsi_object.components_
    weights = lsi_object.singular_values_

    return factors, assignment, weights

```

**Result**
![image](pics/res.png)
