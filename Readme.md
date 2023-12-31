
Speed Dating[¶](#Speed-Dating)
==============================

Informe [¶](#Informe-Hito-3)
==================================

1- Motivacion:[¶](#1--Motivacion:)
----------------------------------

La motivación de este proyecto consiste en analizar los factores que influyen en el éxito de las citas rápidas, específicamente en la atracción mutua entre los participantes. Con este fin, se utiliza un dataset que contiene información sobre más de 8000 citas realizadas entre 2002 y 2004 en Estados Unidos. Este dataset comprende variables demográficas, de personalidad, de intereses y de preferencias de los participantes, además del resultado de cada cita (si se produjo o no un 'match'). El objetivo principal es identificar patrones y tendencias que determinen la compatibilidad entre las personas, y brindar una visión de los atributos más relevantes a la hora de encontrar pareja.


Preguntas y problemas:[¶](#Preguntas-y-problemas:)
--------------------------------------------------

Nos planteamos abordar las siguientes preguntas en los hitos posteriores:

1.  ¿Qué es lo más importante durante una cita? ¿La raza de una persona tiene relevancia en la obtención de likes o matches?
    
    *   Se pretende entrenar un modelo de clasificación interpretativo, como un árbol de decisión, para identificar los atributos más relevantes a la hora de generar un match.
2.  ¿Es posible predecir si una cita resultará en un match en función de los atributos de los sujetos?
    
    *   Se buscará desarrollar un modelo predictivo enfocado en obtener una métrica de clasificación precisa para los matches.
3.  ¿Existen estereotipos reconocibles entre los participantes de las citas rápidas? ¿Hay algún estereotipo que tenga mayor probabilidad de generar un match?
    
    *   En general, el análisis realizado hasta ahora se ha centrado en un conjunto limitado de atributos, como los matches por género y las preferencias por género. En esta etapa, se utilizarán técnicas de clustering para analizar el conjunto completo de atributos y detectar posibles estereotipos presentes en estos experimentos. Se explorará si algún grupo específico obtiene una mayor cantidad de matches.Al realizar esta segmentación de grupos, se analizará si existe algún grupo que obtenga una cantidad significativamente mayor de matches.

Metodologías a implementar[¶](#Metodologías-a-implementar)
----------------------------------------------------------

Pregunta 1: Importancia atributos.[¶](#Pregunta-1:-Importancia-atributos.)
--------------------------------------------------------------------------

El objetivo de la pregunta 1 es identificar los atributos más relevantes para lograr un match utilizando técnicas de clasificación. Para lograr esto, se implementará un Árbol de decisión que nos permitirá visualizar los nodos asociados a la ganancia de información. Además, se empleará un Random Forest para extraer las características más importantes a través de la importancia asignada a los atributos.

El procedimiento a seguir será el siguiente:

#### 1- Preprocesamiento:[¶](#1--Preprocesamiento:)

El objetivo principal es comprender en detalle los atributos de los participantes, por lo que procederemos a eliminar todas las columnas que no estén directamente relacionadas con los aspectos físicos o emocionales. No obstante, ciertas características nominales, como la raza y el género, son de relevancia para el experimento, por lo tanto, las conservaremos y las codificaremos para su inclusión en el modelo.

Asimismo, enfrentaremos el desafío de manejar los valores nulos presentes en el conjunto de datos. Dado que nuestra cantidad de datos no es muy extensa, eliminar filas con valores nulos resultaría en una pérdida significativa de información. Para abordar este problema, aplicaremos técnicas adecuadas para generar valores de entrada y completar los datos faltantes, evitando así la pérdida de información valiosa.

#### 2- Árbol de Decisión[¶](#2--Árbol-de-Decisión)

Durante este experimento, se entrenará un árbol de decisión y se calcularán sus métricas. Aunque el objetivo principal no es obtener una métrica alta, utilizaremos los resultados para validar que el árbol generado sea coherente con los datos. Para llevar a cabo esta validación, dividiremos los datos en un conjunto de entrenamiento y un conjunto de pruebas utilizando una proporción de 70-30, respectivamente.

#### 3- Random Forest[¶](#3--Random-Forest)

Se aprovechará el conjunto de datos preprocesados para entrenar un Random Forest, que es un modelo de ensamble que utiliza múltiples árboles de decisión. Luego, se realizará un ranking de los atributos más importantes utilizando la función "feature_importances_" del Random Forest. Esta función nos proporcionará una medida de la importancia relativa de cada atributo en la predicción del resultado (matches).

El Random Forest es una excelente herramienta para este tipo de análisis, ya que permite identificar los atributos más influyentes en la generación de matches y brindar insights sobre qué características tienen mayor relevancia en la formación de parejas.


Conclusiones derivadas de los resultados obtenidos y planificación futura:[¶](#Conclusiones-derivadas-de-los-resultados-obtenidos-y-planificación-futura:)
----------------------------------------------------------------------------------------------------------------------------------------------------------

### Experimento 1 Importancia de atributos : (¿Qué atributos son los más importantes a la hora de hacer un match?):[¶](#Experimento-1--Importancia-de-atributos-:-(¿Qué-atributos--son-los-más-importantes-a-la-hora-de-hacer-un-match?):)

Es fundamental tener en cuenta que el árbol de decisión es un modelo y el Random Forest consiste en modelos "greedy", lo que implica que en cada iteración se dividen las variables en el hiperespacio utilizando aquellas que generan una mayor ganancia de información. Siguiendo esta lógica, se puede observar que los atributos relacionados con el atractivo físico y el sentido del humor son los que logran la mejor separación del espacio (como se puede apreciar en los nodos principales del árbol de decisión y en la feature importance del Random Forest). Los resultados obtenidos con el Random Forest son coherentes con los del árbol de decisión en este sentido.

En respuesta a la pregunta, podemos afirmar que los parámetros "attractive\_partner" y "attractive\_o" son los más influyentes a la hora de hacer match, seguidos por "funny\_partner" y "funny\_o". A partir de ahí, el resto de atributos no son significativamente más relevantes en la clasificación de las citas.

### Experimento 2 Clasificación: (¿Se puede predecir un match en base a las características de los participantes?):[¶](#Experimento-2-Clasificación:-(¿Se-puede-predecir--un-match-en-base-a-las-características-de-los-participantes?):)

Con respecto a los resultados relacionados con la clasificación, se observa una alta fiabilidad en la manera en que se pre-procesan los datos antes de entrenar los modelos. Se nota una considerable disminución en la cantidad de datos desde el estado bruto hasta el procesado para el entrenamiento del modelo, inicialmente de ~8000 a ~500 filas, debido principalmente a la ausencia de datos en las columnas relevantes para el entrenamiento. Luego, se reduce a ~1100 filas, lo que conduce a una menor cantidad de datos, pero de alta confiabilidad.

Es importante destacar que, desde el principio, se esperaba que las 8000 filas se redujeran al menos a la mitad, es decir, a 4000 filas, por lo que el paso de este número a 1000 no representa una disminución significativa en términos de datos fiables y representativos del dataset.

En conclusión, basándonos en los resultados analizados, podemos afirmar con un 75% de precisión que si tenemos la información necesaria de dos personas, podemos predecir si terminarán haciendo match en una cita al ingresarlos en el modelo clasificador correspondiente.

### Experimento 3 Clustering:(¿Existen estereotipos reconocibles?¿Hay un estereotipo que es más propenso a hacer match ?)[¶](#Experimento-3-Clustering:(¿Existen-estereotipos-reconocibles?¿Hay-un-estereotipo-que-es-más-propenso-a-hacer-match-?))

Para K-means, se identificaron únicamente 2 clusters, mientras que DBscan no pudo separar clusters para su eps óptimo (ver visualización de clusters mediante PCA). La validación de los clusters de K-means indica una agrupación moderada, reflejada por un coeficiente de Silhouette no tan alto (0.3). La matriz de similitud muestra un cluster denso y otro más disperso.

Los resultados del clustering no cumplen completamente con las expectativas, ya que no se logró identificar una gran cantidad de "estereotipos" en las citas. Sin embargo, la caracterización de cada cluster encontrado permite señalar algunas diferencias entre ellos (ver observaciones de caracterización). En cuanto a si un estereotipo es propenso a hacer match, se puede afirmar que existen diferencias consistentes entre los dos clusters encontrados (en cuanto a decisiones y matches), pero estas diferencias no son tan significativas entre sí.

### Conclusiones finales y Planificación futura:[¶](#Conclusiones-finales-y-Planificación-futura:)

Las conclusiones que podemos extraer de los datos del proyecto están limitadas por la cantidad de estos. Nuestro dataset posee alrededor de ~8000 filas, y al ser procesadas, pueden reducirse considerablemente. Debido a esto, es importante mencionar que las conclusiones extraídas en este proyecto están sesgadas hacia este grupo particular de datos y no necesariamente representan una realidad generalizable. Además, la falta de datos claros puede conducir a patrones aleatorizados o poco definidos. Para mejorar el proyecto, sería recomendable buscar nuevas fuentes de datos que se puedan agregar para obtener patrones más claros y robustos.

En cuanto a la clasificación, en una planificación futura, sería ideal encontrar un punto de equilibrio entre la cantidad de filas que se pierden y la completitud de la data. Es decir, permitir que algunas filas con ciertos atributos vacíos se incluyan en el modelo de entrenamiento sin perder una buena representación del dataset. De esta manera, el modelo de clasificación será capaz de reflejar de manera más precisa la información contenida en los datos y, al recibir una consulta, podrá clasificar los datos con parámetros de mayor calidad y coherencia con la realidad simulada por los datos.

Finalmente, es recomendable orientar el análisis exploratorio de datos en función del objetivo final del proyecto para obtener indicadores relevantes sobre si se puede lograr el éxito deseado. Por ejemplo, si el objetivo es predecir matches, es recomendable explorar si existen ciertos factores o correlaciones que sugieran la probabilidad de un match. En este caso, el EDA realizado estuvo enfocado en responder preguntas generales y no se alineó directamente con los objetivos finales del proyecto.

Los algoritmos de machine learning pueden aplicarse a cualquier conjunto de datos, siempre y cuando estos tengan patrones internos (como se puede observar en los diferentes resultados obtenidos en el clustering). Sin embargo, es fundamental comprender lo que se está haciendo y validar los resultados de alguna manera para asegurar la robustez de los análisis y conclusiones.

Anexo:[¶](#Anexo:)
------------------

*   Codigo completo: [https://colab.research.google.com/drive/14FzcwQTW2XPdq-yqN0ZQW-0TNFEjUDqj#scrollTo=mbwTnF5YMi4C](https://colab.research.google.com/drive/14FzcwQTW2XPdq-yqN0ZQW-0TNFEjUDqj#scrollTo=mbwTnF5YMi4C)

Fuentes y material de apoyo:[¶](#Fuentes-y-material-de-apoyo:)
--------------------------------------------------------------

*   Clustering:Para la implementación de los experimentos se utilizaron principalmente el material de los laboratorios y tutoriales (obtener SSE método codo,matriz de similitud).
*   Clasificación:

