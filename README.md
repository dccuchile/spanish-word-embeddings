# Spanish Word Embeddings

Below you find links to Spanish word embeddings computed with different methods and from different corpora. Whenever it is possible, a description of the parameters used to compute the embeddings is included, together with simple statistics of the vectors, vocabulary, and description of the corpus from which the embeddings were computed. Direct links to the embeddings are provided, so please refer to the original sources for proper citation (also see [References](#references)). An example of the use of some of these embeddings can be found [here](examples/Ejemplo_WordVectors.md) or in this [tutorial](https://github.com/mquezada/starsconf2018-word-embeddings) (both in Spanish).

Summary (and links) for the embeddings in this page:

|   |Algorithm  |Corpus     |Corpus Size | #dimensions   |#vectors  |Credits    |
|---|-----------|-----------|------------|---------------|----------|-----------|
|[1](#fasttext-embeddings-from-suc)|FastText|Spanish Unannotated Corpora|3B|300|1,451,827|[José Cañete](https://github.com/josecannete)|
|[2](#fasttext-embeddings-from-sbwc)|FastText|Spanish Billion Word Corpus|1.4B|300|855,380|[Jorge Pérez](https://github.com/jorgeperezrojas)|
|[3](#glove-embeddings-from-sbwc)|Glove|Spanish Billion Word Corpus|1.4B|300|855,380|[Jorge Pérez](https://github.com/jorgeperezrojas)|
|[4](#fasttext-embeddings-from-spanish-wikipedia)|FastText|Spanish Wikipedia|???|300|985,667|[FastText team](https://github.com/facebookresearch/fastText)|
|[5](#word2vec-embeddings-from-sbwc)|Word2Vec|Spanish Billion Word Corpus|1.4B|300|1,000,653|[Cristian Cardellino](https://github.com/crscardellino)|

## FastText embeddings from SUC

#### Embeddings
Links to the embeddings (#dimensions=300, #vectors=1,451,827):
- [Vector format (.vec)](https://zenodo.org/record/3255001/files/embeddings-new_large-general_3B_fasttext.vec?download=1) (3.8 GB) 
- [Binary format (.bin)](https://zenodo.org/record/3255001/files/embeddings-new_large-general_3B_fasttext.bin?download=1) (5.9 GB)
More vectors with different sizes can be found [here](emb-from-suc.md)

#### Algorithm
- Implementation: [FastText](https://github.com/facebookresearch/fastText) with Skipgram
- Parameters: 
    - min subword-ngram = 3 
    - max subword-ngram = 6
    - minCount = 5
    - epochs = 20
    - dim = 300
    - all other parameters set as default
     
#### Corpus
- [Spanish Unannotated Corpora](https://github.com/josecannete/spanish-corpora)
- Corpus Size: 3 billion words
- Post processing: Explained in [Embeddings](https://github.com/BotCenter/spanishWordEmbeddings) and [Corpora](https://github.com/josecannete/spanish-corpora) repos, that include tokenization, lowercase, removed listings and urls.

## FastText embeddings from SBWC

#### Embeddings
Links to the embeddings (#dimensions=300, #vectors=855,380): 
- [Vector format (.vec.gz)](http://dcc.uchile.cl/~jperez/word-embeddings/fasttext-sbwc.vec.gz) (802 MB) 
- [Binary format (.bin)](http://dcc.uchile.cl/~jperez/word-embeddings/fasttext-sbwc.bin) (4.2 GB)

#### Algorithm
- Implementation: [FastText](https://github.com/facebookresearch/fastText) with Skipgram
- Parameters: 
    - min subword-ngram = 3 
    - max subword-ngram = 6
    - minCount = 5
    - epochs = 20
    - dim = 300
    - all other parameters set as default
     
#### Corpus
- [Spanish Billion Word Corpus](http://crscardellino.github.io/SBWCE/)
- Corpus Size: 1.4 billion words
- Post processing: Besides the post processing of the raw corpus explained in the [SBWCE page](http://crscardellino.github.io/SBWCE/) that included deletion of punctuation, numbers, etc., the following processing was applied:
    - Words were converted to lower case letters
    - Every sequence of the 'DIGITO' keyword was replaced by (a single) '0'
    - All words of more than 3 characteres plus a '0' were ommitted (example: 'padre0')

## GloVe embeddings from SBWC

#### Embeddings
Links to the embeddings (#dimensions=300, #vectors=855,380): 
- [Vector format (.vec.gz)](http://dcc.uchile.cl/~jperez/word-embeddings/glove-sbwc.i25.vec.gz) (906 MB) 
- [Binary format (.bin)](http://dcc.uchile.cl/~jperez/word-embeddings/glove-sbwc.i25.bin) (3.9 GB)

#### Algorithm
- Implementation: [GloVe](https://github.com/stanfordnlp/GloVe)
- Parameters: 
    - vector-size = 300
    - iter = 25
    - min-count = 5
    - all other parameters set as default

#### Corpus
- [Spanish Billion Word Corpus](http://crscardellino.github.io/SBWCE/) (see above)


## FastText embeddings from Spanish Wikipedia 

#### Embeddings
Links to the embeddings (#dimensions=300, #vectors=985,667): 
- [Vector format (.vec)](https://dl.fbaipublicfiles.com/fasttext/vectors-wiki/wiki.es.vec) (2.4 GB) 
- [Binary plus vector format (.zip)](https://dl.fbaipublicfiles.com/fasttext/vectors-wiki/wiki.es.zip) (5.4 GB)

#### Algorithm
- Implementation: [FastText](https://github.com/facebookresearch/fastText) with Skipgram
- Parameters: FastText default parameters
     
#### Corpus
- [Wikipedia Spanish Dump](https://archive.org/details/eswiki-20150105)

## Word2Vec embeddings from SBWC

#### Embeddings
Links to the embeddings (#dimensions=300, #vectors=1,000,653) 
- [Vector format (.txt.bz2)](http://cs.famaf.unc.edu.ar/~ccardellino/SBWCE/SBW-vectors-300-min5.txt.bz2) 
- [Binary format (.bin.gz)](http://cs.famaf.unc.edu.ar/~ccardellino/SBWCE/SBW-vectors-300-min5.bin.gz) 

#### Algorithm
- Implementation: [Word2Vec with Skipgram by GenSim](https://radimrehurek.com/gensim/models/word2vec.html) 
- Parameters: For details on parameters please refer to the [SBWCE page](http://crscardellino.github.io/SBWCE/)
     
#### Corpus
- [Spanish Billion Word Corpus](http://crscardellino.github.io/SBWCE/) 
- Corpus Size: 1.4 billion words


## References

- FastText embeddings from SUC: Word embeddings were computed by [José Cañete](https://github.com/josecannete) at [BotCenter](https://github.com/BotCenter). You can use these vectors as you wish under the MIT license. Please refer to [BotCenter Embeddings repo](https://github.com/BotCenter/spanishWordEmbeddings) for further discussion. You may also want to cite the FastText paper [Enriching Word Vectors with Subword Information](https://arxiv.org/abs/1607.04606).
- FastText embeddings from SBWC: Word embeddings were computed by [Jorge Pérez](https://github.com/jorgeperezrojas). You can use these vectors as you wish under the CC-BY-4.0 license. You may also want to cite the FastText paper [Enriching Word Vectors with Subword Information](https://arxiv.org/abs/1607.04606) and the [Spanish Billion Word Corpus project](http://crscardellino.github.io/SBWCE/). 
- GloVe embeddings from SBWC: Word embeddings were computed by [Jorge Pérez](https://github.com/jorgeperezrojas). You can use these vectors as you wish under the CC-BY-4.0 license. You may also want to cite the GloVe paper [GloVe: Global Vectors for Word Representation](https://nlp.stanford.edu/pubs/glove.pdf) and the [Spanish Billion Word Corpus project](http://crscardellino.github.io/SBWCE/).
- FastText embeddings from Spanish Wikipedia: Word embeddings were computed by [FastText team](https://github.com/facebookresearch/fastText).
Please refer to [FastText Pre-trained Vectors page](https://github.com/facebookresearch/fastText/blob/master/docs/pretrained-vectors.md) if you want to use these vectors.
- Word2Vec embeddings from SBWC: Word embeddings were computed by [Cristian Cardellino](https://github.com/crscardellino). Please refer to the [SBWCE page](http://crscardellino.github.io/SBWCE/) if you want to use these vectors.
