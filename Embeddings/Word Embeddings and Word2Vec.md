## Word Embeddings
* **Represent the word in a dense vector, while making sure that similar words are close in the embedding space**
* Finding a dense vector representation for a word 
* Vector size lower than vocabulary size V
* Define the words by their context/surrounding words

## Word2Vec

### First Idea: Skip Gram
* Use a sliding window of -/+ 2 words in the surrounding.
* Build the Main and Context dataset, with main words and their -/+ surrounding words.
* Each main word will have 4 context words.

**Example**
![image](images/sample2.png)

![image](images/pos.png)

### Second Idea: Negative Sampling
* We also register main words with words that are not part of the surroundings.
* Words that do not occur in a window slide of -/+2.
* Context words have label **1**, and negative samples have label **0**
* We take k negative samples for each word

**Example**
![image](images/neg.png)

## Learn the Vectors
* We create random vectors with $\mathbb{R}^{n}$ dimension. The dense vectors for the embeddings should be of a smaller dimension that the vocabulary size.
* Typically around 16, 32 size.
* We create main and context embeddings. Vectors for main words and vectors for context words and negative samples:
	* Vector for ***abricot***: $(0.1, 0.4, 1,5)$
	* Vector for ***tablespoon***: $(0.1, 0.3, 1,5)$
	* Vector for ***of***: $(0.1, 0.2, 1,5)$
	* Vector for ***a***: $(0.1, 0.4, 5)$
	* Vector for ***jam***: $(0.1, -0.7, 1,5)$
	* ....
#### Algorithm
* For each main and context word we:
	* Initialize randomly the vectors: $V_{main}, V_{context}$
	* First: calculate the score: $\sigma(V_{main} \cdot V_{context})$
	* Second: evaluate the error: $Label - \sigma(V_{main} \cdot V_{context})$
		* Closer vectors will have low positive error
		* Further vectors will have high negative error
	* Update the Vectors:
		* positive error -> increase the likelyhood of similar words
		* negative error -> increase dissimilarity of context words

### Update Phase:
* To maximize the similarity between positive context and main words
* To minimize the similarity between negative context and main words

#### Different Approaches
+ Stochastic Gradient Descent
	* Adjust word weights to make positive more likely and negative less likely
* As matrix Factorization
* As a Neural Network:

#### Skip-Gram and CBOW
* They are one hidden-layer Neural Network
* Idea: Predict central word from the context
* **CBOW**: Context words -> predict main word
* **Skip Gram**: main word -> predict context words
![image](images/cbow.png)
* CBOW trains faster and is slightly better than Skip-Gram.

[[GloVe and Fast Text]]

### Biases
* Increases sexism and it's sometimes unfair
* It also amplifies gender biasis

