There is no extrinisc evaluation possible on language models because it's time consuming.
We use instead intrinsic evaluation methods like the following:

## Perplexity
* **How well can our language model predict the next word**
* If a model assigns a high probability to the test set, it means that it is not surprised to see it: it’s not **perplexed** by it

#### Formula
* The perplexity is calculated as the probability of the test set normalized by the number of words.$$ PP(w_{1}, w_{2},...,w_{n}) = \sqrt[N]{\prod_{i=1}^{n} \frac{1}{P(w_{1}|w_{2}, w_{3},...,w_{n})}}$$
* 
* For **Bi-gram** models, the $PP(W)$ will look like this:$$PP(w_{1}, w_{2},...,w_{n}) = \sqrt[N]{\prod_{i=1}^{n} \frac{1}{P(w_{i}|w_{i-1})}}$$
* For **Tri-gram** models, the $PP(W)$ will look like this:$$PP(w_{1}, w_{2},...,w_{n}) = \sqrt[N]{\prod_{i=1}^{n} \frac{1}{P(w_{i}|w_{i-1}, w_{i-2})}}$$
**Lower $PP(W)$ perplexity is better**.

## PMI: Pointwise Mutual Information
* **A way to measure the collocation of two words.**
* The ratio / difference between the probability that the two words occur separtely versus the two words occuring jointly:$$PMI = log_{2}\left( \frac{P(w_{1}|w_{2})}{P(w_{1})\cdot P(w_{2})}\right)$$
### NPMI: Normalized PMI
* The normalized PMI gives a real sens of co-occurences. 
* It's the normalized version of PMI taking values from -1 to 1 $NPMI \in [-1, 1]$.
	* **-1**: The words never co-occur together
	* **1**: The words are very likely to occur together. $$NPMI = \frac{PMI(w_{1}, w_{2})}{-log_{2}(P(w_{1}, w_{2}))} \in [-1, 1]$$
	* **NPMI can identify n-grams statisitically**.