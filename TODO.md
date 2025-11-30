# Análisis de Factores que Influyen en el Rendimiento Académico


## 1. Introducción

El rendimiento académico es un tema central en el ámbito educativo, ya que influye directamente en las oportunidades académicas y profesionales futuras de los estudiantes. Sin embargo, el desempeño en un examen no depende únicamente de la “inteligencia” o capacidad innata, sino de una combinación de factores académicos, familiares, personales y de estilo de vida.

En este proyecto se analiza un conjunto de datos de estudiantes que recoge información sobre hábitos de estudio, asistencia a clase, motivación, implicación de los padres, características del profesorado, entorno escolar y otros aspectos relacionados con su día a día. Junto con estas variables, se dispone además de la calificación final obtenida en un examen (`Exam_Score`), que se utilizará como medida del rendimiento académico.

A partir de estos datos, se aplicarán distintas herramientas estadísticas para explorar qué factores parecen tener una mayor influencia sobre el rendimiento, con el objetivo de obtener una visión más clara de qué elementos podrían potenciar (o dificultar) el desempeño académico de los estudiantes.

### 1.1 Tema general

El tema general de este proyecto es el análisis de los factores que influyen en el rendimiento académico de los estudiantes, medido a través de la variable `Exam_Score`. Para ello se utilizará información sobre hábitos de estudio, contexto familiar, entorno escolar y estilo de vida.

Se prestará especial atención a variables como las horas de estudio (`Hours_Studied`), la asistencia a clase (`Attendance`), el nivel de motivación (`Motivation_Level`), la calidad percibida del profesorado (`Teacher_Quality`), las horas de sueño (`Sleep_Hours`), la implicación de los padres (`Parental_Involvement`), el tipo de escuela (`School_Type`) y la presencia de dificultades de aprendizaje (`Learning_Disabilities`).

### 1.2 Objetivo general

El objetivo general del estudio es analizar estadísticamente el conjunto de datos *Student Performance Factors* para identificar y cuantificar la relación entre distintos factores académicos, familiares, personales y de entorno, y el rendimiento académico de los estudiantes medido por la variable `Exam_Score`.

### 1.3 Objetivos específicos

A partir del objetivo general, se plantean los siguientes objetivos específicos:

1. Describir la distribución de las principales variables del conjunto de datos y caracterizar el comportamiento de la variable de rendimiento `Exam_Score`.
2. Explorar, de forma gráfica y numérica, la relación entre variables académicas clave (`Hours_Studied`, `Attendance`, `Previous_Scores`) y la calificación del examen.
3. Evaluar si existen diferencias estadísticamente significativas en el rendimiento (`Exam_Score`) entre grupos de estudiantes definidos por su nivel de motivación (`Motivation_Level`) y por la calidad percibida del profesorado (`Teacher_Quality`).
4. Construir un modelo de regresión lineal múltiple que permita explicar el rendimiento académico (`Exam_Score`) a partir de un conjunto seleccionado de variables explicativas académicas, familiares, personales y del entorno escolar.
5. Preparar el terreno para la aplicación de técnicas adicionales como el Análisis de Componentes Principales (PCA) y, opcionalmente, métodos de agrupamiento (*clustering*).

### 1.4 Preguntas de investigación

Las preguntas de investigación que guían el análisis son:

- **P1:** ¿Cómo se relacionan las horas de estudio (`Hours_Studied`) y la asistencia a clase (`Attendance`) con la calificación de examen `Exam_Score`?
- **P2:** ¿Existen diferencias significativas en la media de `Exam_Score` entre grupos de estudiantes definidos por su nivel de motivación (`Motivation_Level`) y por la calidad percibida del profesorado (`Teacher_Quality`)?
- **P3:** Considerando simultáneamente varios factores (horas de estudio, asistencia, desempeño previo, motivación, calidad del profesorado, implicación parental, tipo de escuela, horas de sueño, presencia de dificultades de aprendizaje, etc.), ¿qué variables se comportan como mejores predictores de la calificación de examen `Exam_Score` en un modelo de regresión lineal múltiple?

### 1.5 Descripción del conjunto de datos y alcance de las variables

El dataset *Student Performance Factors* contiene información de 6607 estudiantes y 20 variables. La variable de respuesta es `Exam_Score`, que representa la puntuación obtenida en un examen. El conjunto incluye:

