# Spanish Word Embeddings

Below you find links to Spanish word embeddings computed with different methods. Whenever it is possible we include a description of the parameters used to compute the embeddings, together with simple statistics of the vocabulary, and description of the corpus from which the embeddings were computed. Direct links to the embeddings are provided when possible with explicit links to the source.

## FastText embeddings from SBWC (by [Jorge Pérez](https://github.com/jorgeperezrojas))

#### Embeddings
Links to the embeddings (#dimensions=300, #vectors=855380): 
- [Vector format (.vec.gz)](http://dcc.uchile.cl/~jperez/word-embeddings/fasttext-sbwc.3.6.e20.vec.gz)(802 MB) 
- [Binary format (.bin)](http://dcc.uchile.cl/~jperez/word-embeddings/fasttext-sbwc.3.6.e20.bin) (4.2 GB)

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


## FastText embeddings from Spanish Wikipedia (by [FastText team](https://github.com/facebookresearch/fastText))

#### Embeddings
Links to the embeddings (#dimensions=300, #vectors=985667): 
- [Vector format (.vec)](https://s3-us-west-1.amazonaws.com/fasttext-vectors/wiki.es.vec) (2.4 GB) 
- [Binary plus Vector format (.zip)](https://s3-us-west-1.amazonaws.com/fasttext-vectors/wiki.es.zip) (5.4 GB)

#### Algorithm
- Implementation: [FastText](https://github.com/facebookresearch/fastText) with Skipgram
- Parameters: FastText default parameters
     
#### Corpus
- Corpus: [Wikipedia Spanish Dump](https://archive.org/details/eswiki-20150105)


## Word2Vec embeddings from SBWC (by [Cristian Cardellino](https://github.com/crscardellino))

#### Embeddings
Links to the embeddings (#dimensions=300, #vectors=1000653) 
- [Vector format (.txt.bz2)](http://cs.famaf.unc.edu.ar/~ccardellino/SBWCE/SBW-vectors-300-min5.txt.bz2) 
- [Binary format (.bin.gz)](http://cs.famaf.unc.edu.ar/~ccardellino/SBWCE/SBW-vectors-300-min5.bin.gz) 

#### Algorithm
- Implementation: [Word2Vec with Skipgram by GenSim](https://radimrehurek.com/gensim/models/word2vec.html) 
- Parameters: For details on parameters please refer to the [SBWCE page](http://crscardellino.me/SBWCE/)
     
#### Corpus
- Corpus: [Spanish Billion Word Corpus](http://crscardellino.me/SBWCE/) 
- Corpus Size: 1.4 billion words


