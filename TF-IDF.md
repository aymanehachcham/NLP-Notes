## What is it?
* It's a measure of how relevant a term is in a document.
* It weights the importance of the term in the document.
* Helps to determine which terms carry real meaning for each document.
* TF-IDF -> Term Frequency x Inverse Document Frequency
* How to calculate:
	* ltc standard: $idf = log(\frac{N}{df_{t}})$

## Why is it useful?
* It helps to shape the document vector.
* It's a feature engineering technique that helps to determine which words carry meaning.
* Used in [[Information Retrieval]] and [[Ranked Retrieval]] in order to map words to vector space

### Methodology
* Calcualte the DTM [[Document Term Matrix]] Matrix.
* Calculate the IDF:
	* $idf = log(\frac{N}{df_{t}})$ -> vector of all the words in the vocab.
* Create the TFIDF matrix 
	* Multiply each document vector $V(\vec{d})$ with the $idf_{t,d}$ vector element-wise.
	* Normalize the document vector $||V(\vec{d})||$.
* Output: Sparse Matrix TFIDF: $TF-IDF_{docs, vocab}$

### Example
```
def idf(dtm): # Shape: vocab*1
    """ Compute the "t" step inverse document frequency """
    idf_matrix = np.log(dtm.shape[0] / (dtm.getnnz(0) + 1))
    return idf_matrix

def tfidf(dtm):
    """Finish the computation of standard TF-IDF with the c step"""
    _tf, _idf = tf(dtm), idf(dtm) # Must use above functions.
    # YOUR CODE HERE
    
    tf_idf = np.zeros(_tf.shape)
    for row_index in range(0,_tf.shape[0]):
        for col_index in range(0,_tf.shape[1]):
            tf_idf[row_index, col_index] = _tf[row_index, col_index] * _idf[row_index]
    
    tf_idf = scipy.sparse.csr_matrix(tf_idf)
    _norm = 1 / scipy.sparse.linalg.norm(tf_idf, ord=2, axis=1)
    
    for row_index in range(0,_tf.shape[0]):
        tf_idf[row_index] = tf_idf[row_index] * _norm[row_index]
    
    
    return tf_idf
```

![image](images/tf-idf.png)


## Score a document on a query
* Each vector document ca be scored using the **overlap score measure**. The idea is to score a document $d$ against a query $q$. The general formula defines as follow: $$Score(Q, d) = \sum_{t \in Q} tf-idf_{t,d}$$
* A query can be a set of keywords in the vocab `{'elena', 'rose', 'hability'}` and the goal is to sum all $tf-idf_{t,d}$ components from $d$ to evaluate the score. 
* This is called Ranked Retrieval.

## Document Similarity
* Computing the cosine angle between two document vectors can help us know if the documents are similar. The bigger the cosine the more similar they are. 
* The cosine angle is calculated as the dot product between two vectors. if we take $V(\vec{d_{1}})$ and $V(\vec{d_{2}})$ and compute the dot product $V(\vec{d_{1}}) \cdot V(\vec{d_{1}})$ we obtain the cosine of the angle between both: $cos(\theta) = V(\vec{d_{1}}) \cdot V(\vec{d_{1}})$. 
* Therefore, we can compute the cosine similarity between two $tf-idf$ as following: $$sim(d_{1}, d_{2}) = \sum_{t} tf-idf_{t, d_{1}} \,\, \cdot \,\, tf-idf_{t, d_{2}}$$
## Compute the top-k documents
* In a collection of documents we can compute the top-k document score for a given query. 
* Given a query with a set of key-words: `q = {'elena', 'zab', 'hamid'}`, we evaluate the score measure $Score(q, d)$ on all documents $d_{1}, ..., d_{n}$ and we pick the $k$ documents with the highest scores. 