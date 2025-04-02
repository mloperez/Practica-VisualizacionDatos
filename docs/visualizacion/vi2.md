# Visualización 2 - Box plot


- [1. Definición de la técnica de visualización utilizada](#Definición-de-la-técnica-de-visualizacion-utilizada)
- [2. Descripción de los datos utilizados](#Descripción-de-los-datos-utilizados)
- [3. Explicación de la visualización](#Explicación-de-la-visualización)

---

## ℹ️ Definición de la técnica de visualización utilizada 
##### Tipo de visualización
Los diagramas de caja o Box Plot muestran la distribución de datos para una variable cuantitativa.

![Box Plot](../assets/images/BoxPlot.JPG)

El box plot se utiliza para mostrar estadísticas descriptivas de datos cuantitativos como:
- Mediana (la línea dentro de la caja) - El valor en el 50% de los datos.
- Rango intercuartílico (IQR) (la caja entre el primer cuartil y el tercer cuartil).
    - Q1 (primer cuartil): El valor en el 25% de los datos.
    - Q3 (tercer cuartil): El valor en el 75% de los datos.
- Valores atípicos (los puntos fuera de los bigotes).
- Mínimo y máximo (los extremos de los bigotes).

**Origen** 

 El conjunto de datos elegido es [Global Cybersecurity Threats 2015-2024](https://www.kaggle.com/datasets/atharvasoundankar/global-cybersecurity-threats-2015-2024) de la plataforma Kaggle.

 En este conjunto de datos se encuentran más de 3000 valores tomados desde 2015 a 2024 de las amenazas de Ciberseguridad a nivel mundial. Proporciona información exhaustiva sobre ciberataques, tipos de malware, sectores objetivo y países afectados.


**¿Cuándo usar diagramas Box Plot?**
- Para comparar varias categorías o grupos.
- Para ver la distribución de una sola variable.
- Para identificar si los datos se agrupan en patrones o los datos son dispersos.
- Para identificar outliers, estos serán los que se encuentren mas alejados de la mediana y cuartiles.
  
**Ejemplos de aplicación** - Los diagramas Box Plot son herramientas muy utiles ver la distribución de una sola variable y comparar grupos o categorías . Como por ejemplo:
- *¿Cómo varían los salarios en diferentes departamentos?* Se podria analizar la distribución de los salarios en cada uno de los departamentos. Por ejemplo: La distribución de los salarios en el dept. RRHH y ña distribución de salarios en el dept. IT

## 📥 Descripción de los datos utilizados 
#### Los datos utilizados ¿Son cuantitativos o cualitativos?

Los gráficos box plot se utilizan para representar los valores de una variable y conocer su posicion dentro del rango posible de valores.

En nuestro caso hemos utilizado dos variables:
  Financial Loss (in Millions $) --> variable cuantitativa continua ya que los valores de esta variable no son enteros.
  Attack Type --> datos de tipo cualitativo categóricos (Malware, DDoS...). Representación box plot por cada valor de esta variable "Attack Type".


#### ¿Qué estructura tienen que tener los datos para esta técnica?

Para poder representar un conjunto de datos con box plot se debe cumplir la siguiente estructura en los datos:
    Variable cuantitativa: Los datos deben ser numéricos (continua o discreta).
    Representación de una unica variable: Los datos deben representar una sola variable, aunque se puede comparar varias con un gráfico de cajas agrupadas (En nuestra   representación hacemos uso de varios graficos para representar varias variables categoricas).

#### ¿Existe alguna limitación en los datos para esta técnica? 

Algunas limitaciones en los datos para el diagrama Box plot:
- Uso de este tipo de visualización con datos categoricos (pais, color, género...) ya que no se pueden representar este tipo de datos en un espacio bidimensional. Para la representación de datos categoricos es recomendable el uso de otros tipos de visualizaciones como diagramas de barras, gráficos de cajas...
- Con la existencia de muchos outliers, el gráfico puede no ser representativo de la mayoría de los datos y la interpretación de los resultados puede ser errónea.
- Uso de gran volúmenes de datos, el box plot es eficaz para conjuntos de datos pequeños.

En nuestro caso no vemos ninguna de las limitaciones mencionadas en nuestro conjunto de datos.

#### ¿Hay medida mínima y máxima del juego de datos para esta técnica?

Para este tipo de visualización sí existe medida mínima y máxima de los datos:
- Medida mínima -->  Para poder calcular los cuartiles y la mediana se necesitan al menos 5-10 valores. Con pocos valores nos se veran patrones ni una distribución de los datos concreta.
- Medida máxima --> No existe medida máxima pero para la representación de conjuntos de datos muy grandes puede ser preferible utilizar otros gráficos como histogramas o gráficos de dispersión.
  
## 📈 Detalle de la visualización realizada 
#### Visualización 2 - Box Plot

Pasos del análisis de datos:

1. Elección de conjunto de datos
2. Análisis de los datos
3. Importación de los datos
4. Preparación de los datos
5. Visualización de los datos

Para crear el diagrama de dispersión o scatterplot se ha seguido el siguiente proceso:

- *Elección de conjunto de datos* - El conjunto de datos elegido es [Global Cybersecurity Threats 2015-2024](https://www.kaggle.com/datasets/atharvasoundankar/global-cybersecurity-threats-2015-2024) de la plataforma Kaggle.
- *Análisis de los datos* - Se revisan las variables del conjunto de datos elegido:

    - Country
    - Year
    - Attack Type
    - Target Industry
    - Financial Loss (in Million $)
    - Number of Affected Users
    - Attack Source
    - Security Vulnerability Type
    - Defense Mechanism Used
    - Incident Resolution Time (in Hours)

- *Importación de datos* - La herramienta elegida para esta visualización es [Flourish](https://flourish.studio/), donde se ha importado el conjunto de datos por csv
- *Preparación de los datos* - Para esta visualización, unicamente hemos filtrado los datos del Country USA, para comprar por cada tipo de ataque cuantos Millones supuso dicho ataque en USA
- *Visualización de los datos* - A continuación se muestra la representación de las variables ph y quality del conjunto de datos escogido con el digrama de dispersión.

[![Vista previa del informe](../assets/images/BoxPlot_cyber.JPG)](https://public.flourish.studio/visualisation/22306737/) 

*Nota: Hacer click en la imagen*


Cuestiones relevantes acerca de la visualización mostrada:
- ¿Qué tipos de datos se utiliza?
  Como se ha comnetado con anterioridad se hace uso de dos variables en esta reprsentación:
    Financial Loss (in Millions $) --> variable cuantitativa continua representada a lo largo del Box plot.
    Attack Type --> datos de tipo cualitativo categóricos (Malware, DDoS...). Representación de un box plot por cada valor de esta variable "Attack Type", así es sencillo poder comparar las diferentes variables categoricas.

- ¿Qué se pretende comunicar o descubrir con la visualización? ¿Ayuda la técnica a lograrlo?

  Como hemos visto anteriormente este tipo de representación se utiliza para comparar diferentes categorias, en este caso los tipos de ataques. Esta representación puede contestar varias preguntas como: ¿Qué tipo de ataque es el que más perdidas ha causado en USA desde 2015 a 2024? ¿Cuál el que menos?

  - SQL Injection Media: 59.03
  - DDoS Media: 54.37
  - Malware Media:49.88
  - Man-in-the-Middle Media:49.58
  - Phishing Media:48.84
  - Ransomware Media: 46.59

  El ataque que más perdidas causó en USA desde 2015 a 2024 fue el SQL Injection y el que menos Ransomware.
  Esta representación si ayuda a comprara varios ataques segun diferentes variables. Tambien se podría haber comparado, por ejemplo:
  
  - Número de usuarios afectados (x) con los diferentes ataques (y).
  - Mecanismo de defensa utilizado (y) con el tiempo de resolucion del incidente (x).

---

↩️**[Volver a Página de Inicio](../index.md)** ⬅️**[Visualización 1](./visualizacion/vi1.md)** ➡️**[Visualización 2](./visualizacion/vi2.md)**
