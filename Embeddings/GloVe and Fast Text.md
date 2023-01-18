## The GloVe algorithm: Global vector for Word representation

## Fast Text
A new improving algorithm for word embeddings

### Approach
* Split words into n grams
	* Example:  Love -> [Lo], [ve]
* Train embeddings for n grams and complete words
* To get the target embedding: Sum n-gram embedding and complete word embedding
	* $V_{word} = V_{n-gram} + V_{complete}$
* The Goal is to predict context words using the target embeddings with SGNS
* Also uses Hierarchical Clustering and Binary trees to speed the process of maximizing similarity between word vectors.

## Advantages
* understands suffixes and prefixes
* understands composed words
* works (often) also with unseen words
