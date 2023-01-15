# What is it?
* Formal techniques used to discover and analyse underlaying topics in a collection of documents
* The main interest is to understand the contents and the general ideas discussed in those documents
* 2 main objectives:
	* **First**: Discover what topics are there. With $k$ number of topics, we need to find the relevant topics discussed$\{\theta_{1},...,\theta_{k}\}$.
	* **Second**: Discover to what extent each document $d_{i}$ (from the collection of documents $C$), covers each topic $\{\theta_{1},...,\theta_{k}\}$. The probability of each document $d_{i}$ covering a portion of all topics is defined as: $\pi_{ij}$ for $j={1,2,...,k}$.

![image](pics/topic_modeling.png)
## Formal Definition
#### Inputs
* Collection of documents: $d_{1},...,d_{n} \in C$. 
* Number of topics predefined from the data: $k$.

#### Outputs
* Set of $k$ Topics Discovered: $\{\theta_{1},...,\theta_{k}\}$.
* Coverage of topics by each document $d_{i}$:   $\pi_{ij}$, where $\sum_{j=1}^{k} \pi_{ij} \, = 1$.
* Probability of coverage $\pi_{ij}$.

## Topics as Distribution of Terms
* Topics can be naturally defined from the set of words or vocabulary extracted from the collection of documents, $w \in V$ where $V = \{w_{1},...,w_{m}\}$. 
* Three conditions should apply:
	* A topical term should have a high expressive power: It has to be meaningful and represent a set of nested words. 
	* A topical term should include related words that express the same topic.
	* A topical term has to consider the existence of ambiguous terms, terms that share meaning across different topics.

![image](pics/topical_terms.png)
* Where $P(w|\theta_{i})$ is the probability distribution of all the words in the vocabulary set $V$ in the topic $\theta_{i}$. All probabilities sum up to one: $\sum_{w \in V} P(w|\theta_{i}) = 1$.
* The words : {**play**, **star**, **travel**} are existent in several topics but with a different probability $P(w|\theta_{i})$ in each topic. Expressing the relevance in each topic.
* Words very relevant to the topic have a highest probability, example {**sports**, **game**, **basketball**, **football**} have the highest probability in the Sports topic.
* Two probability outputs:
	* $\pi_{ij}$: Probability of each document $d_{i}$ covering each of the topics $\{\theta_{1},...,\theta_{j}\}$.
	* $\theta_{j}$: Probability distribution of words inside the topic: $P(w|\theta_{i})$.


# How to create the Model: Two Approaches:
### Non Probabilistic Models
* Non probabilistic models like LSA and SVD [[Non Probabilistic Models]], using matrix decomposition

### Probabilistic Models
* The model that is capable of generating the topics $\{\theta_{1},...,\theta_{j}\}$ and the probability distributions $P(w|\theta_{i})$ is a probabilistic model [[Probabilistic Models]].
