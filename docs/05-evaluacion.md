# Evaluación práctica: Análisis multitemporal para detectar inundaciones en La Plata (2013)

## Objetivo:
Los estudiantes deben realizar un análisis multitemporal en **Google Earth Engine (GEE)** para identificar las áreas afectadas por las inundaciones en La Plata durante abril de 2013, utilizando imágenes satelitales y técnicas de teledetección.

https://es.wikipedia.org/wiki/Inundaci%C3%B3n_en_La_Plata_de_2013

---

```{=html}
<iframe width="100%" height="400"
  src="https://es.wikipedia.org/wiki/Inundaci%C3%B3n_en_La_Plata_de_2013"
  frameborder="0" allow="autoplay; encrypted-media"
  allowfullscreen></iframe>
```
---

## Requisitos para la entrega:
1. **Script en GEE**: Los estudiantes deben entregar el script que implementaron en GEE, asegurándose de comentar cada línea para explicar su función.
2. **Resultados visuales**: Incluya capturas de pantalla del mapa generado que muestre las áreas afectadas por las inundaciones.
3. **Informe breve**: Explica los resultados obtenidos, incluyendo las limitaciones y posibles mejoras del análisis.


## Instrucciones:
1. **Definir la región de interés (ROI)**  
   - Define la región correspondiente a La Plata y sus alrededores, por ejemplo usando la colección de límites administrativos o bien a partir de un polígono.
   - Visualiza la región en el mapa para verificar que está correctamente delimitada.

2. **Seleccionar las imágenes satelitales**  
   - Usa la colección de imágenes disponible que mejor se adecue al evento (Landsat, MODIS, etc.).
   - Filtra las imágenes para dos períodos: 
     - Antes del evento (marzo 2013).
     - Durante o inmediatamente después del evento (abril 2013).

3. **Preprocesamiento**  
   - Aplica filtros de nubosidad y recorta las imágenes a la región de interés.
   - Realiza las correcciones atmosféricas o utiliza índices relevantes para reducir ruido.

4. **Calcular índices**  
   - Calcula índices relevantes como el **NDWI** (Índice de Agua Diferenciado Normalizado) o el **NDVI**, según el tipo de imagen satelital.
   - Analiza los cambios en los índices entre los períodos pre y post-inundación.

5. **Generar una máscara de áreas inundadas**  
   - Usa un umbral en el índice calculado (por ejemplo, NDWI > 0.2) para identificar áreas afectadas por agua acumulada.
   - Excluye áreas que podrían generar falsos positivos, como cuerpos de agua permanentes.

6. **Calcular la superficie afectada**  
   - Calcula la superficie total de las áreas inundadas (en hectáreas) utilizando la función `reduceRegion`.

7. **Visualizar y exportar los resultados**  
   - Visualiza las áreas inundadas en el mapa con una paleta de colores distintiva.
   - Exporta los resultados (imágenes procesadas o shapefiles) a Google Drive o al sistema local.

---

## Criterios de evaluación:
- **Corrección del código** (40%): Uso adecuado de las funciones de GEE y estructura lógica del script.
- **Interpretación de resultados** (30%): Calidad de las visualizaciones y explicación de los resultados.
- **Creatividad y análisis crítico** (20%): Identificación de limitaciones y propuestas de mejora.
- **Presentación** (10%): Claridad en los comentarios del script, capturas y organización del informe.

