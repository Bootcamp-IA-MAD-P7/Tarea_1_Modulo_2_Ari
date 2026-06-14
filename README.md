# Tarea_1_Modulo_2_Ari
EDA - Análisis Exploratorio de Datos | Bootcamp IA Factoría F5
Investigación: Análisis Exploratorio de Datos (EDA)

1. ¿Qué es el EDA y cuál es su propósito en el análisis de datos?

El EDA (Exploratory Data Analysis) es la fase inicial de cualquier proyecto de análisis de datos en la que se examina un dataset para entender su estructura, calidad y patrones generales, antes de aplicar modelos o sacar conclusiones definitivas.

Su propósito principal es:


Conocer qué datos tenemos (tipos, tamaño, formato).
Detectar errores, valores nulos, duplicados o atípicos.
Descubrir relaciones entre variables.
Generar hipótesis que luego se podrán validar.
Decidir qué transformaciones o limpieza necesita el dataset antes de modelar.


En resumen: es como hacer un "reconocimiento del terreno" antes de construir cualquier modelo o sacar conclusiones.


2. ¿Qué tipos de datos existen en un EDA?

De forma general, los datos se dividen en dos grandes grupos:

Cualitativos (categóricos):


Nominales: categorías sin un orden lógico (ej. color de ojos, género, ciudad).
Ordinales: categorías con un orden lógico (ej. nivel educativo: primaria < secundaria < universidad).


Cuantitativos (numéricos):


Discretos: valores enteros, contables (ej. número de hijos, número de habitaciones).
Continuos: valores que pueden tomar cualquier valor dentro de un rango (ej. altura, temperatura, salario).


Identificar correctamente el tipo de cada variable es clave porque determina qué tipo de gráficos, estadísticas y transformaciones podemos aplicarle.


3. Diferencia entre análisis univariado, bivariado y multivariado


Univariado: analiza una sola variable a la vez. Busca entender su distribución, valores típicos, dispersión y posibles outliers (ej. histograma de la edad de los clientes).
Bivariado: analiza la relación entre dos variables. Busca ver si existe correlación, dependencia o algún patrón conjunto (ej. relación entre horas de estudio y nota del examen, mediante un scatterplot).
Multivariado: analiza tres o más variables a la vez, buscando interacciones más complejas entre ellas (ej. un mapa de calor de correlaciones entre varias columnas numéricas, o un pairplot de seaborn).


La progresión típica del EDA va de lo más simple (univariado) a lo más complejo (multivariado), igual que primero entendemos una variable sola antes de ver cómo se relaciona con otras.


4. ¿Qué es la estadística descriptiva?

Es el conjunto de técnicas que permiten resumir y describir las características principales de un conjunto de datos mediante números y gráficos, sin sacar conclusiones más allá de los propios datos (eso sería estadística inferencial).

Incluye medidas como:


Tendencia central: media, mediana, moda.
Dispersión: rango, varianza, desviación estándar, rango intercuartílico.
Forma de la distribución: asimetría (skewness) y curtosis.


En Python, el método .describe() de pandas nos da rápidamente la mayoría de estas medidas para las columnas numéricas de un DataFrame.


5. ¿Qué es la limpieza de datos y qué tareas suelen incluirse?

La limpieza de datos (data cleaning) es el proceso de detectar y corregir (o eliminar) datos incorrectos, incompletos, duplicados o inconsistentes, para que el dataset sea fiable antes de analizarlo o modelarlo.

Tareas habituales:


Valores nulos: detectarlos (isnull()) y decidir si se eliminan o se imputan (con media, mediana, moda, o un valor constante).
Duplicados: identificar (duplicated()) y eliminar filas repetidas (drop_duplicates()).
Outliers: detectarlos y decidir si se eliminan, se transforman o se dejan (dependiendo del contexto).
Normalización/Estandarización: escalar variables numéricas a un rango común (ej. Min-Max Scaling o Z-score) para que tengan un peso comparable.
Corrección de tipos: asegurarse de que cada columna tiene el tipo de dato correcto (fechas como datetime, números como int/float, etc.).
Corrección de inconsistencias: por ejemplo, unificar "Madrid", "madrid", "MADRID" en un único formato.



6. ¿Qué papel juegan pandas, matplotlib y seaborn en un EDA?


