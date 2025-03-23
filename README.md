# 🚀 UOC - Visualizacion de Datos PEC2

Este repositorio contiene la solución del **PEC 2**, en el cual se presentan tres tipos de visualizaciones de datos usando técnicas diferentes  **Microsoft Azure** de forma automatizada utilizando **Terraform** y **Ansible**. Se incluyen configuraciones para la creación de recursos en la nube, instalación de servicios y despliegue de aplicaciones en contenedores con almacenamiento persistente.

## 🎯 Objetivos

- Identificar y analizar qué conjuntos de datos son los más apropiados para cada técnica de visualizacion.
- Crear una página donde se presenten las 3 visualizaciones.
- Generar un video de 7-8 minutos en total donde se detallen los siguientes puntos de cada visualización:
        - Presentación.
        - Indicar donde están publicadas las visualizaciones.  
        - Definir cada técnica de visualización (nombre, origen, descripción/funcionamiento, ejemplos de aplicación...)
        - Describir el tipo de datos que se pueden representar con cada técnica ¿(datos cuantitativos, cualitativos? ¿Qué estructura tienen  que tener para cada técnica?).
        - Explicar las limitaciones en cuanto a datos (¿hay medida mínima y máxima del juego de datos para cada técnica?)
        - Explicar brevemente cada visualización realizada.
        - Explicar que se pretende comunicar o descubrir con la visualización y cómo la técnica y los datos seleccionados ayudan a lograr ese objetivo.

Las tres técnicas de visualización son:
  - TÉCNICA GRUPO I (Básicas y populares): Diagrama de dispersión o scatterplot
  - TÉCNICA GRUPO II (Habituales y específicas): Box plot
  - TÉCNICA GRUPO III (Menos habituales o específicas): Isotype & Unit charts


## 📁 Estructura del repositorio

El proyecto se organiza en tres grandes bloques: infraestructura, despliegue y documentación. A continuación se resume su estructura principal:

```
📦 repo-root
├── terraform/        # Código para el despliegue de la infraestructura (ACR, VM, AKS)
├── ansible/          # Playbooks y roles para configurar la VM y desplegar en AKS
├── docs/             # Documentación del proyecto (MkDocs)
├── site/             # Sitio estático generado de la documentación
├── setup.sh          # Script para exportar variables tras despliegue
├── mkdocs.yml        # Configuración de MkDocs
├── Dockerfile.docs   # Dockerfile para generar la imagen de documentación
├── requirements.txt  # Dependencias de Python
├── README.md         # Descripción general del proyecto
└── LICENSE           # Licencia del repositorio
```

## ⚙️ Tecnologías utilizadas

- **Terraform**: Creación de infraestructura en Azure (ACR, VM, AKS).
- **Ansible**: Configuración automática de servicios y despliegue de aplicaciones.
- **Podman**: Contenedorización de aplicaciones en la VM.
- **Kubernetes (AKS)**: Orquestación de aplicaciones con almacenamiento persistente.

---

📌 **Autor**: *[@mloperez](https://github.com/mloperez)*  
📌 **Fecha**: *23-03-2025*
