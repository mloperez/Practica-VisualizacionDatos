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

#[20%] Presentación en vivo: Mostrar las características de la visualización mientras se navega por ella, destacando aspectos clave del diseño y la funcionalidad

**[15%] Conjunto de datos: Describir brevemente las características más relevantes del conjunto de datos utilizado, su origen y cualquier proceso de preparación realizado.**


Se ha elegido la herramienta PowerBI para el análisis de los datos y se ha utilizado DAX y R para el tratamiento de los datos.

Datos seleccionados:

    Presupuesto general 2024
    Presupuestos. Proyectos de Presupuesto de ejercicios anteriores - Conjunto de datos - datos.gob.es

En primer lugar debemos ingestar los diferentes conjuntos de datos en PowerBI Desktop.



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
    
Para la ingesta de los datos en PowerBI, vamos a Inicio > Obtener Datos > Carpeta. Seleccionamos las carpetas donde se encuentran nuestros conjuntos de datos. Y seleccionamos --> Combinar y Transformar Datos

Para combinar lo datos PowerBI toma de ejemplo el primer archivo en este caso → Gastos_Proyecto_2022.csv y Ingresos_Proyecto_2022.csv
He estructurado el proyecto de forma clara y coherente. En primer lugar, presento los datos utilizados y explico brevemente su origen y estructura: cada fila representa un registro económico con un centro, año, tipo (ingreso o gasto) e importe.



**[20%] Preguntas clave: Detallar las preguntas que la visualización responde y cómo estas se abordan a través del diseño interactivo y analítico.**

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



