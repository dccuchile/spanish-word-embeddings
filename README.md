# Spanish Word Embeddings

Below you find links to Spanish word embeddings computed with different methods. Whenever it is possible we include a description of the parameters used to compute the embeddings, together with simple statistics of the vocabulary, and description of the corpus from which the embeddings were computed. Direct links to the embeddings are provided when possible with explicit links to the source.

## Word2Vec embeddings from SBWC (by [Cristian Cardellino](https://github.com/crscardellino))


#### Embeddings
- Links to the embeddings: [.vec.gz]() () [.bin]() ()
- dimensions: 300
- vectors: 1000653

#### Algorithm
- Implementation: [Word2Vec](https://code.google.com/archive/p/word2vec/) with Skipgram
- Parameters: For details on parameters please refer to the [SBWCE page](http://crscardellino.me/SBWCE/)
     
#### Corpus
- Corpus: [Spanish Billion Word Corpus](http://crscardellino.me/SBWCE/) 
- Corpus Size: 1.4 billion words


## FastText embeddings from Spanish Wikipedia (by [FastText team](https://github.com/facebookresearch/fastText))

Links to the embeddings: [.vec](https://s3-us-west-1.amazonaws.com/fasttext-vectors/wiki.es.vec)(802 MB) [(.bin + .vec).zip](https://s3-us-west-1.amazonaws.com/fasttext-vectors/wiki.es.zip) (5.4 GB)
dimensions: 300
vectors: 

#### Algorithm
- Implementation: [FastText](https://github.com/facebookresearch/fastText) with Skipgram
- Parameters: FastText default parameters.
     
#### Corpus
- Corpus: [Spanish Billion Word Corpus](http://crscardellino.me/SBWCE/)
- Post processing: 



## FastText embeddings from SBWC (by (Jorge Pérez)[https://github.com/jorgeperezrojas])

Links to the embeddings: [.vec.gz](http://dcc.uchile.cl/~jperez/word-embeddings/fasttext-sbwc.3.6.e20.vec.gz)(802 MB) [.bin]((http://dcc.uchile.cl/~jperez/word-embeddings/fasttext-sbwc.3.6.e20.bin) (4.2 GB)
dimensions: 300
vectors: 855380

#### Algorithm
- Implementation: [FastText](https://github.com/facebookresearch/fastText) with Skipgram
- Parameters: 
    - min subword-ngram = 3 
    - max subword-ngram = 6
    - epochs = 20
    - dim = 300
    - all other paramenters set as default
     
#### Corpus
- Corpus: [Spanish Billion Word Corpus](http://crscardellino.me/SBWCE/)
- Corpus Size: 1.4 billion words
- Post processing: Besides the post processing of the raw corpus explained in the [SBWCE page](http://crscardellino.me/SBWCE/) that included deletion of punctuation, numbers, etc., the following processing was applied:
    - Words were converted to lower case letters
    - Every sequence of the 'DIGITO' keyword was replaced by (a single) '0'
    - All words of more than 3 characteres plus a '0' were ommitted (example: 'padre0')


