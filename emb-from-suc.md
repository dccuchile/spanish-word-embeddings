## FastText embeddings from SUC

Below you find embeddings for different sizes computed from the [Spanish Unannotated Corpora](https://github.com/josecannete/spanish-corpora).

#### Embeddings
Links to the embeddings:
##### XS (#dimensions=10, #vectors=1313423): 
- [Vector format (.vec)](https://zenodo.org/record/3234051/files/embeddings-xs-model.vec?download=1) (122 MB) 
- [Binary format (.bin)](https://zenodo.org/record/3234051/files/embeddings-xs-model.bin?download=1) (209 MB)
##### S (#dimensions=30, #vectors=1313423): 
- [Vector format (.vec)](https://zenodo.org/record/3234051/files/embeddings-s-model.vec?download=1) (348 MB) 
- [Binary format (.bin)](https://zenodo.org/record/3234051/files/embeddings-s-model.bin?download=1) (579 MB)
##### M (#dimensions=100, #vectors=1313423): 
- [Vector format (.vec)](https://zenodo.org/record/3234051/files/embeddings-m-model.vec?download=1) (1.1 GB) 
- [Binary format (.bin)](https://zenodo.org/record/3234051/files/embeddings-m-model.bin?download=1) (1.9 GB)
##### L (#dimensions=300, #vectors=1313423): 
- [Vector format (.vec)](https://zenodo.org/record/3234051/files/embeddings-l-model.vec?download=1) (3.4 GB) 
- [Binary format (.bin)](https://zenodo.org/record/3234051/files/embeddings-l-model.bin?download=1) (5.6 GB)
##### new L (#dimensions=300, #vectors=1451827): 
- [Vector format (.vec)](https://zenodo.org/record/3255001/files/embeddings-new_large-general_3B_fasttext.vec?download=1) (3.8 GB) 
- [Binary format (.bin)](https://zenodo.org/record/3255001/files/embeddings-new_large-general_3B_fasttext.bin?download=1) (5.9 GB)

#### Algorithm
- Implementation: [FastText](https://github.com/facebookresearch/fastText) with Skipgram
- Parameters: 
    - min subword-ngram = 3 
    - max subword-ngram = 6
    - minCount = 5
    - epochs = 20
    - dim = 10, 30, 100, 300, 300
    - all other parameters set as default
     
#### Corpus
- [Spanish Unannotated Corpora](https://github.com/josecannete/spanish-corpora)
- Corpus Size: 2.6 billion words and 3 billion words (for the new 300 dim)
- Post processing: Explained in [Embeddings](https://github.com/BotCenter/spanishWordEmbeddings) and [Corpora](https://github.com/josecannete/spanish-corpora) repos, that include tokenization, lowercase, removed listings and urls.
