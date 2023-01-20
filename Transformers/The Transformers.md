**A special case of Encode-Decoder Architectures using Attention mechanism**

## Architecture
* The Encoder part is a stack of 6 encoders.
* The Decoder component is also a stack of 6 encoders
![image](images/trans.png)

The Encoder and Decoder block are constituted of a self-attention layer and a Feed Forward layer:
![image](images/ffd.png)
## How the Encoder Works
* The input for the Encoder are the embeddings of the list of words. Embeddings as a 512 dimension vectro.
* Each of the 512-vector words flows first into the self-Attention layer that catches dependencies between words (context analysis), and then generates other vectors to the Feed Forward layer.
* The vectors flow independently through the Encoder. 
![image](images/flow.png)
### The Self Attention Layer
The self attention mechanism extracts the context for each word, focusing on how to extrac clues from the surroundings of the word.
1. **The first Step**:
	* We create three vectors out of the Embeddings: **Query**, **Key**, **Value** vectors of 64 dimesion. 
	* We create them multiplying the embeddings by trained Matrices: $W^{Q}, W^{K}, W^{V}$
2. **The second Step**:
	* Calculate the score. The score determines how much focus to place on other parts of the input sentence as we encode a word at a certain position.
	* We calculate the dot product of $q_{1} \cdot k_{1}$, $q_{1} \cdot k_{2}$, $q_{1} \cdot k_{3}$,...., $q_{1} \cdot k_{m}$ 
![image](images/ku.png)
3. **The third Step**:
	* Divide all scores by 8, the root square of 64. Keeps the gradients stable.
	* Calculate the softmax of each score.
4. **The fourth Step**:
	* Multiply each softmax score by the value vector. So that softmax score that are very low are insignificant.
	* Sum up all value vectors for the current and output the self-attention vector of the current word.
![image](images/soft.png)
## The Concept of Multiheaded Attention: MHA
* Instead of using only one self-attention layer, we use 8 heads of attention layers on each word.
* Advantages:
	* It expands the model’s ability to focus on different positions.
	* It gives the attention layer multiple “representation subspaces”.
* We have a set of 8 different $W^{Q}, W^{K}, W^{V}$ trained with different values.
* We do the same 4 steps of a self-attention layer on the different words. 
* We end up having 8 Z that we need to compress to pass to the FF layer.
* We concatenate up all Z matrices and multiply by $W^{O}$ matrix to get a Z vector for each word. 
![image](images/concats.png)
Finally this the final picture for the MHA:
![image](images/final.png)
## Positional Enconding
* Add a transformation on the vector Embeddings
* A transformation that takes care of the order in the sequence of words
* The intuition here is that adding these values to the embeddings provides meaningful distances between the embedding vectors once they’re projected into Q/K/V vectors.
![image](images/positional.png)
### Normalizations and Residuals
* skip/residual connection
* Allow direct information flow
* Layer normalization across the features
![image](images/norma.png)
## Decoder Layer
* decoder is very similar to encoder layer
* masked MHA at the bottom
* Each word from the top most encoder is fed to the bottom decoder and it flows all up through the decoder till getting the final Output
### Output Layer
* Two layers of:
	* Linear Layer Feed Forward
	* Softmax
1. **Linear Layer**
	* fully connected NN (up-projection)
	* vocabulary size
	* results in logits
2. Softmax Layer
	* transforms logits to pseudo-probabilities
	* then, arg max a typical prediction
![image](images/archi.png)






