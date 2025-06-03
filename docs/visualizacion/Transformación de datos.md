# Transformación de datos


## ℹ️ Definición de la técnica de visualización utilizada 
##### Tipo de visualización
En esta fase los datos pasan por diferentes transformaciones para que puedan ser utilizados de forma correcta.

En el proceso de transformación se puede realizar diferentes pasos: eliminación/filtrado de columnas, cambiar tipo de datos, combinación de tablas, agregar columnas personalizadas…

Para realizar la transformación de los datos tenemos que acceder a Inicio> Transformar Datos.


## ℹ️ Transformaciones en Tabla Gastos


Una vez ingestados veremos que se nos han creado unas tablas con las diferentes columnas. En la primera fila se encuentran cada una de las variables y en el resto sus valores.

Columnas creadas:

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
- Relación de Partidas
- Proyecto Presupuesto 2022 V50

Vemos que hay una de ellas que en los datos originales no tiene el mismo nombre en todos los conjuntos de datos “Proyecto Presupuesto 2022 V50”. Por tanto comprobamos que en este columna para los csv no usados de ejemplo “Gastos_Proyecto_2023.csv”, “V50_Gastos_Proyecto_2024.csv” y “V50_Gastos_Proyecto_2025.csv” todos los valores son null.


📉#Transformación 1 - Tabla Gastos

| 📌 Objetivo                                                 |
|---------------------------------------------------------------------|
| Obtener los gastos de todos los año en columnas diferentes. |


Nuestra primera transformación va a ser modificar el nombre de la columna para que al combinarlas coja correctamente los valores.

Vemos que PowerBI ha realizado los siguientes pasos para combinar los tres archivos:



Vamos a revisar paso a paso que es lo que ha hecho sola la herramienta y crearemos un paso más para solventar el problema.

Paso 1: Origen → Cargar los archivos de la carpeta:
```
= Folder.Files("C:\Users\María\Desktop\MASTER BigData\Visualizacion\powerbi\Gastos")
```

Paso 2: Archivos ocultos filtrados1 → Filtra y elimina las filas donde el valor de Hidden es true.
```
= Table.SelectRows(Origen, each [Attributes]?[Hidden]? <> true)
```

Paso 3: Invocar función personalizada1 → Crea una nueva columna en la tabla llamada “Content” que contiene el contenido de los archivos en formato binario.
```
= Table.AddColumn(#"Archivos ocultos filtrados1", "Transformar archivo", each #"Transformar archivo (2)"([Content]))
```

Paso 4: Columnas con nombre cambiado1 → Renombra una columna de la tabla a “Source.Name”
```
= Table.RenameColumns(#"Invocar función personalizada1", {"Name", "Source.Name"})
```

Paso 5: Otras columnas quitadas1 → Selecciona un subconjunto de columnas de la tabla, para mantener ciertas columnas y elimina el resto.

```
= Table.SelectColumns(#"Columnas con nombre cambiado1", {"Source.Name", "Transformar archivo"})
```

Paso 6: Columna de tabla expandida1 → (NUEVO PASO CREADO) Este nuevo paso se encarga de expandir las tablas dentro de la columna "Transformar archivo" y obtener todas las columnas de todos los archivos CSV
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

Paso 7: Tipo cambiado → Ajustamos el tipo de variable
```
= Table.TransformColumnTypes(#"Columna de tabla expandida1",{{"Source.Name", type text}, {"Centro", Int64.Type}, {"Descripcion Centro", type text}, {"Seccion", Int64.Type}, {"Descripcion Seccion", type text}, {"Programa", Int64.Type}, {"Descripcion Programa", type text}, {"Capitulo", Int64.Type}, {"Descripcion Capitulo", type text}, {"Economico", Int64.Type}, {"Relación de partidas", type text}, {"Proyecto Presupuesto 2022 V50", Int64.Type}, {" Proyecto Presupuesto 2024 V50 ", Int64.Type}, {"Gastos_2023_V50", Int64.Type}, {"Proy Presupuesto 2025", Int64.Type}})
```


📉Transformación 2 -Tabla Gastos


Objetivo: Crear una nueva columna “Gastos 2022_2023_2024_2025” con los gastos de las columnas añadidas en el paso 6 y después eliminar las columnas no deseadas


El siguiente paso que vamos a realizar es unificar en una única columna, las cuatro anteriormente indicadas:



Debido a que cuando una de ellas tiene un valor el resto tiene el valor null, esto es debido al combinar las tres tablas en una sola.

Paso 8: Rename columns →  (NUEVO PASO CREADO)


= Table.RenameColumns(#"Tipo cambiado", List.Transform(Table.ColumnNames(#"Tipo cambiado"), each {_, Text.Trim(_)}))


Paso 9: Add column → (NUEVO PASO CREADO) Crea una columna de las cuatro anteriores, Gastos_2022_2023_2024_2025
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

Paso 10: Add column → (NUEVO PASO CREADO)Eliminar el resto de columnas de gatos
```
= Table.RemoveColumns(#"Add column", {
	"Proyecto Presupuesto 2022 V50",
	"Gastos_2023_V50",
	"Proyecto Presupuesto 2024 V50",
	"Proy Presupuesto 2025"
})
```



📉 Transformación 3 -Tabla Gastos


Objetivo: Crear una nueva columna “Año” con los diferentes años (lo obtenemos de la columna Source.Name)



Además vemos que se ha generado una primera columna donde se indica el nombre del archivo. Esto nos viene bien para poder obtener valores del mismo y saber si la tabla que estamos utilizando es un ingreso o gasto y el año al que corresponde.


Para evitar hacer modificaciones en la tabla original, vamos a crear tablas nuevas donde transformaremos los datos.

Para crear una tabla a partir de la original, hacemos click en la tabla original > Referencia.

Paso 11: column año → (NUEVO PASO CREADO) Crea una nueva columna “Año” con el año que corresponde

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


Objetivo: Eliminar valores nulos o vacíos.


El siguiente paso que vamos a realizar es eliminar valores vacíos o nulos.


Paso 12: Delete Null →  (NUEVO PASO CREADO)

```
= Table.SelectRows(#"Filas filtradas", each [Gastos_2022_2023_2024_2025] <> null and [Gastos_2022_2023_2024_2025] <> "")

= Table.SelectRows(#"Filas filtradas", each [Economico] <> null and [Economico] <> "")

= Table.SelectRows(#"Tipo cambiado1", each [Descripcion Centro] <> null and [Descripcion Centro] <> "")
```