- Variables académicas: `Hours_Studied`, `Attendance`, `Previous_Scores`, `Tutoring_Sessions`.
- Variables familiares y socioeconómicas: `Parental_Involvement`, `Family_Income`, `Parental_Education_Level`, `Access_to_Resources`.
- Variables personales y de estilo de vida: `Motivation_Level`, `Sleep_Hours`, `Physical_Activity`, `Peer_Influence`, `Extracurricular_Activities`, `Learning_Disabilities`.
- Variables del entorno escolar: `School_Type`, `Teacher_Quality`, `Distance_from_Home`, `Internet_Access`.

Aunque el conjunto original es amplio, para responder de forma clara a las preguntas planteadas se trabajará principalmente con un subconjunto de variables: `Exam_Score`, `Hours_Studied`, `Attendance`, `Previous_Scores`, `Tutoring_Sessions`, `Motivation_Level`, `Teacher_Quality`, `Sleep_Hours`, `Parental_Involvement`, `Family_Income`, `School_Type` y `Learning_Disabilities`. La inclusión explícita de `Learning_Disabilities` permite considerar posibles diferencias asociadas a dificultades de aprendizaje y reducir el riesgo de sesgos en la interpretación de los resultados.

---

## 2. Análisis exploratorio de datos (EDA)

En esta sección se estudia el comportamiento de las variables seleccionadas y su relación inicial con el rendimiento académico.

### 2.1 Vista general del subconjunto de interés

- Presentar el número de observaciones y variables del subconjunto utilizado.
- Clasificar las variables en:
  - Numéricas: `Exam_Score`, `Hours_Studied`, `Attendance`, `Previous_Scores`, `Tutoring_Sessions`, `Sleep_Hours`.
  - Categóricas: `Motivation_Level`, `Teacher_Quality`, `Parental_Involvement`, `Family_Income`, `School_Type`, `Learning_Disabilities`.
- Resumir la presencia de valores faltantes, destacando que la mayoría de variables están completas y que los faltantes se concentran en `Teacher_Quality` (y otras variables que pueden tratarse en el preprocesamiento).

### 2.2 Análisis univariante

#### 2.2.1 Variables numéricas

- Describir la distribución de `Exam_Score` mediante medidas de tendencia central y dispersión, así como mediante histogramas.
- Analizar la distribución de `Hours_Studied`, `Attendance`, `Previous_Scores`, `Tutoring_Sessions` y `Sleep_Hours`, identificando posibles asimetrías o valores extremos.

#### 2.2.2 Variables categóricas

- Presentar tablas de frecuencias y, opcionalmente, gráficos de barras para `Motivation_Level`, `Teacher_Quality`, `Parental_Involvement`, `Family_Income`, `School_Type` y `Learning_Disabilities`.
- Comentar la proporción de estudiantes con dificultades de aprendizaje, la distribución de niveles de motivación y la percepción de la calidad del profesorado.

### 2.3 Relaciones bivariantes con `Exam_Score`

#### 2.3.1 Relación con `Hours_Studied` y `Attendance` (P1)

- Utilizar gráficos de dispersión entre `Hours_Studied` y `Exam_Score`, y entre `Attendance` y `Exam_Score`.
- Calcular correlaciones simples entre `Exam_Score`, `Hours_Studied` y `Attendance`.
- Interpretar visual y numéricamente la fuerza y dirección de las relaciones, como primer acercamiento a la pregunta P1.

#### 2.3.2 Relación con `Motivation_Level` y `Teacher_Quality` (P2)

- Representar `Exam_Score` mediante diagramas de caja (*boxplots*) por niveles de `Motivation_Level` y de `Teacher_Quality`.
- Observar diferencias en medianas y dispersión entre grupos, anticipando el análisis inferencial de P2.

#### 2.3.3 Correlaciones entre variables numéricas

- Calcular y representar la matriz de correlaciones entre las variables numéricas principales.
- Destacar las variables más correlacionadas con `Exam_Score`, como motivación para su uso posterior en el modelo de regresión (P3).

---

## 3. Preparación de datos

Antes de aplicar técnicas inferenciales, es necesario realizar ciertas transformaciones sobre los datos.

### 3.1 Tratamiento de valores faltantes

- Identificar las variables con valores faltantes dentro del subconjunto de interés (principalmente `Teacher_Quality`).
- Justificar la estrategia de imputación: por ejemplo, reemplazar los valores faltantes de `Teacher_Quality` por la categoría más frecuente (moda), dado que el porcentaje de datos faltantes es reducido.

### 3.2 Codificación de variables categóricas

#### 3.2.1 Variables ordinales

