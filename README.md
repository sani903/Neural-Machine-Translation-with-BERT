# Neural-Machine-Translation-with-BERT
Modified re-implementation of paper published in ICLR 2020 used to translate English to Dutch
<br>
## Pre-processing and Tokenization
1. Data from the translation dictionary is cleaned and converted to a Dataframe.
2. Text is converted to unicode, unnecessary whitespaces are removed, and each word in the dictionary is assigned an integer ID.
3. The class 'BasicTokenizer' tokenizes based on whitespace and punctuation, and lower-cases the text. It supports tokenizations for CJK characters.
4. The class 'WordpieceTokenizer' takes as input the tokens from BasicTokenizer and implements WordPiece tokenization. 
5. The class 'FullTokenizer' integrates both tokenizers and provides a full tokenization pipeline. It also includes functions to map tokens to IDs and vice versa.

## Attention
1. Positional encoding vectors are calculated and added to the embedding vector.
2. Padding mask and look-ahead mask are used.
3. Multi-head attention using scaled dot-product attention is employed in the model layers, which is followed by a feed forward neural network.

## Encoder
1. The Encoder layers are built using pre-trained BERT layers.

## Decoder
1. The Decoder layers are built using the custom architecture of masked multi-head attention and feed forward network sublayers which are connected via layer normalization.
2. Multiple Decoder layers are stacked to build the Decoder.
3. In multi-head attention(with padding mask), V (value) and K (key) receive the encoder output as inputs. Q (query) receives the output from the masked multi-head attention sublayer.

## Transformer
1. A transformer consists of the encoder, decoder, and a final linear layer. The output of the decoder is the input to the linear layer and its output is returned.
2. During training, Adam optimizer is used and custom learning rate scheduling as per the formula in 'Attention is All You Need' paper is implemented.
3. Checkpointing is also implemented during training. Teacher forcing is used in to train the model.

References:
1. https://www.tensorflow.org/text/guide/subwords_tokenizer
2. https://www.tensorflow.org/text/tutorials/transformer
