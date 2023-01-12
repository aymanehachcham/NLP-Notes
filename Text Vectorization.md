## What is it?
* The process of transforming a document $d$ into a multidimensional vector with $m$ components. The document vector $d \in \mathbb{R}^m$ contains $m$ dimensions that correspond to the size of the Vocabulary $m$.
* Each component of the vector $V(\vec{d})$ is the weight associated to the frequency of each term in the document $d$.  Therefore, each component of the vector could be the $tf_{t,d}$  or the $tf-idf_{t,d}$.
* Three main components:
	* $tf_{t, d}$: Frequency of the word ($t$) in document ($d$).
	* $df_{t}$: Sum of all occurences of the word ($t$) in all documents.$$ \sum_{d=1}^{D} tf_{t, d} > 0 $$
### Example
* We take the following sentence as a document: `Elena went to College this afternoon, Elena saw the doctor`.
* We tokenize the document removing stop words and use the Bag of Words model [[Bag of Words]].
	* `BoW = {'Elena':2, 'went':1, 'College':1, 'saw':1, 'doctor':1}`
* We now have the vocabulary = `['Elena', 'went', 'College', 'saw', 'doctor']` with size $m = 5$. For document $d_{1}$ the vector representation would take in consideration first the $tf_{t,d}$, like that : $d_{1} = (2, 1, 1, 1, 1)$.
* Then the normalized version of the vector $d_{1}$: $$||d_{1}|| = \left(\frac{2}{\sqrt{2^2 + 1+1+1+1}}, \frac{1}{\sqrt{2^2 + 1+1+1+1}},...,\frac{1}{\sqrt{2^2 + 1+1+1+1}}\right)$$
$$||d_{1}|| = (0.707, 0.353, 0.353, 0.353, 0.353)$$
* We could also use $tf-idf_{t,d}$ , by calculating the $idf_{t,d}$ and multiplying by the above vector: $$idf_{t,d} = log(\frac{N}{tf_{t}}) = (0.15, 0.452, 0.452, 0.452, 0.452)$$
* We multiply $idf_{t,d} \cdot tf_{t,d}$ and we have our final vector : $$d_{1_{tf-idf}} = (0.106, 0.159, 0.159, 0.159, 0.159)$$