
# Ejemplos de uso de word embeddings computados con FastText

Primero cargamos los vectores/embeddings usando [gensim](https://radimrehurek.com/gensim/). Hay al menos dos formas posibles. La primera es cargar todos los vectores desde el archivo binario (.bin) en su formato nativo de FastText. Esta opción es más demandante en recursos (tiempo y memoria), pero es mucho más versatil por ejemplo para obtener vectores para palabras que no se ecuentran en el vocabulario. Esta forma se encuentra comentada en la siguiente celda


```python
# opción 1: cargar todos los vectores desde el formato binario (lento, requiere mucha memoria)
# from gensim.models.wrappers import FastText
# wordvectors_file = 'fasttext-sbwc.3.6.e20'
# wordvectors = FastText.load_fasttext_format(wordvectors_file)
```

La segunda forma, mucho más rápida, es cargar sólo una parte de los vectores. Para esto usamos el formato nativo de word2vec y cargamos una cantidad fija de vectores (se pueden cargar vectores generados por diversos métodos como FastText).


```python
# opción 2: cargar una cantidad fija de vectores (más rápido dependiendo de la cantidad cargada)
from gensim.models.keyedvectors import KeyedVectors
wordvectors_file_vec = 'fasttext-sbwc.3.6.e20.vec'
cantidad = 100000
wordvectors = KeyedVectors.load_word2vec_format(wordvectors_file_vec, limit=cantidad)
```

## Word vectors en analogías

Ejemplo de uso: `most_similar_cosmul(positive=lista_palabras_positivas, negative=lista_palabras_negativas)`

Esta llamada encuentra las palabras del vocabulario que están más cercanas a las palabras en `listas_palabras_positivas` y no estén cercanas a `lista_palabras_negativas` (para una formalización del procedimiento, ver la fórmula (4) en la Sección 6 de [este artículo](http://www.aclweb.org/anthology/W14-1618)).

Cuando `lista_palabras_positivas` contiene dos palabras, digamos `a` y `b_p`, y `lista_palabras_negativas` contiene una palabra, digamos `a_p`, el anterior procedimiento se lee coloquialmente como el encontrar la palabra `b` que responde a la pregunta: `a_p` es a `a` como `b_p` es a ???. El ejemplo clásico se tiene cuando `a` es `rey`, `b_p` es `mujer`, y `a_p` es `hombre`. La palabra buscada `b` es `reina`, pues `hombre` es a `rey` como `mujer` es a `reina`. (Personalmente considero que la intuición de palabras  más lejanas y más cercanas es mucho mejor que la de analogías, pero la de analogías es más común en los tutoriales de word embeddings). 

### Ejemplos considerando género


```python
wordvectors.most_similar_cosmul(positive=['rey','mujer'],negative=['hombre'])
```




    [('reina', 0.9141066670417786),
     ('isabel', 0.8743277192115784),
     ('princesa', 0.843113124370575),
     ('infanta', 0.8425983190536499),
     ('monarca', 0.8357319831848145),
     ('hija', 0.8211697340011597),
     ('consorte', 0.8179485201835632),
     ('iv', 0.813984215259552),
     ('esposa', 0.8115168213844299),
     ('ii', 0.8099035620689392)]




```python
wordvectors.most_similar_cosmul(positive=['actor','mujer'],negative=['hombre'])
```




    [('actriz', 0.9732905030250549),
     ('actores', 0.8580312728881836),
     ('actrices', 0.8464058041572571),
     ('cantante', 0.8347789645195007),
     ('reparto', 0.8277631402015686),
     ('protagonista', 0.8202100396156311),
     ('invitada', 0.8101590871810913),
     ('papel', 0.8021049499511719),
     ('guionista', 0.7968517541885376),
     ('intérprete', 0.7961310744285583)]




```python
wordvectors.most_similar_cosmul(positive=['hijo','mujer'],negative=['hombre'])
```




    [('hija', 0.9856907725334167),
     ('esposa', 0.9255169034004211),
     ('hijos', 0.9249492883682251),
     ('madre', 0.9138885736465454),
     ('hermana', 0.8996301889419556),
     ('hijas', 0.8754291534423828),
     ('casó', 0.8729564547538757),
     ('matrimonio', 0.8709645867347717),
     ('viuda', 0.8557067513465881),
     ('casada', 0.8546223044395447)]




```python
wordvectors.most_similar_cosmul(positive=['yerno','mujer'],negative=['hombre'])
```




    [('nuera', 0.9055585861206055),
     ('cuñada', 0.8592773079872131),
     ('esther', 0.8199110627174377),
     ('sobrina', 0.8171849846839905),
     ('suegra', 0.8157253265380859),
     ('hija', 0.8014461398124695),
     ('infanta', 0.8008802533149719),
     ('esposa', 0.8008227944374084),
     ('nieta', 0.7964767813682556),
     ('cuñado', 0.7955604195594788)]



### Ejemplos considerando conjugaciones


```python
wordvectors.most_similar_cosmul(positive=['jugar','canta'],negative=['cantar'])
```




    [('juega', 0.8944003582000732),
     ('jugando', 0.8376926183700562),
     ('jugará', 0.834348201751709),
     ('jugador', 0.8295056819915771),
     ('jugó', 0.8156978487968445),
     ('jugado', 0.8147079348564148),
     ('futbolista', 0.7927162647247314),
     ('juegue', 0.7921290397644043),
     ('fútbol', 0.7888965606689453),
     ('juegan', 0.7832154631614685)]




```python
wordvectors.most_similar_cosmul(positive=['jugar','cantaría'],negative=['cantar'])
```




    [('jugaría', 0.8204259276390076),
     ('jugará', 0.7848052382469177),
     ('juegue', 0.7704501152038574),
     ('jugara', 0.7684974670410156),
     ('ganamos', 0.7370696067810059),
     ('disputaría', 0.7334685325622559),
     ('perderá', 0.7326226234436035),
     ('lesionó', 0.723604679107666),
     ('perdería', 0.7234238386154175),
     ('jugó', 0.7223093509674072)]




```python
wordvectors.most_similar_cosmul(positive=['ir','jugando'],negative=['jugar'])
```




    [('yendo', 0.881558895111084),
     ('llevando', 0.8737362623214722),
     ('ido', 0.8687229156494141),
     ('saliendo', 0.8531793355941772),
     ('seguir', 0.8456405997276306),
     ('haciendo', 0.8450909852981567),
     ('va', 0.8442757725715637),
     ('vaya', 0.838218629360199),
     ('dando', 0.8275400996208191),
     ('estamos', 0.8271223306655884)]



### Ejemplos capitales y países


```python
wordvectors.most_similar_cosmul(positive=['santiago','venezuela'],negative=['chile'])
```




    [('caracas', 0.8996074795722961),
     ('bolívar', 0.8295609354972839),
     ('mérida', 0.8287113308906555),
     ('maracaibo', 0.826995849609375),
     ('miranda', 0.8242772817611694),
     ('santa', 0.8197780847549438),
     ('trujillo', 0.8175155520439148),
     ('pérez', 0.8143640756607056),
     ('rafael', 0.8114412426948547),
     ('lara', 0.8102367520332336)]




```python
wordvectors.most_similar_cosmul(positive=['habana','chile'],negative=['santiago'])
```




    [('cuba', 0.9782935380935669),
     ('venezuela', 0.8504070043563843),
     ('bolivia', 0.8276636600494385),
     ('rica', 0.8253333568572998),
     ('colombia', 0.819764256477356),
     ('cubana', 0.8174163699150085),
     ('argentina', 0.8128121495246887),
     ('brasil', 0.8126526474952698),
     ('panamá', 0.8123562932014465),
     ('nicaragua', 0.8074418306350708)]



## Word vectors en términos excluídos

Ejemplo de uso: `doesnt_match(lista_palabras)`

Esta llamada selecciona la palabra dentro de `listas_palabras` que está más lejana del resto de las palabras de la lista. La distancia es simplemente el ángulo entre las direcciones de los vectores de las palabras.


```python
wordvectors.doesnt_match(['blanco','azul','rojo','chile'])
```




    'chile'




```python
wordvectors.doesnt_match(['sol','luna','almuerzo','jupiter'])
```




    'jupiter'




```python
wordvectors.doesnt_match(['abril', 'mayo', 'septiembre', 'martes', 'julio'])
```




    'martes'




```python
wordvectors.doesnt_match(['lunes', 'martes', 'septiembre', 'jueves', 'viernes'])
```




    'septiembre'




```python
wordvectors.doesnt_match(['everton', 'cobreloa', 'huachipato', 'talca'])
```




    'talca'




```python
wordvectors.doesnt_match(['santiago', 'paris', 'talca', 'concepcion'])
```




    'concepcion'




```python
wordvectors.doesnt_match(['talca', 'paris', 'londres'])
```




    'talca'


