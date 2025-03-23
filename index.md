# Inicio

:blue_book: Asignatura: **Visualización de Datos**

:fontawesome-solid-user: Alumno: **Maria López Pérez**

:material-calendar: Fecha: **23/04/25**

Este informe documenta la entrega del Caso Práctico 2 de la asignatura DevOps & Cloud del programa avanzado DevOps de la UNIR. El contenido del informe se estructura en las siguientes secciones:

    Objetivo: Descripción de los componentes desplegados y su configuración.
    Desarrollo: Ejecución práctica de la infraestructura y su configuración.
    Evidencias: Recopilación de pruebas de funcionamiento y validaciones.
    Licencia: Definición del marco legal de uso.
    Referencias: Fuentes utilizadas en el desarrollo del ejercicio.

Para la generación del informe, se ha utilizado MkDocs, una librería de Python para la creación de documentación técnica (MkDocs, s.f.), junto con el plugin WithPDF, que permite la exportación a formato PDF (WithPDF, s.f.). Esta elección responde a la naturaleza del caso práctico, en el que una de las tareas consiste en desplegar una imagen estática de una web en Nginx sin persistencia. Dado que MkDocs genera HTML estático, se ha integrado su uso dentro del ejercicio para la documentación y su despliegue.

[:octicons-browser-16: Ir a la versión online](https://charlstown.github.io/unir-cp2){ .md-button }

## Introducción

Este repositorio contiene la solución del **Caso Práctico 2**, en el cual se ha desplegado una infraestructura en **Microsoft Azure** de forma automatizada utilizando **Terraform** y **Ansible**. Se incluyen configuraciones para la creación de recursos en la nube, instalación de servicios y despliegue de aplicaciones en contenedores con almacenamiento persistente.

![diagrama enunciado](./assets/images/diagrama-enunciado.png)

## Objetivos

- Crear infraestructura de forma automatizada en un proveedor de Cloud pública.
- Utilizar herramientas de gestión de la configuración para automatizar la instalación y configuración de servicios.
- Desplegar mediante un enfoque totalmente automatizado aplicaciones en forma de contenedor sobre el sistema operativo.
- Desplegar mediante un enfoque totalmente automatizado aplicaciones que hagan uso de almacenamiento persistente sobre una plataforma de orquestación de contenedores.