pandas: es la librería base para cargar, explorar y manipular los datos. Permite leer ficheros (CSV, Excel...), ver las primeras filas (head()), conocer tipos de datos (info()), estadísticas (describe()), filtrar, agrupar (groupby), tratar nulos y duplicados, etc. Es el punto de partida de casi todo EDA.
matplotlib: es la librería de visualización "base" de Python. Permite crear gráficos personalizados (histogramas, scatterplots, líneas, boxplots...) con mucho control sobre los detalles, aunque requiere más código.
seaborn: está construida sobre matplotlib y ofrece gráficos estadísticos más elaborados y estéticos con menos código (heatmaps de correlación, pairplots, boxplots por categoría, distribuciones, etc.). Es muy usada en EDA porque facilita ver relaciones entre variables rápidamente.


En resumen: pandas para explorar y preparar los datos, matplotlib y seaborn para visualizarlos y detectar patrones de forma gráfica.


7. ¿Qué es una matriz de correlación y para qué sirve en el EDA?

Una matriz de correlación es una tabla que muestra el coeficiente de correlación (normalmente de Pearson, entre -1 y 1) entre cada par de variables numéricas de un dataset.


Un valor cercano a 1 indica una correlación positiva fuerte (cuando una variable sube, la otra también).
Un valor cercano a -1 indica una correlación negativa fuerte (cuando una sube, la otra baja).
Un valor cercano a 0 indica que no hay relación lineal aparente entre ellas.


En el EDA sirve para:


Detectar rápidamente qué variables están relacionadas entre sí.
Identificar posible multicolinealidad (variables muy correlacionadas entre sí, lo cual puede ser un problema para algunos modelos).
Orientar qué variables pueden ser más relevantes para predecir una variable objetivo.


En Python se calcula con df.corr() y se suele visualizar con un heatmap de seaborn (sns.heatmap()).


8. ¿Qué son los outliers y qué métodos existen para detectarlos y tratarlos?

Los outliers (valores atípicos) son observaciones que se desvían significativamente del resto de los datos. Pueden deberse a errores de medición/captura, o ser valores reales pero excepcionales.

Métodos de detección:


Visualización: boxplots, scatterplots, histogramas.
Rango intercuartílico (IQR): se consideran outliers los valores por debajo de Q1 - 1.5*IQR o por encima de Q3 + 1.5*IQR.
Z-score: se consideran outliers los valores que están a más de 2-3 desviaciones estándar de la media.


Métodos de tratamiento:


Eliminarlos, si se confirma que son errores.
Transformarlos (capping/winsorización): sustituirlos por el valor del límite superior/inferior aceptable.
Transformación de la variable (ej. logarítmica) para reducir su impacto.
Dejarlos, si representan información real y relevante (ej. un cliente VIP con gasto muy alto).


La decisión depende siempre del contexto del negocio/problema, no solo de la estadística.


9. ¿Qué es el hipothesis testing y para qué sirve en el EDA?

El hipothesis testing (contraste de hipótesis) es una técnica de estadística inferencial que permite comprobar, con una base estadística, si una afirmación sobre los datos es probablemente cierta o no, usando una muestra de datos.

El proceso típico es:


Plantear una hipótesis nula (H0) (normalmente "no hay efecto/diferencia") y una hipótesis alternativa (H1).
Elegir un test estadístico adecuado (t-test, chi-cuadrado, ANOVA, etc.).
Calcular un p-valor.
Si el p-valor es menor que un umbral (normalmente 0.05), se rechaza H0, concluyendo que sí hay evidencia de diferencia/relación.


En el EDA, el hypothesis testing sirve para validar de forma más rigurosa las intuiciones que hemos detectado visualmente. Por ejemplo: si en un gráfico parece que un grupo tiene una media distinta a otro, un test de hipótesis nos permite comprobar si esa diferencia es estadísticamente significativa o podría ser simplemente fruto del azar.


Parte 2: Práctica de EDA

El notebook con la práctica paso a paso se encuentra en este repositorio: EDA_practica.ipynb.

En él se desarrollan los siguientes pasos siguiendo la guía proporcionada:


Carga del dataset y primera exploración (head(), info(), shape, describe()).
Identificación de tipos de variables (categóricas, numéricas, ordinales).
Limpieza de datos: tratamiento de nulos, duplicados y tipos de datos.
Análisis univariado: distribución de cada variable (histogramas, boxplots, countplots).
Análisis bivariado: relaciones entre pares de variables (scatterplots, boxplots por categoría).
Análisis multivariado: matriz de correlación y heatmap, pairplot.
Detección y tratamiento de outliers.
Conclusiones del análisis exploratorio.
