# FAQ

### How to use them?

Please check out our [Tutorial.](https://github.com/dccuchile/spanish-word-embeddings/blob/master/examples/Ejemplo_WordVectors.md)

### Are the embeddings ordered in any way?

Yes, the embeddings are ordered by frequencies.

### How can I get the frequencies of the words?

In FastText models, you can obtain the frequencies of the words by using the following code:

    import fasttext
    model = fasttext.load_model("your_embedding_model.bin")
    palabras, frecuencias = model.get_words(include_freq=True)

### My question is not here

Please feel free to create a new [Issue](https://github.com/dccuchile/spanish-word-embeddings/issues) with your doubts or thoughts.
