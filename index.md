# Inicio

📘 Asignatura: **Visualización de Datos**

🔖 Actividad: **Práctica**

👩‍💼 Alumno: **Maria López Pérez**

📆 Fecha: **10/06/25**

Este informe documenta la entrega de la Práctica de la asignatura Visualización de Datos del Máster de Ciencia de Datos de la UOC.   

## Objetivos

Elección adecuada de herramientas y técnicas: Identificar y utilizar herramientas específicas para la creación de visualizaciones que se alineen con las características del conjunto de datos, el tipo de análisis realizado y los objetivos del proyecto.
Creación de un proyecto profesional: Diseñar una visualización que combine estructura, diseño y contenido de calidad profesional, orientada a públicos especializados y no especializados.

Respuestas a preguntas clave: Formular y responder razonadamente. a preguntas clave relacionadas con los datos, utilizando la visualización como un medio para facilitar la exploración y la comprensión.

Diseño interactivo y comunicativo: Incorporar elementos interactivos que mejoren la experiencia del usuario y favorezcan la comunicación efectiva de los resultados.
Requisitos adicionales: Además de la visualización, el estudiante deberá presentar un video explicativo que aborde los siguientes aspectos, distribuidos en los porcentajes indicados:

**[20%] Proceso de creación: Explicar las etapas del desarrollo, las decisiones de diseño tomadas y los fundamentos detrás de dichas decisiones.**

Para este proyecto he utilizado dos herramientas principales: R y Flourish.
R es una herramienta muy potente para el análisis de datos, que me ha permitido limpiar, transformar y agrupar los datos según mis necesidades. He usado R para             calcular totales, balances, proporciones y preparar los ficheros CSV para su visualización.

Por otro lado, he usado Flourish para crear visualizaciones interactivas. Flourish me permite diseñar gráficos dinámicos, comprensibles y atractivos para públicos no       técnicos, como gestores públicos o ciudadanos.

La combinación de ambas herramientas me ha permitido realizar un análisis completo: desde el tratamiento de los datos hasta su comunicación visual.

## [20%] Presentación en vivo: Mostrar las características de la visualización mientras se navega por ella, destacando aspectos clave del diseño y la funcionalidad

## [15%] Conjunto de datos: Describir brevemente las características más relevantes del conjunto de datos utilizado, su origen y cualquier proceso de preparación realizado

### Análisis de Datos

Se ha elegido la herramienta PowerBI para el análisis de los datos y se ha utilizado DAX y R para el tratamiento de los datos.

Datos seleccionados:

[Presupuesto general 2024](https://datos.gob.es/es/catalogo/l01280796-presupuestos-presupuesto-general-2024)

[Presupuestos. Proyectos de Presupuesto de ejercicios anteriores - Conjunto de datos - datos.gob.es](https://datos.gob.es/es/catalogo/l01280796-presupuestos-historico-de-proyectos-2017-20201)

Los datos estan distribuidos de la siguiente manera:

📁Carpeta Gastos

    “Proyecto Presupuesto 2022 V50.csv”
    “Gastos_Proyecto_2023.csv”
    “V50_Gastos_Proyecto_2024.csv”
    “V50_Gastos_Proyecto_2025.csv”

📁Carpeta Ingresos

    “Ingresos_Proyecto_2022.csv”
    “Ingresos_Proyecto_2023.csv”
    “V50_Ingresos_Proyecto_2024.csv”
    “V40_Ingresos_Presupuesto_2025.csv”
    
### Ingesta de datos

Para la ingesta de los datos en PowerBI, vamos a Inicio > Obtener Datos > Carpeta. Seleccionamos las carpetas donde se encuentran nuestros conjuntos de datos. Y seleccionamos --> Combinar y Transformar Datos

Para combinar lo datos PowerBI toma de ejemplo el primer archivo en este caso → Gastos_Proyecto_2022.csv y Ingresos_Proyecto_2022.csv
He estructurado el proyecto de forma clara y coherente. En primer lugar, presento los datos utilizados y explico brevemente su origen y estructura: cada fila representa un registro económico con un centro, año, tipo (ingreso o gasto) e importe.

### Transformación de los datos

## ℹ️ Transformaciones en Tabla Gastos


Una vez ingestados veremos que se nos han creado unas tablas con las diferentes columnas. En la primera fila se encuentran cada una de las variables y en el resto sus valores.

Columnas creadas:

- Source. Name
- Centro
- Descripción Centro
- Sección
- Descripción Sección
- Programa
- Descripción Programa
- Capítulo
- Descripción Capítulo
- Económico
- Relación de Partidas
- Proyecto Presupuesto 2022 V50

Vemos que hay una de ellas que en los datos originales no tiene el mismo nombre en todos los conjuntos de datos “Proyecto Presupuesto 2022 V50”. Por tanto comprobamos que en este columna para los csv no usados de ejemplo “Gastos_Proyecto_2023.csv”, “V50_Gastos_Proyecto_2024.csv” y “V50_Gastos_Proyecto_2025.csv” todos los valores son null.


📉#Transformación 1 - Tabla Gastos

 📌**Objetivo:** Obtener los gastos de todos los año en columnas diferentes.     


Nuestra primera transformación va a ser modificar el nombre de la columna para que al combinarlas coja correctamente los valores.

Vemos que PowerBI ha realizado los siguientes pasos para combinar los tres archivos:



Vamos a revisar paso a paso que es lo que ha hecho sola la herramienta y crearemos un paso más para solventar el problema.

- Paso 1: Origen → Cargar los archivos de la carpeta:
```
= Folder.Files("C:\Users\María\Desktop\MASTER BigData\Visualizacion\powerbi\Gastos")
```

- Paso 2: Archivos ocultos filtrados1 → Filtra y elimina las filas donde el valor de Hidden es true.
```
= Table.SelectRows(Origen, each [Attributes]?[Hidden]? <> true)
```

- Paso 3: Invocar función personalizada1 → Crea una nueva columna en la tabla llamada “Content” que contiene el contenido de los archivos en formato binario.
```
= Table.AddColumn(#"Archivos ocultos filtrados1", "Transformar archivo", each #"Transformar archivo (2)"([Content]))
```

- Paso 4: Columnas con nombre cambiado1 → Renombra una columna de la tabla a “Source.Name”
```
= Table.RenameColumns(#"Invocar función personalizada1", {"Name", "Source.Name"})
```

- Paso 5: Otras columnas quitadas1 → Selecciona un subconjunto de columnas de la tabla, para mantener ciertas columnas y elimina el resto.

```
= Table.SelectColumns(#"Columnas con nombre cambiado1", {"Source.Name", "Transformar archivo"})
```

- Paso 6: Columna de tabla expandida1 → (NUEVO PASO CREADO) Este nuevo paso se encarga de expandir las tablas dentro de la columna "Transformar archivo" y obtener todas las columnas de todos los archivos CSV
```
= Table.ExpandTableColumn(
	#"Otras columnas quitadas1",
	"Transformar archivo",
	List.Distinct(List.Combine(List.Transform(#"Otras columnas quitadas1"[Transformar archivo], each Table.ColumnNames(_))))
)
```

Por tanto ahora vamos tenemos estas columnas:

- Source.Name
- Centro
- Descripción Centro
- Sección
- Descripción Sección
- Programa
- Descripción Programa
- Capítulo
- Descripción Capítulo
- Económico
- Relación d Partidas
- Proyecto Presupuesto 2022 V50
- Gastos_2023_V50
- Proyecto Presupuesto 2024 V50
- Proy Presupuesto 2025

- Paso 7: Tipo cambiado → Ajustamos el tipo de variable
```
= Table.TransformColumnTypes(#"Columna de tabla expandida1",{{"Source. Name", type text}, {"Centro", Int64.Type}, {"Descripcion Centro", type text}, {"Seccion", Int64.Type}, {"Descripcion Seccion", type text}, {"Programa", Int64.Type}, {"Descripcion Programa", type text}, {"Capitulo", Int64.Type}, {"Descripcion Capitulo", type text}, {"Economico", Int64.Type}, {"Relación de partidas", type text}, {"Proyecto Presupuesto 2022 V50", Int64.Type}, {" Proyecto Presupuesto 2024 V50 ", Int64.Type}, {"Gastos_2023_V50", Int64.Type}, {"Proy Presupuesto 2025", Int64.Type}})
```


📉Transformación 2 -Tabla Gastos

 📌**Objetivo:** Crear una nueva columna “Gastos 2022_2023_2024_2025” con los gastos de las columnas añadidas en el paso 6 y después eliminar las columnas no deseadas.

El siguiente paso que vamos a realizar es unificar en una única columna, las cuatro anteriormente indicadas:



Debido a que cuando una de ellas tiene un valor el resto tiene el valor null, esto es debido al combinar las tres tablas en una sola.

- Paso 8: Rename columns →  (NUEVO PASO CREADO)

```
= Table.RenameColumns(#"Tipo cambiado", List.Transform(Table.ColumnNames(#"Tipo cambiado"), each {_, Text.Trim(_)}))
```

- Paso 9: Add column → (NUEVO PASO CREADO) Crea una columna de las cuatro anteriores, Gastos_2022_2023_2024_2025
```
= Table.AddColumn(#"Rename columns", "Gastos_2022_2023_2024_2025", each
	List.First(List.RemoveNulls({
    	[Proyecto Presupuesto 2022 V50],
    	[Gastos_2023_V50],
    	[Proyecto Presupuesto 2024 V50],
    	[Proy Presupuesto 2025]
	}))
)
```

- Paso 10: Add column → (NUEVO PASO CREADO)Eliminar el resto de columnas de gatos
```
= Table.RemoveColumns(#"Add column", {
	"Proyecto Presupuesto 2022 V50",
	"Gastos_2023_V50",
	"Proyecto Presupuesto 2024 V50",
	"Proy Presupuesto 2025"
})
```



📉 Transformación 3 -Tabla Gastos

📌**Objetivo:** Crear una nueva columna “Año” con los diferentes años (lo obtenemos de la columna Source.Name).


Además vemos que se ha generado una primera columna donde se indica el nombre del archivo. Esto nos viene bien para poder obtener valores del mismo y saber si la tabla que estamos utilizando es un ingreso o gasto y el año al que corresponde.


Para evitar hacer modificaciones en la tabla original, vamos a crear tablas nuevas donde transformaremos los datos.

Para crear una tabla a partir de la original, hacemos click en la tabla original > Referencia.

- Paso 11: column año → (NUEVO PASO CREADO) Crea una nueva columna “Año” con el año que corresponde

```
= Table.AddColumn(#"Delete columns", "Año", each
	if Text.Contains([Source.Name], "2022") then "2022"
	else if Text.Contains([Source.Name], "2023") then "2023"
	else if Text.Contains([Source.Name], "2024") then "2024"
	else if Text.Contains([Source.Name], "2025") then "2025"
	else null
)
```


📉Transformación 4 -Tabla Gastos


📌**Objetivo:** Eliminar valores nulos o vacíos.

El siguiente paso que vamos a realizar es eliminar valores vacíos o nulos.


- Paso 12: Delete Null →  (NUEVO PASO CREADO)

```
= Table.SelectRows(#"Filas filtradas", each [Gastos_2022_2023_2024_2025] <> null and [Gastos_2022_2023_2024_2025] <> "")

= Table.SelectRows(#"Filas filtradas", each [Economico] <> null and [Economico] <> "")

= Table.SelectRows(#"Tipo cambiado1", each [Descripcion Centro] <> null and [Descripcion Centro] <> "")
```

## ℹ️ Transformaciones en Tabla Ingresos

Una vez ingestados veremos que se nos han creado unas tablas con las diferentes columnas. En la primera fila se encuentran cada una de las variables y en el resto sus valores.

Columnas creadas:

- Source.Name
- Centro
- Descripción Centro
- Capítulo
- Descripción Capítulo
- Económico
- Relación de Partidas
- Proyecto Ppto Ingresos 2022 V50

Vemos que hay una de ellas que en los datos originales no tiene el mismo nombre en todos los conjuntos de datos “Proyecto Ppto Ingresos 2022 V50”. Por tanto comprobamos que al igual que pasaba en la tabla de gastos tenemos que hacer transformaciones similares



📈Transformación 1 - Tabla Ingresos
 
📌**Objetivo:** Obtener los ingresos de todos los año en columnas diferentes

Nuestra primera transformación va a ser modificar el nombre de la columna para que al combinarlas coja correctamente los valores.

Vamos a revisar paso a paso que es lo que ha hecho sola la herramienta y crearemos un paso más para solventar el problema.

- Paso 1: Origen → Cargar los archivos de la carpeta:
```
= Folder.Files("C:\Users\María\Desktop\MASTER BigData\Visualizacion\powerbi\ingresos")
```

- Paso 2: Archivos ocultos filtrados1 → Filtra y elimina las filas donde el valor de Hidden es true.
```
= Table.SelectRows(Origen, each [Attributes]?[Hidden]? <> true)
```

- Paso 3: Invocar función personalizada1 → Crea una nueva columna en la tabla llamada “Content” que contiene el contenido de los archivos en formato binario.
```
= Table.AddColumn(#"Archivos ocultos filtrados1", "Transformar archivo", each #"Transformar archivo (2)"([Content]))
```

- Paso 4: Columnas con nombre cambiado1 → Renombra una columna de la tabla a “Source.Name”
```
= Table.RenameColumns(#"Invocar función personalizada1", {"Name", "Source.Name"})
```

- Paso 5: Otras columnas quitadas1 → Selecciona un subconjunto de columnas de la tabla, para mantener ciertas columnas y elimina el resto.

```
= Table.SelectColumns(#"Columnas con nombre cambiado1", {"Source.Name", "Transformar archivo"})
```

- Paso 6: Columna de tabla expandida1 → (NUEVO PASO CREADO) Este nuevo paso se encarga de expandir las tablas dentro de la columna "Transformar archivo" y obtener todas las columnas de todos los archivos CSV
```
= Table.ExpandTableColumn(
	#"Otras columnas quitadas1",
	"Transformar archivo",
	List.Distinct(List.Combine(List.Transform(#"Otras columnas quitadas1"[Transformar archivo], each Table.ColumnNames(_))))
)
```

Por tanto ahora vamos tenemos estas columnas:

- Source.Name
- Centro
- Descripción Centro
- Capítulo
- Descripción Capítulo
- Económico
- Relación de Partidas
- Proyecto Ppto Ingresos 2022 V50
- Ingresos_2023_V50
- Proyecto Ppto Ingresos 2024 V50
- Presupuesto 2025

- Paso 7: Tipo cambiado → Ajustamos el tipo de variable
```
= Table.TransformColumnTypes(#"Columna de tabla expandida1",{{"Source.Name", type text}, {"Centro", Int64.Type}, {"Descripcion Centro", type text}, {"Capitulo", Int64.Type}, {"Descripcion Capitulo", type text}, {"Economico", Int64.Type}, {"Relación de partidas", type text}, {"Proyecto Ppto Ingresos 2022 V50", Int64.Type}, {"Ingresos_2023_V50", Int64.Type}, {"Proyecto Ppto Ingresos 2024 V50", Int64.Type}, {"Presupuesto 2025", Int64.Type}})
```


📈Transformación 2 -Tabla Ingresos

📌**Objetivo:** Crear una nueva columna “Ingresos 2022_2023_2024_2025” con los ingresos de las columnas añadidas en el paso 6 y después eliminar las columnas no deseadas

El siguiente paso que vamos a realizar es unificar en una única columna, las cuatro anteriormente indicadas:



Debido a que cuando una de ellas tiene un valor el resto tiene el valor null, esto es debido al combinar las tres tablas en una sola.

- Paso 8: Rename columns →  (NUEVO PASO CREADO)

```
= Table.RenameColumns(#"Tipo cambiado", List.Transform(Table.ColumnNames(#"Tipo cambiado"), each {_, Text.Trim(_)}))
```

- Paso 9: Add column → (NUEVO PASO CREADO) Crea una columna de las cuatro anteriores, Ingresos 2022_2023_2024_2025
```
= Table.AddColumn(#"Rename columns", "Ingresos_2022_2023_2024_2025", each
	List.First(List.RemoveNulls({
    	[Proyecto Ppto Ingresos 2022 V50],
    	[Ingresos_2023_V50],
    	[Proyecto Ppto Ingresos 2024 V50],
    	[Presupuesto 2025]
	}))
)
```

- Paso 10: Delete columns → (NUEVO PASO CREADO)Eliminar el resto de columnas de gatos
```
= Table.RemoveColumns(#"Add column", {
	"Proyecto Presupuesto 2022 V50",
	"Gastos_2023_V50",
	"Proyecto Presupuesto 2024 V50",
	"Proy Presupuesto 2025"
})
```


📈Transformación 3 -Tabla Ingresos

📌**Objetivo:** Crear una nueva columna “Año” con los diferentes años (lo obtenemos de la columna Source.Name)


Además vemos que se ha generado una primera columna donde se indica el nombre del archivo. Esto nos viene bien para poder obtener valores del mismo y saber si la tabla que estamos utilizando es un ingreso o gasto y el año al que corresponde.


Para evitar hacer modificaciones en la tabla original, vamos a crear tablas nuevas donde transformaremos los datos.

Para crear una tabla a partir de la original, hacemos click en la tabla original > Referencia.

- Paso 11: column año → (NUEVO PASO CREADO) Crea una nueva columna “Año” con el año que corresponde

```
= Table.AddColumn(#"Delete columns", "Año", each
	if Text.Contains([Source.Name], "2022") then "2022"
	else if Text.Contains([Source.Name], "2023") then "2023"
	else if Text.Contains([Source.Name], "2024") then "2024"
	else if Text.Contains([Source.Name], "2025") then "2025"
	else null
)
```

📈 Transformación 4 -Tabla Ingresos

📌**Objetivo:** Eliminar valores nulos o vacíos.


El siguiente paso que vamos a realizar es eliminar valores vacíos o nulos.


- Paso 12: Delete Null →  (NUEVO PASO CREADO)

```
= Table.SelectRows(#"Filas filtradas1", each [Ingresos_2022_2023_2024_2025] <> null and [Ingresos_2022_2023_2024_2025] <> "")

= Table.SelectRows(#"Filas filtradas", each [Economico] <> null and [Economico] <> "")

= Table.SelectRows(#"Tipo cambiado1", each ([Descripcion Centro] <> null and [Descripcion Centro] <> ""))
```
Una vez que tenemos los datos agrupados y sin nulos, procedemos a utilizar R para poder transformar y conseguir tablas que se ajusten a lo que se necesite representar:

- Obtener CSV de gastos y otro de ingresos que unicamente contenga Ayuntamiento de Madrid:
```
# Paso 1: Leer tu archivo original
datos_gastos <- read.csv("3.Gastos total.csv", encoding = "UTF-8")
datos_ingresos <- read.csv("4.Ingresos total.csv", encoding = "UTF-8")

# Paso 2: Filtrar por "AYUNTAMIENTO DE MADRID"
ayuntamiento_madrid_gastos <- datos_gastos %>%
  filter(Descripcion.Centro == "AYUNTAMIENTO DE MADRID")

ayuntamiento_madrid_ingresos <- datos_ingresos %>%
  filter(Descripcion.Centro == "AYUNTAMIENTO DE MADRID")

# Paso 3: Exportar a CSV
write.csv(ayuntamiento_madrid_gastos, "ayuntamiento_madrid_gastos.csv", row.names = FALSE)
write.csv(ayuntamiento_madrid_ingresos, "ayuntamiento_madrid_ingresos.csv", row.names = FALSE)
```
- Se ha tenido que pivotar las columnas y concatenar valores de columnas para poder usar los datos correctamente en Flourish:

```
  datos_gastos <- read.csv("ayuntamiento_madrid_gastos.csv", encoding = "UTF-8")
datos_ingreso <- read.csv("ayuntamiento_madrid_ingresos.csv", encoding = "UTF-8")
  # Agrupar y sumar los gastos por Descripcion Seccion y Año

# Pivotar para que cada año sea una columna
gastos_pivot <- datos_gastos %>%
  pivot_wider(names_from = Año, values_from = Gastos, values_fill = 0)
ingresos_pivot <- datos_ingreso %>%
  pivot_wider(names_from = Año, values_from = Ingresos, values_fill = 0)
  
#concatenar 
ingresos_concat <- ingresos_pivot %>%
  mutate(Seccion_Año = paste(Descripcion.Capitulo, Relación.de.partidas, sep = " - "))

# Guardar como CSV
write_csv(gastos_pivot, "gastos_por_seccion_y_ano.csv")
write_csv(ingresos_concat, "ingresos_por_seccion_y_ano.csv")
```


**[20%] Preguntas clave: Detallar las preguntas que la visualización responde y cómo estas se abordan a través del diseño interactivo y analítico.**

[Proyecto en Flourish](https://public.flourish.studio/story/3148434/)

La primera visualización responde a la pregunta: 1.¿Qué años presentan mayor actividad económica total?

> Esta representación, en forma de gráfico de columnas, muestra la evolución anual del total de ingresos y gastos. Se han utilizado diferentes colores para cada año. Podemos comprobar que efectivamente los ingresos y gastos han aumentado progresivamente con el tiempo. El usuario puede pasar el cursor por cada una de las columnas para obtener el valor concreto de gasto o ingreso total por año.

La segunda visualización responde a la pregunta: 2.¿Qué sector es el que presenta mayor ingreso y gasto?

> Esta representación contiene dos gráficos de columnas, la primera muestra el gasto total mientras que en la segunda se muestra el ingreso total. Pudiendo elegir el año para ver como modifica estos valores a lo largo del periodo. Tambien se puede pasar el cursor por cada una de las columnas para obtener el valor concreto de ingreso y gasto acumulado en el año. Se ha seleccionado diferentes colores ara cada sector. Como se puede observar el sector con mayor gasto e ingreso es relativo al Ayuntamiento de Madrid, por tanto en las siguientes visualizacione svamos a analizar en que areas y subsectores se acumula mas gasto e ingreso.

La tercera visualización responde a la pregunta: 3.¿Qué capítulos concentran mayor cantidad de gastos acumulados a lo largo de los años?

> Esta representación (treemap) muestra el reparto total de ingresos por capítulos, sumando todos los años disponibles.
Cada rectángulo representa un capítulo, y su tamaño es proporcional a la suma total de gastos que ha generado. Así se puede identificar fácilmente qué capítulos han aportado más a lo largo del tiempo, y cuáles tienen un peso menor dentro del presupuesto total.

La cuarta visualización responde a la pregunta: 4.¿Qué capítulos concentran mayor cantidad de ingresos acumulados a lo largo de los años?

> Esta representación (treemap) muestra el reparto total de ingresos por capítulos, sumando todos los años disponibles.
Cada rectángulo representa un capítulo, y su tamaño es proporcional a la suma total de ingresos que ha generado. Así se puede identificar fácilmente qué capítulos han aportado más a lo largo del tiempo, y cuáles tienen un peso menor dentro del presupuesto total.

La quinta visualización responde a la pregunta: 5.¿Cómo se distribuyen los gatos en el ayto. de Madrid durante el periodo?

> Esta representación (bar chart race) muestra la distribución de gastos en el ayuntamiento de Madrid a lo largo de 2022 y 2025. Se ha escogido el color rojo para representar el valor de gastos.

La sexta visualización responde a la pregunta: 6¿De dónde provienen los ingresos en el ayto. de Madrid en el periodo?

> Esta representación (bar chart race) muestra la distribución de ingresos en el ayuntamiento de Madrid a lo largo de 2022 y 2025. Se ha escogido el color verde para representar el valor de ingresos. Como se puede observar la mayor parte de los ingresos provienen de transferencias corrientes e impuestos directos.

La séptima visualización responde a la pregunta: 7.Dentro del Ayuntamiento, ¿En que sección se ha gastado más en cada año? ¿Qué relación  de gastos existe entre las diferentes secciones?

> Esta representación (Circles) muestra la distribución de gastados en el ayuntamiento de Madrid pudiendo seleccionar cada año. Con este tipo de representación podemos observa facilmente en que sectores se acumula el mayor gasto en el ayuntamiento de Madrid. Tambien podemos seleccionar un sector para poder ver con mayor precisión cada una de los subsectores. Se ha elegido diferentes colores para cada sector.

La octava visualización responde a la pregunta: 8.Dentro del Ayuntamiento, ¿Qué sección ha generado mayor ingreso? ¿Qué relación de ingresos existe entre las diferentes secciones?

> Esta representación (Circles) muestra la distribución de ingresos en el ayuntamiento de Madrid pudiendo seleccionar cada año. Con este tipo de representación podemos observa facilmente en que sectores se acumula el mayor gasto en el ayuntamiento de Madrid. Tambien podemos seleccionar un sector para poder ver con mayor precisión cada una de los subsectores. Se ha elegido diferentes colores para cada sector.

**[15%] Interactividad: Demostrar los elementos interactivos disponibles, explicando cómo contribuyen a la experiencia del usuario. Incluir reflexiones sobre aspectos de accesibilidad.**

**[10%] Reflexión final: Responder a preguntas como: ¿Qué he aprendido de los datos y de las técnicas empleadas? ¿Qué limitaciones he encontrado? ¿Qué me habría gustado hacer y no pude?**

El video deberá tener una duración de entre 4 y 6 minutos. Respetar este rango de tiempo es esencial, ya que se evaluará tanto la capacidad de síntesis como la calidad del guión.


## Flujo de trabajo

A continucación se muestran el flujo de trabajo realizado para llevar a cabo la práctica:

- **[Ingesta de datos](./visualizacion/vi1.md)**
- **[Transformación de datos](./visualizacion/vi2.md)**
- **[Carga de datos en el modelo](./visualizacion/vi3.md)**
- **[Modelado de datos](./visualizacion/vi3.md)**
- **[Análisis y Visualización](./visualizacion/vi3.md)**



