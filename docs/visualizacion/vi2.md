# Visualización 2 - Box plot


- [1. Definición de la técnica de visualización utilizada](#Definición-de-la-técnica-de-visualizacion-utilizada)
- [2. Descripción de los datos utilizados](#Descripción-de-los-datos-utilizados)
- [3. Explicación de la visualización](#Explicación-de-la-visualización)

---

## ℹ️ Definición de la técnica de visualización utilizada 
##### Tipo de visualización
Los diagramas de caja o Box Plot muestran la distribución de datos para una variable continua.

![Box Plot](../../docs/assets/images/BoxPlot.JPG)


**Origen** - QUITAR- No se puede decir que un solo autor inventó este gráfico, pero sin duda hay que mencionar a Sir John Frederick W. Herschel (Reino Unido, 1792 - 1871) y Sir Francis Galton (Reino Unido, 1822 - 1911). Sus investigaciones en astronomía y genética fueron clave para que llegáramos al gráfico de dispersión tal como lo usamos hoy.

**¿Cuándo usar diagramas Box Plot?**
- Para comparar varias categorías o grupos.
- Para ver la distribución deuna sola variable.
- Para identificar si los datos se agrupan en patrones o los datos son dispersos.
- Para identificar outliers, estos serán los que se encuentren mas alejados de la mediana y cuartiles.
  
**Ejemplos de aplicación** - Los diagramas Box Plot son herramientas muy utiles ver la distribución de una sola variable y comparar grupos o categorías . Como por ejemplo:
- *¿Cómo varían los salarios en diferentes departamentos?* Se podria analizar la distribución de los salarios en cada uno de los departamentos. Por ejemplo: La distribución de los salarios en el dept. RRHH y ña distribución de salarios en el dept. IT

## 📥 Descripción de los datos utilizados 
#### Los datos utilizados ¿Son cuantitativos o cualitativos?

Los gráficos de dispersión se utilizan para identificar patrones, tendencias y posibles correlaciones entre las variables que se analizan. Por tanto, los mejores datos para un diagrama de dispersión son aquellos donde tienes dos variables numéricas (cuantitativas) que deseas comparar o analizar en términos de su relación o correlación.

#### ¿Qué estructura tienen que tener los datos para esta técnica?

Como se ha comentado anteriormente, en los diagramas de dispoersión se representan datos de dos variables. Una variable se representa en el eje horozontal X y la otra variable se representa en el eje vertical Y. Por tanto los datos deben ser cuantitativos y tener una relación de contexto, es decir, por ejemplo si se quiere representar que relación puede existir entre las variables edad y altura es necesario que los datos de ambas variables sean tomados de las mismas personas.

#### ¿Existe alguna limitación en los datos para esta técnica? 
Existesn varias limitantes en los datos, por su tipologia o relación entre ellos, a la hora de representar con diagramas de dispoersión. 

Una limitación que hemos visto con anterioridad es la falta de relación entre las variables a analizar. Por tanto para este tipo de visualización es necesario tener o sospechar que existe una relación entre ambas variables.

Otra limitación es el uso de este tipo de visualización con datos categoricos (pais, color, género...) ya que no se pueden representar este tipo de datos en un espacio bidimensional. Para la representación de datos categoricos es recoemndable el uso de otros tipos de visualizaciones como diagramas de barras, gráficos de cajas...

#### ¿hay medida mínima y máxima del juego de datos para esta técnica?

Para este tipo de visualización sí existe medida mínima y máxima de los datos:
- Medida mínima --> Al menos se necesitarán 2 puntos, aunque no se podrá obtener mucha información sobre la relación entre las dos variables. Se podrá estimar una tendencia aunque estará lejos de un analisis con tendencia más real conseguida con más datos.
  
- Medida máxima --> Aunque los diagramas de dispersión pueden manejar gran cantidad de datos, se debe realizar una buena limpieza de los datos y realiar un buen uso del los colores para que no sea dificil la interpretación.
  
## 📈 Detalle de la visualización realizada 
#### Visualización 2 - Box Plot

Pasos del análisis de datos:

1. Elección de conjunto de datos
2. Análisis de los datos
3. Importación de los datos
4. Preparación de los datos
5. Visualización de los datos

Para crear el diagrama de dispersión o scatterplot se ha seguido el siguiente proceso:

- *Elección de conjunto de datos* - El conjunto de datos elegido es [Student Depression](https://www.kaggle.com/datasets/adilshamim8/student-depression-dataset) de la plataforma Kaggle.
- *Análisis de los datos* - Se revisan los datos elegidos cuyas variables elegidas para la visualización son ph y quality, de todas las que se muestran a continuación:

   Input variable
    - ID: Unique identifier for each student
    - Demographics: Age, Gender, City
    - Academic Indicators: CGPA, Academic Pressure, Study Satisfaction
    - Lifestyle & Wellbeing: Sleep Duration, Dietary Habits, Work Pressure, Job Satisfaction, Work/Study Hours
    - Additional Factors: Profession, Degree, Financial Stress, Family History of Mental Illness, and whether the student has ever had suicidal thoughts 

  Output variable
    - Depression_Status: A binary indicator (0/1 or Yes/No) that denotes whether a student is experiencing depression

- *Importación de datos* - La herramienta elegida para esta visualización es LookerStudio, donde se ha importado el conjunto de datos por csv
- *Preparación de los datos* - En este caso, para esta visualización, no ha hecho falta realzar ninguna transformación en los datos.
- *Visualización de los datos* - A continuación se muestra la representación de las variables ph y quality del conjunto de datos escogido con el digrama de dispersión.

[![Vista previa del informe](../../docs/assets/images/Visualizacion_dispersion.JPG)](https://lookerstudio.google.com/reporting/1d9fc4ae-ae8b-410b-ac2d-b1471f3023ab) 

*Nota: Hacer click en la imagen*


Cuestiones relevantes acerca de la visualización mostrada:
- ¿Qué tipos de datos se utiliza?

  Como hemos visto anteriormente, los diagramas de dispersión son idelaes cuando se tienen datos numéricos y se desea saber si existe una relación directa entre ellos. En este caso las variables a tratar son ph y quality.

  ph --> datos de tipo decimal.

  quality --> datos de tipo entero.
  
- ¿Qué se pretende comunicar o descubrir con la visualización? ¿Ayuda la técnica a lograrlo?

  El diagrama de dispersión muestra la relación que existe entre el ph de vinos rojos Portugueses y su calidad. Como se puede observar existe una relación positiva ya que a medida que los valores de una variable aumenta, los valores de la otra variable también tienden a aumentar.
  
---

**[Volver a Página de Inicio](../index.md)**
