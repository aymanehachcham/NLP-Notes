* In Clustering typically there is no labels to compare to, therefore the evaluation should be unsupervised. 
* On well known measure to assess the goodness of clustering is Silhouette:

### Silhouette Coefficient:
* Calculate two distances:
	* $d_{1}(x_{m})$: Distance of $x_{m}$ to own cluster
	* $d_{2}(x_{m})$: Distance of $x_{m}$ to closest cluster
	* And then the silhouette coefficient is:$$ silhouette(x_{m}) = \frac{d_{2}(x_{m}) - d_{1}(x_{m})}{\max{(d_{2}(x_{m}), d_{1}(x_{m}))}} \,\, \in [-1, 1] $$
### For Supervised evaluation
* We could use $F_{1}$ measure as a combination: $$ F_{1} = \frac{2 Precision \cdot Recall}{Precisio + Recall} $$
* Also $MI$ or Entropy could be used.

