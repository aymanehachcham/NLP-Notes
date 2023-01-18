At a very high level, an encoder-decoder model can be thought of as two blocks, the encoder and the decoder connected by a vector which we will refer to as the **context vector**
![images](lstm.png)
Usually, first:
* Layer of Embeddings to vectorize the sequence of text into vector-tokens

**Encoder**: an LSTM cell that takes the vectorized sequence at each time step. 
Then it tries to create a compact vector of information containing the hidden state $h_{t}$ and the cell state $ce_{t}$ at time $t$. The compact vector is the context vector $c_{t}$.

**Context Vector**: The vector is built in such a way that it's expected to encapsulate the whole meaning of the input-sequence and help the decoder make accurate predictions.

**Decoder**: The decoder reads the context vector and tries to predict the target-sequence token by token.
The decoder block is also an LSTM cell. The main thing to note here is that the initial states **(h₀, c₀)** of the decoder are set to the final states **(hₜ, cₜ)** of the encoder. These act as the ‘context’ vector and help the decoder produce the desired target-sequence.

## Training and testing phase

**Encoder**: The encoder part is trained normally as normal LSTM but ignoring the actual output and focusing on the context vector.

**Decoder**:The input fed to the decoder at the first time-step is a special symbol **“<START>”**. This is used to signify the start of the output-sequence. Now the decoder uses this input and the internal states **(hₜ, cₜ)** to produce the output in the 1st time-step which is supposed to be the 1st word/token in the target-sequence

Also:
Decoder uses two different non-trivial approaches:

• teacher forcing while training (cf. next slide):  
use true labels as inputs, not the predicted output sequence

• during the testing phase the predicted token are used as input for next token — as one-hot-encoded vector passed to the embedding layer

