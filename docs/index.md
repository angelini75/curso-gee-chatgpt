---
title: "Uso de Google Earth Engine asistido por ChatGPT para gestión de Recursos Naturales"
author: "Dr. Marcos E. Angelini"
date: "2024-12-19"
site: bookdown::bookdown_site
documentclass: book
bibliography: [book.bib, packages.bib]
description: |
  Curso práctico sobre el uso de Google Earth Engine (GEE) para la gestión de recursos naturales,
  con la asistencia de ChatGPT para la generación y optimización de scripts en JavaScript.
link-citations: yes
github-repo: https://github.com/angelini75/curso-gee-chatgpt
---

# Introducción

Este curso está diseñado para enseñar el uso de **Google Earth Engine (GEE)**, una plataforma basada en la nube, combinando análisis de teledetección con el poder de la inteligencia artificial a través de **ChatGPT**. 

## Objetivos del Curso

1. Comprender los fundamentos de Google Earth Engine.
2. Aprender los conceptos básicos de programación en JavaScript.
3. Realizar análisis avanzados como:
   - Detección de cambios (inundaciones, incendios).
   - Clasificación supervisada.
   - Análisis de fenómenos estacionales.
   - Interpolación utilizando Random Forest.
4. Utilizar ChatGPT para:
   - Generar y corregir scripts en GEE.
   - Resolver problemas comunes en teledetección.

## Estructura del Curso

El curso está dividido en los siguientes capítulos:
- **Introducción a Google Earth Engine y ChatGPT.**
- **Fundamentos de programación en JavaScript.**
- **Ingeniería de Prompts con ChatGPT.**
- **Aplicaciones prácticas de GEE: detección de cambios, clasificación supervisada, y más.**

Esperamos que este curso te proporcione las herramientas necesarias para integrar GEE y ChatGPT en tus proyectos de análisis geoespacial.

## Cómo Renderizar el Libro

Para renderizar este libro:
1. Ve al panel **Build** en RStudio y selecciona **Build Book**.
2. Alternativamente, desde la consola de R ejecuta:
   
   ``` r
   bookdown::render_book()
   ```