Se consideran ordinales las variables:

- `Motivation_Level`
- `Teacher_Quality`
- `Parental_Involvement`
- `Family_Income`

Para las que se asignan valores numéricos respetando el orden natural (`Low < Medium < High`).

#### 3.2.2 Variables nominales

Las variables `School_Type` y `Learning_Disabilities` se tratan como nominales, empleando codificación mediante variables ficticias (*one-hot encoding*), por ejemplo, generando columnas como `School_Type_Private` y `Learning_Disabilities_Yes`.

### 3.3 Estandarización de variables numéricas

Las variables numéricas (`Hours_Studied`, `Attendance`, `Previous_Scores`, `Tutoring_Sessions`, `Sleep_Hours`) se estandarizan (media 0, desviación estándar 1) con el fin de:

- Facilitar la interpretación comparada de los coeficientes en la regresión.
- Preparar los datos para técnicas sensibles a la escala, como PCA o *clustering*.

### 3.4 Datasets derivados

Se distinguen dos objetos principales:

- **`df_main`**: subconjunto de variables de interés, utilizado para el EDA.
- **`df_model`**: versión transformada (imputación, codificación y estandarización), empleada en los modelos de regresión y PCA.

---

## 4. Aplicación de técnicas estadísticas

### 4.1 Pruebas de hipótesis para P2

Para responder a la pregunta P2 se emplean pruebas ANOVA de un factor:

- ANOVA entre `Exam_Score` y niveles de `Motivation_Level`.
- ANOVA entre `Exam_Score` y niveles de `Teacher_Quality`.

En cada caso se plantean las hipótesis:

- $H_0$: las medias de `Exam_Score` son iguales en todos los grupos.
- $H_1$: al menos un grupo presenta una media diferente.

Se interpretan los valores del estadístico F y del p-valor, y se consultan las medias por grupo para describir las diferencias encontradas.

### 4.2 Regresión lineal múltiple para P1 y P3

Se construye un modelo de regresión lineal múltiple con `Exam_Score` como variable dependiente e incluye como predictores:

- Variables de esfuerzo y desempeño previo: `Hours_Studied`, `Attendance`, `Previous_Scores`, `Tutoring_Sessions`, `Sleep_Hours`.
- Variables ordinales: `Motivation_Level_ord`, `Teacher_Quality_ord`, `Parental_Involvement_ord`, `Family_Income_ord`.
- Variables nominales codificadas: `School_Type_Private`, `Learning_Disabilities_Yes`.

Se analizan:

- El coeficiente de determinación $R^2$ y la significancia global del modelo.
- Los coeficientes asociados a `Hours_Studied` y `Attendance`, para cuantificar su efecto sobre `Exam_Score` (P1).
- Las variables que resultan estadísticamente significativas y su contribución relativa como predictores del rendimiento (P3).

Opcionalmente, se evalúa el ajuste mediante un esquema entrenamiento/prueba (*train/test*) y se reportan métricas como $R^2$ y el error cuadrático medio.

### 4.3 Análisis de Componentes Principales (PCA) como complemento

El PCA se aplica a las variables numéricas estandarizadas con el propósito de:

- Reducir la dimensionalidad del conjunto de predictores.
- Identificar componentes que agrupen variables en factores interpretables (por ejemplo, “esfuerzo académico” o “bienestar”).

Se analizan la varianza explicada por cada componente y las cargas (*loadings*) de las variables originales, discutiendo su posible interpretación en el contexto del rendimiento académico.

---

## 5. Resultados y conclusiones

### 5.1 Resumen de hallazgos

En esta sección se resumen los resultados más relevantes del EDA, de las pruebas de hipótesis y del modelo de regresión, destacando:

- La relación entre horas de estudio, asistencia y rendimiento.
- Las diferencias en `Exam_Score` según niveles de `Motivation_Level` y `Teacher_Quality`.
- Los predictores más importantes identificados por la regresión y, en su caso, por el PCA.

### 5.2 Respuesta a las preguntas de investigación

Se responde explícitamente a P1, P2 y P3, apoyando las afirmaciones en los resultados numéricos (correlaciones, p-valores, coeficientes y $R^2$).

### 5.3 Limitaciones y trabajo futuro

Se discuten las principales limitaciones del estudio (representatividad del dataset, ausencia de ciertas variables, naturaleza no causal de los resultados) y se proponen posibles extensiones, como el uso de modelos más complejos o análisis específicos para estudiantes con dificultades de aprendizaje.
