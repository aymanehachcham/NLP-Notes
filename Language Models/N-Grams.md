# What is it?
* A probabilistic language model. 
* The goal is to compute the highest probability for a sequence of words. 
	* **Joint Probability**:$$P(w_{1},w_{2},...,w_{n})$$
	* **Conditional Probability** based on one word:$$P(w_{1}|w_{2},...,w_{n})$$
* The way to calculate the conditioned or joint probability is by using the **Chain Rule**:$$P(w_{1}|w_{2},...,w_{n}) = P(w_{1}) \cdot P(w_{2}|w_{1}) \cdot P(w_{3}|w_{1}, w_{2})\cdot \cdot \cdot P(w_{n}|w_{1}, w_{2},...,w_{n-1})$$ $$P(w_{1}|w_{2},...,w_{n}) = \prod_{i=1}^{n} P(w_{i}|w_{1}, w_{2},...,w_{i-1})$$
### Markov Chains 
* It is often too complicated to calculate the whole chain rule probabilities of all sequences in a text. Therefore, we use the simplifying assumption of **Markov Chains** that calculates the probability of a word based on small previous sequences:$$ P(w_{1}|w_{2},...,w_{n}) = \prod_{i=1}^{k} P(w_{i}|w_{i-1}, w_{i-2},...,w_{i-k})  $$
### N-grams
* Are language models based on the assumption of Markov chains. They calculate the probability of the next word given a sequence of 2, 3, 4, 5, etc words.
#### Bi-grams: Sequence of 2 
$$P(w_{1}|w_{2},...,w_{n}) = \prod_{i} P(w_{i}|w_{i-1})$$
#### Tri-grams: Sequence of 3
$$P(w_{1}|w_{2},...,w_{n}) = \prod_{i} P(w_{i}|w_{i-1}, w_{i-2})$$
**Examples**
* Bi-gram model: ` outside, new, car, parking, lot, of, the 
* Tri-gram model: `outside, there, is, new, car, in, lot, of `

