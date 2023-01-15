# What is it?
* Describes a set of particular problems that take place when there is an important increase in the number of attributes used in a model.
* Generally, the data that we manipulate tends to behave differently from the number of dimensions we have in paper. Example with the text, most of our vectors are sparse, therefore only an intrinsic subset of the initial vector space $\mathbb{R}^{d}$ is really used.
* There is three kinds of problems related to the curse of dimensionality:

## Combinatorial Explosion
* Increasing the partitioning of a dataset into higher dimensions leads to an exponential numbers of combinations and experiments to run on the data. Specially, in the case of text data most of the data points are not used (sparse data).
* Most grid based, indexing and hypertuning algorithms will not work on huge dimensions. It's too costly in terms of efficiency and time.

![image](pics/combins.png)

## Concentration of Distances
* In higher dimensions the distances between data points tend to converge to zero. All the points become concentrated in a space subset and the distance between $D_{max}$ and $D_{min}$ is zero. 
* Also the ratio between the max distance and the min distance is also 1: $D_{max}/D_{min} \rightarrow 1$.
![image](pics/distances.png)
