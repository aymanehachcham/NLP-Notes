* RNN architectures belong to the family of sequence modeling architectures

### Example of Sequence Modeling Architectures
1. Vector to Sequence Model
![image](images/vec-toimage.png)

2. Sequence to Vector Model
![image](images/se-to-vec.png)
3. Sequence to Sequence Model
![image](images/seq-to-seq.png)
* Where the order of the words does not matter.
* The Recurrent Neural Networks have the following architecture:
Basically multiples Feed Forward NN stack together and each layer passes the information to the  next layer
![image](images/rnn.png)

* $h_{t} = tanh(W_{t}X_{t} + h_{t-1})$ -> Linear transformations with $W_{t}X_{t}$ plus the information contained in the previous hidden layer $h_{t-1}$
* $o_{t} = softmax(u_{t})$: The output layer takes the softmax of the linear calcualtion $u_{t}$.
![image](images/pic_rnn.png)

* The information passed from layer $h_{t-1}$ to $h_{t}$ is called **long term dependency**. Because the network keeps the information from the beginning.
* The Long short term memory is a drawback and advantage.

## LSTM and Improvement
* The Long short Term memory RNN is an improvement on the current RNN.
* It has forget cells that help to miss on information coming from previous layers.
* It uses skip connections :
![image](images/skip.png)
* Uses LSTM Cells, that keep track of the current cell state, they also have gates:
	* Input Gate: is the cell updated
	* Forget Gate: Is the memory set to zero
	* Output Gate: is the current cell output visible
![image](images/cell.png)



