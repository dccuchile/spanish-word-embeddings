
# Ejemplos de uso de word embeddings computados con FastText

Primero cargamos los vectores/embeddings usando [gensim](https://radimrehurek.com/gensim/). Hay al menos dos formas posibles. La primera es cargar todos los vectores desde el archivo binario (.bin) en su formato nativo de FastText. Esta opción es más demandante en recursos (tiempo y memoria), pero es mucho más versatil por ejemplo para obtener vectores para palabras que no se ecuentran en el vocabulario. Esta forma se encuentra comentada en la siguiente celda


```python
# opción 1: cargar todos los vectores desde el formato binario (lento, requiere mucha memoria)
# from gensim.models.wrappers import FastText
# wordvectors_file = 'fasttext-sbwc.3.6.e20'
# wordvectors = FastText.load_fasttext_format(wordvectors_file).wv
```

La segunda forma, mucho más rápida, es cargar sólo una parte de los vectores. Para esto usamos el formato nativo de word2vec y cargamos una cantidad fija de vectores (se pueden cargar vectores generados por diversos métodos como FastText).


```python
# opción 2: cargar una cantidad fija de vectores (más rápido dependiendo de la cantidad cargada)
from gensim.models.keyedvectors import KeyedVectors
wordvectors_file_vec = 'fasttext-sbwc.3.6.e20.vec'
cantidad = 100000
wordvectors = KeyedVectors.load_word2vec_format(wordvectors_file_vec, limit=cantidad).wv
```

## Word vectors en analogías

Ejemplo de uso: `most_similar_cosmul(positive=lista_palabras_positivas, negative=lista_palabras_negativas)`

Esta llamada encuentra las palabras del vocabulario que están más cercanas a las palabras en `listas_palabras_positivas` y no estén cercanas a `lista_palabras_negativas` (para una formalización del procedimiento, ver la fórmula (4) en la Sección 6 de [este artículo](http://www.aclweb.org/anthology/W14-1618)).

Cuando `lista_palabras_positivas` contiene dos palabras, digamos `a` y `b_p`, y `lista_palabras_negativas` contiene una palabra, digamos `a_p`, el anterior procedimiento se lee coloquialmente como el encontrar la palabra `b` que responde a la pregunta: `a_p` es a `a` como `b_p` es a ???. El ejemplo clásico se tiene cuando `a` es `rey`, `b_p` es `mujer`, y `a_p` es `hombre`. La palabra buscada `b` es `reina`, pues `hombre` es a `rey` como `mujer` es a `reina`. (Personalmente considero que la intuición de palabras  más lejanas y más cercanas es mucho mejor que la de analogías, pero la de analogías es más común en los tutoriales de word embeddings). 

### Ejemplos considerando género


```python
wordvectors.most_similar_cosmul(positive=['rey','mujer'],negative=['hombre'])
```




    [('reina', 0.9141532778739929),
     ('infanta', 0.8582408428192139),
     ('berenguela', 0.8470728993415833),
     ('princesa', 0.8445042371749878),
     ('consorte', 0.835599422454834),
     ('emperatriz', 0.8247664570808411),
     ('regente', 0.8239887356758118),
     ('infantas', 0.8104739785194397),
     ('hermanastra', 0.8072930574417114),
     ('regencia', 0.8037241101264954)]




```python
wordvectors.most_similar_cosmul(positive=['actor','mujer'],negative=['hombre'])
```




    [('actriz', 0.9687138795852661),
     ('compositora', 0.8557133078575134),
     ('cantante', 0.8482002019882202),
     ('actrices', 0.845941424369812),
     ('dramaturga', 0.8354867696762085),
     ('presentadora', 0.8346402645111084),
     ('bailarina', 0.830103874206543),
     ('coprotagonista', 0.8284398317337036),
     ('guionista', 0.828334629535675),
     ('cantautora', 0.827379047870636)]




```python
wordvectors.most_similar_cosmul(positive=['hijo','mujer'],negative=['hombre'])
```




    [('hija', 0.9641352295875549),
     ('esposa', 0.9116341471672058),
     ('madre', 0.9057636260986328),
     ('nieta', 0.8976945877075195),
     ('hermanastra', 0.8958925604820251),
     ('nuera', 0.8941904902458191),
     ('hijos', 0.8940641283988953),
     ('embarazada', 0.8930323123931885),
     ('primogénita', 0.8921582698822021),
     ('hermana', 0.8830597996711731)]




```python
wordvectors.most_similar_cosmul(positive=['yerno','mujer'],negative=['hombre'])
```




    [('nuera', 0.8991931080818176),
     ('cuñada', 0.8967029452323914),
     ('esposa', 0.879116415977478),
     ('hija', 0.8787108659744263),
     ('suegra', 0.8752366304397583),
     ('sobrina', 0.8678680658340454),
     ('hermanastra', 0.8615662455558777),
     ('viuda', 0.8587483167648315),
     ('yernos', 0.8577941656112671),
     ('nieta', 0.8574915528297424)]



### Ejemplos considerando conjugaciones


```python
wordvectors.most_similar_cosmul(positive=['jugar','canta'],negative=['cantar'])
```




    [('juega', 0.9270390272140503),
     ('jugará', 0.903049647808075),
     ('juegue', 0.8957996368408203),
     ('jugando', 0.8832089304924011),
     ('juegan', 0.868077278137207),
     ('jugado', 0.8658616542816162),
     ('jugó', 0.8645129799842834),
     ('juegas', 0.8533656597137451),
     ('jugaría', 0.8508267402648926),
     ('jugara', 0.8470847606658936)]




```python
wordvectors.most_similar_cosmul(positive=['jugar','cantaría'],negative=['cantar'])
```




    [('jugaría', 1.002570629119873),
     ('jugarían', 0.951291024684906),
     ('jugara', 0.9422449469566345),
     ('disputaría', 0.9186552166938782),
     ('jugará', 0.908361554145813),
     ('jugaran', 0.8989543914794922),
     ('jugase', 0.8874876499176025),
     ('disputarían', 0.8822468519210815),
     ('jugó', 0.8740344643592834),
     ('ficharía', 0.8733252286911011)]




```python
wordvectors.most_similar_cosmul(positive=['ir','jugaba'],negative=['jugar'])
```




    [('iba', 0.8358239531517029),
     ('iría', 0.8330116868019104),
     ('iban', 0.8197974562644958),
     ('andaba', 0.8181521892547607),
     ('venía', 0.8127180933952332),
     ('pasaba', 0.806372880935669),
     ('salía', 0.8061624765396118),
     ('llegaba', 0.8007727861404419),
     ('ido', 0.8003631830215454),
     ('venían', 0.790458083152771)]



### Ejemplos de política


```python
wordvectors.most_similar_cosmul(positive=['pinochet','argentino'],negative=['chileno'])
```




    [('menem', 0.8302620649337769),
     ('perón', 0.8235861659049988),
     ('galtieri', 0.8023414611816406),
     ('onganía', 0.8013173937797546),
     ('videla', 0.7994171380996704),
     ('alfonsín', 0.7985163331031799),
     ('kirchner', 0.7978085279464722),
     ('kirchnerismo', 0.7961062788963318),
     ('dictador', 0.795034646987915),
     ('peronismo', 0.7945936322212219)]




```python
wordvectors.most_similar_cosmul(positive=['pinochet','peruano'],negative=['chileno'])
```




    [('fujimori', 0.879432737827301),
     ('leguía', 0.8281515836715698),
     ('dictador', 0.814770519733429),
     ('ollanta', 0.8126699328422546),
     ('humala', 0.80531907081604),
     ('apristas', 0.7981743812561035),
     ('odría', 0.7976544499397278),
     ('aprista', 0.7967919707298279),
     ('belaúnde', 0.7959150671958923),
     ('orbegoso', 0.7874271273612976)]




```python
wordvectors.most_similar_cosmul(positive=['bachelet','argentina'],negative=['chile'])
```




    [('kirchner', 0.9510541558265686),
     ('mandataria', 0.8866869211196899),
     ('dilma', 0.8731293082237244),
     ('rousseff', 0.870695173740387),
     ('kirchnerista', 0.8655502200126648),
     ('duhalde', 0.8641150593757629),
     ('scioli', 0.856192946434021),
     ('alfonsín', 0.8515958189964294),
     ('perón', 0.8501841425895691),
     ('kirchnerismo', 0.8450447916984558)]




```python
wordvectors.most_similar_cosmul(positive=['bachelet','brasil'],negative=['chile'])
```




    [('dilma', 0.9780699610710144),
     ('rousseff', 0.9759045243263245),
     ('lula', 0.92941814661026),
     ('inácio', 0.8913270831108093),
     ('inacio', 0.8903253674507141),
     ('mandataria', 0.8615238666534424),
     ('kirchner', 0.8515970706939697),
     ('luiz', 0.8485301733016968),
     ('cavaco', 0.846683919429779),
     ('collor', 0.83381187915802)]



### Ejemplos capitales y países


```python
wordvectors.most_similar_cosmul(positive=['santiago','venezuela'],negative=['chile'])
```




    [('caracas', 0.9048638343811035),
     ('barinas', 0.871845543384552),
     ('brión', 0.8565776944160461),
     ('cojedes', 0.8514757752418518),
     ('cumaná', 0.8507834672927856),
     ('guanare', 0.8507248759269714),
     ('maturín', 0.8474243879318237),
     ('mariño', 0.84685218334198),
     ('barquisimeto', 0.8451403975486755),
     ('falcón', 0.8430416584014893)]




```python
wordvectors.most_similar_cosmul(positive=['habana','chile'],negative=['santiago'])
```




    [('cuba', 0.9638005495071411),
     ('venezuela', 0.8891817331314087),
     ('colombia', 0.8762299418449402),
     ('cubana', 0.8471046686172485),
     ('nicaragua', 0.8443880081176758),
     ('cubanos', 0.8370179533958435),
     ('ecuador', 0.8361555337905884),
     ('brasil', 0.8355840444564819),
     ('cubano', 0.8315702080726624),
     ('panamá', 0.8302189111709595)]



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




    'almuerzo'




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




    'paris'




```python
wordvectors.doesnt_match(['talca', 'paris', 'londres'])
```




    'talca'


