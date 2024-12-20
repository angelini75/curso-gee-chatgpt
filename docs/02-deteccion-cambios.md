# Análisis multitemporal para la detección de cambios

El análisis multitemporal en Google Earth Engine (GEE) permite estudiar cómo evolucionan las características de una región a lo largo del tiempo utilizando imágenes satelitales capturadas en diferentes fechas. Esta técnica es fundamental para monitorear fenómenos como la deforestación, el avance urbano, los incendios forestales o las inundaciones. Al integrar este tipo de análisis en GEE, los usuarios pueden automatizar procesos y manejar grandes volúmenes de datos satelitales de forma eficiente.

A continuación, se describen los pasos esenciales para realizar un análisis multitemporal, integrando tanto la teoría subyacente como la práctica para que puedas aplicarlos de forma efectiva.

---

## Pasos para el análisis multitemporal

### 1. Definir la región de interés (ROI)

El primer paso para cualquier análisis geoespacial es definir la región de interés (ROI, por sus siglas en inglés). Esta región establece el área geográfica donde se concentrará el análisis y delimita el espacio que se analizará en cada imagen satelital. Definir la ROI correctamente es esencial para optimizar el rendimiento computacional, ya que permite reducir el volumen de datos procesados.

Para definir la ROI, puedes optar por distintas estrategias. Por un lado, puedes dibujar la región directamente en el editor de GEE utilizando las herramientas de dibujo (polígonos, puntos o rectángulos). Por otro lado, si ya cuentas con archivos de formato Shapefile o GeoJSON, puedes importarlos y usarlos como referencia para la región de estudio. Las coordenadas también se pueden definir manualmente si tienes puntos específicos en mente.

Desde el punto de vista teórico, la ROI establece los límites espaciales del análisis, lo que significa que solo los píxeles dentro de esta región serán procesados. Esto mejora la eficiencia computacional y permite focalizar los recursos de procesamiento en el área relevante.


### 2. Seleccionar las colecciones de imágenes adecuadas

Una vez que se ha definido la región, se deben seleccionar las colecciones de imágenes satelitales adecuadas. Las imágenes deben cubrir el período de tiempo que se desea analizar y, además, deben ser apropiadas para los objetivos del análisis. Los conjuntos de datos más utilizados en GEE incluyen las colecciones de Landsat, Sentinel-2 y MODIS.

La elección de la colección de imágenes depende del fenómeno a estudiar. Por ejemplo, para la detección de cambios en la vegetación, el NDVI (Índice de Vegetación de Diferencia Normalizada) suele calcularse a partir de las bandas de infrarrojo cercano y rojo, que están presentes tanto en Landsat como en Sentinel. Si se busca mayor resolución temporal, se prefiere Sentinel-2, ya que ofrece imágenes cada 5 días, mientras que Landsat solo captura imágenes cada 16 días.

Desde una perspectiva teórica, la disponibilidad de una amplia colección de imágenes garantiza la posibilidad de realizar un análisis preciso. También es fundamental considerar la cobertura de nubes de la colección seleccionada, ya que la nubosidad puede dificultar la observación de la superficie terrestre.

### 3. Aplicar filtros temporales y espaciales

Con la colección de imágenes seleccionada, se deben aplicar filtros para reducir el volumen de imágenes a las fechas y áreas de interés. Este proceso implica dos acciones clave: filtrar por rango de fechas y por región de interés.

El filtro de fechas permite seleccionar imágenes dentro de un rango temporal específico. Este paso es esencial para realizar comparaciones antes y después de eventos como incendios o inundaciones. Por ejemplo, si se desea estudiar la deforestación entre 2018 y 2022, se puede aplicar un filtro de fechas que permita extraer solo las imágenes de esos años.

El filtro espacial asegura que solo se utilicen imágenes que intersecten la región de interés (ROI). De esta forma, se evitan imágenes innecesarias de regiones distantes que no aportan valor al análisis. Esta etapa es clave para reducir el tamaño de los datos y acelerar el procesamiento.

Teóricamente, los filtros temporales y espaciales garantizan que solo se procesen los datos que realmente importan. Además, estos filtros reducen la carga de procesamiento computacional, permitiendo una ejecución más eficiente y rápida.

### 4. Preprocesamiento de las imágenes

El preprocesamiento de imágenes es esencial para asegurar la calidad y precisión de los datos antes de aplicar cualquier tipo de análisis. Este paso permite corregir posibles errores o distorsiones en las imágenes satelitales, asegurando que los resultados no estén contaminados por elementos indeseados.

El preprocesamiento puede incluir la corrección atmosférica, que se utiliza para eliminar los efectos de la atmósfera (como neblina o aerosoles) en la reflectancia de la superficie. Este paso es crucial para realizar comparaciones multitemporales, ya que las variaciones en la atmósfera pueden hacer que una imagen parezca diferente a otra, incluso si no ha habido ningún cambio real en la superficie.

Otra tarea importante del preprocesamiento es la eliminación de nubes y sombras. Las nubes pueden bloquear la vista de la superficie terrestre, mientras que las sombras proyectadas por estas nubes pueden introducir errores en los análisis. Las imágenes de las colecciones Sentinel y Landsat suelen incluir máscaras de nubes que permiten ocultarlas automáticamente.

### 5. Calcular índices o métricas relevantes

Para visualizar y cuantificar los cambios en la superficie terrestre, es común calcular índices o métricas que resuman la información contenida en las bandas espectrales. Los índices de vegetación, agua o suelo son los más utilizados en teledetección.

El NDVI (Índice de Vegetación de Diferencia Normalizada) es uno de los índices más comunes. Se calcula combinando la banda de infrarrojo cercano (NIR) y la banda roja (Red), y permite detectar la presencia de vegetación viva. Este índice varía entre -1 y 1, donde valores altos indican vegetación densa y valores bajos representan suelos desnudos o cuerpos de agua.

Otros índices relevantes incluyen el NDWI (índice de agua) y el NDSI (índice de nieve). Cada uno de estos índices resalta características específicas de la superficie, lo que facilita la identificación de cambios a lo largo del tiempo.

### 6. Generar composiciones temporales

La creación de composiciones temporales permite observar los cambios visualmente. Estas composiciones se pueden realizar asignando diferentes fechas a cada canal de color (rojo, verde y azul) para representar de forma gráfica los cambios entre imágenes. Por ejemplo, se puede asignar una imagen de enero a la banda roja, una de mayo a la banda verde y una de septiembre a la banda azul.

Esta técnica permite detectar cambios fácilmente, ya que las diferencias de color reflejan la variación en la cobertura del suelo. Si la vegetación ha desaparecido entre enero y septiembre, la banda verde perderá intensidad, mientras que los otros canales se mantendrán constantes.

Desde una perspectiva teórica, esta técnica permite representar el cambio de forma intuitiva y visual, facilitando la identificación de áreas donde se han producido alteraciones significativas.

### 7. Analizar y visualizar los resultados

En esta etapa, se analizan los resultados obtenidos y se visualizan de forma clara e interpretativa. Los cambios pueden representarse con mapas temáticos que indiquen, por ejemplo, la pérdida de cobertura forestal o la expansión de áreas urbanas.

Las gráficas de series temporales son otra forma de visualizar los cambios. Estas gráficas permiten observar la evolución de un índice (por ejemplo, NDVI) a lo largo del tiempo, destacando puntos de inflexión, como incendios o inundaciones.

Visualizar los resultados no solo permite identificar cambios, sino que también facilita la comunicación de los hallazgos. Los mapas temáticos y las gráficas son herramientas de comunicación visual esenciales en informes técnicos y presentaciones.

### 8. Validación y verificación

Para garantizar que los resultados sean precisos y reproducibles, se deben validar y verificar los hallazgos. Este paso implica la comparación de los resultados con fuentes externas o datos de campo. Si se está evaluando la deforestación, se pueden utilizar imágenes de mayor resolución espacial o información obtenida de inspecciones de campo.

La validación es fundamental, ya que permite corregir errores que pueden surgir por la presencia de nubes, sombras o variaciones en la reflectancia. Este paso garantiza que los resultados finales sean precisos y confiables.



## Análisis multitemporal de incendios en Córdoba (2020) usando ChatGPT y Google Earth Engine

---

```{=html}
<iframe src="https://es.wikipedia.org/wiki/Incendios_forestales_de_C%C3%B3rdoba_de_2020" 
        width="100%" 
        height="600px" 
        frameborder="0" 
        allowfullscreen>
</iframe>
```

---

En esta sección, aprenderemos a utilizar ChatGPT como asistente para desarrollar un análisis multitemporal en Google Earth Engine (GEE). El objetivo es identificar y delimitar las áreas quemadas durante los incendios forestales de Córdoba en 2020. Usaremos imágenes de la colección MODIS, que tiene una alta frecuencia temporal y permite detectar rápidamente cambios de cobertura en grandes áreas.

El análisis se enfocará en tres tareas principales:

1. Identificación de los incendios utilizando índices de vegetación como el NDVI.
2. Creación de una máscara de incendios para delimitar las áreas afectadas.
3. Cálculo de la superficie quemada dentro de la región de interés.

---

### Objetivo general
El objetivo es guiar al usuario para que desarrolle su propio script en GEE con la asistencia de ChatGPT. Para ello, utilizaremos prompts cuidadosamente diseñados para que ChatGPT genere el código y explique los pasos.

---

### Instrucciones generales para los estudiantes

1. Usar ChatGPT de forma activa: Durante la práctica, se te proporcionarán "Prompts de ejemplo" que deberás copiar y pegar en ChatGPT. Observa la respuesta generada y, si es necesario, mejora el prompt para obtener una respuesta más precisa.

2. Construir el script paso a paso: No recibirás todo el código completo desde el inicio. Trabajarás en fragmentos de código que se irán construyendo poco a poco.

3. Responder preguntas de evaluación: Al final, se te harán preguntas para verificar tu comprensión de los conceptos.

---

Aquí tienes un prompt detallado y completo para definir el caso de estudio y el objetivo del análisis para ChatGPT. Este prompt está diseñado para que ChatGPT comprenda completamente el contexto, la tarea específica, los pasos a seguir y el formato de los resultados esperados. Este prompt se puede utilizar directamente en ChatGPT para obtener respuestas precisas y personalizadas para el análisis multitemporal.

---

### Prompt inicial para ChatGPT

```
Actúa como un experto en Google Earth Engine (GEE) y teledetección. Necesito realizar un análisis multitemporal para identificar las áreas afectadas por los incendios forestales que ocurrieron en la provincia de Córdoba, Argentina, entre julio y noviembre de 2020. Este análisis se llevará a cabo paso a paso y tu tarea será proporcionar código parcial y explicaciones breves en cada paso, no el código completo de una sola vez.

### Contexto general
1. Ubicación: La región de interés (ROI) es la provincia de Córdoba, Argentina, que fue gravemente afectada por incendios forestales en 2020.
2. Fechas de análisis: Necesito imágenes de dos periodos clave:
   - Imagen previa a los incendios: Junio de 2020 (antes del inicio de los incendios).
   - Imagen posterior a los incendios: Noviembre de 2020 (cuando los incendios ya habían finalizado).
3. Fuente de datos: Usaremos la colección de imágenes satelitales de MODIS (MOD09GA) debido a su alta frecuencia de captura.
4. Objetivo: Identificar y cuantificar la superficie quemada mediante el cálculo del índice de quemadura normalizada (NBR) y la diferencia de NBR (dNBR) entre las dos fechas.
5. Indicadores clave: 
   - NBR: Índice de quemadura normalizada, calculado a partir de las bandas NIR y SWIR (para MODIS, las bandas 2 y 7, respectivamente).
   - dNBR: Diferencia entre el NBR antes y después del incendio.
   - Superficie quemada: Se consideran quemadas las áreas donde dNBR > 0.66.

---

### Flujo de trabajo propuesto
El análisis se realizará paso a paso y en cada paso te solicitaré que generes un fragmento de código parcial y comentado para completar la tarea. Los pasos son los siguientes:
1. Definir la región de interés (ROI): Proporciona el código para obtener la geometría de la provincia de Córdoba (Argentina) a partir de la colección FAO/GAUL.
2. Seleccionar imágenes MODIS antes y después de los incendios: Proporciona el código para seleccionar las imágenes MODIS de junio y noviembre de 2020, aplicando los filtros de región y fechas.
3. Calcular el índice NBR antes y después del incendio: Proporciona el código para calcular el NBR para las imágenes antes y después del incendio.
4. Calcular la diferencia de NBR (dNBR): Proporciona el código para calcular la diferencia de NBR (dNBR) y resaltar las áreas quemadas.
5. Crear la máscara de áreas quemadas: Proporciona el código para generar una máscara binaria que resalte las áreas donde dNBR > 0.66.
6. Calcular la superficie total quemada: Proporciona el código para calcular la superficie total quemada (en hectáreas) utilizando la función reduceRegion.
7. Visualizar los resultados: Proporciona el código para visualizar las capas de NBR, dNBR y la máscara de áreas quemadas en el mapa.
8. Exportar los resultados: Proporciona el código para exportar la imagen de las áreas quemadas a Google Drive.

---

### Instrucciones adicionales
- Proporcióname el código para un solo paso a la vez, y asegúrate de explicar cada línea del código.
- No me proporciones todo el código de una sola vez. Quiero avanzar paso a paso para comprender cada parte.
- Usa comentarios en cada línea de código para explicar el propósito de cada operación.
- Al final de cada paso, indícame si hay alguna recomendación o buena práctica para optimizar el análisis.
- Proporciona sugerencias para depurar o corregir errores si algo no funciona según lo esperado.

---

Para comenzar, vamos a realizar el Paso 1: Definir la región de interés (ROI). Proporciona el fragmento de código para definir la región de Córdoba, Argentina, usando la colección FAO/GAUL y explica cada línea del código.
```

---

#### Explicación del Prompt

1. Contexto inicial:  
   Este prompt establece claramente la región de interés, la fuente de datos y los objetivos del análisis. Esto asegura que ChatGPT comprenda el contexto y la tarea principal desde el inicio.

2. Estructura de los pasos:  
   Se enumeran los pasos específicos, pero se le dice explícitamente a ChatGPT que debe entregar un solo paso a la vez. Este enfoque asegura que el usuario tenga control sobre la secuencia de instrucciones.

3. Instrucciones claras:  
   Se pide que el código esté comentado y explicado línea por línea, facilitando la comprensión del usuario.  
   Se prohíbe explícitamente que ChatGPT entregue todo el código de una vez, con la intención de que el usuario aprenda y pueda reflexionar sobre cada parte antes de avanzar.

---

#### Resultado del prompt
```javascript
// Paso 1: Definir la región de interés (ROI)

// 1. Cargar la colección de límites administrativos GAUL de FAO
var gaulCollection = ee.FeatureCollection('FAO/GAUL/2015/level1');

// 2. Filtrar la colección para seleccionar solo las características (regiones) de Argentina
var argentina = gaulCollection.filter(ee.Filter.eq('ADM0_NAME', 'Argentina'));

// 3. Filtrar la región de interés para obtener solo la provincia de Córdoba
var cordoba = argentina.filter(ee.Filter.eq('ADM1_NAME', 'Córdoba'));

// 4. Visualizar la región de Córdoba en el mapa para verificar que la geometría esté correcta
Map.centerObject(cordoba, 8); // Centrar el mapa en Córdoba con un nivel de zoom de 8
Map.addLayer(cordoba, {color: 'red'}, 'Provincia de Córdoba'); // Añadir la capa de Córdoba al mapa
```
> Identifica el problema en el código y corrige el prompt si es necesario

### Paso 1: Definir la región de interés (ROI), siguiendo la metodología paso a paso.


#### Prompt para ChatGPT - Paso 1

```
Para comenzar con el análisis, necesito definir la región de interés (ROI) correspondiente a la provincia de Córdoba, Argentina. Usa la colección de FAO/GAUL para obtener la geometría de Córdoba y proporciona el código paso a paso. Explica cada línea de código y agrega comentarios dentro del código para facilitar la comprensión.
```
> Copia el resultado del prompt y pegalo en GEE. Luego dale RUN al script. Evalua los resultados.

#### Respuesta esperada de ChatGPT
```javascript
// Paso 1: Definir la región de interés (ROI)

// 1. Cargar la colección de límites administrativos GAUL de FAO (nivel 1 - provincias/estados)
var gaulCollection = ee.FeatureCollection('FAO/GAUL/2015/level1');

// 2. Filtrar la colección para seleccionar solo las entidades correspondientes a Argentina
var argentina = gaulCollection.filter(ee.Filter.eq('ADM0_NAME', 'Argentina'));

// 3. Filtrar la región de interés para obtener solo la provincia de Cordoba (sin tilde)
var cordoba = argentina.filter(ee.Filter.eq('ADM1_NAME', 'Cordoba'));

// 4. Visualizar la región de Córdoba en el mapa para verificar la geometría
Map.centerObject(cordoba, 8); // Centrar el mapa en Córdoba con un nivel de zoom de 8
Map.addLayer(cordoba, {color: 'red'}, 'Provincia de Córdoba'); // Añadir la capa de Córdoba al mapa en color rojo

// 5. Usar la función print() para mostrar la información de la variable gaulCollection
print('Colección de límites administrativos GAUL (Argentina):', argentina);

// 6. Usar la función print() para mostrar la información de la geometría de Córdoba

```

Explicación esperada:  
- Se usa la colección FAO/GAUL/2015/level1 para obtener la geometría de Córdoba.  
- Se aplica un filtro para seleccionar la provincia de Córdoba.  
- Se usa Map.centerObject y Map.addLayer para centrar la vista en la ROI y visualizarla en rojo.  
- Observa que en la Consola (Console) aparece la siguiente informacion como respuesta a la función print.
```
Colección de límites administrativos GAUL (Argentina):
FeatureCollection FAO/GAUL/2015/level1 (24 elements, 11 columns)
type: FeatureCollection
id: FAO/GAUL/2015/level1
version: 1701682593235039
columns: Object (11 properties)
features: List (24 elements)
properties: Object (1 property)
```

Puedes usar esta información en ChatGPT para que te explique en qué consiste este FeatureCollection

### Paso 2: Seleccionar imágenes MODIS antes y después de los incendios

Este paso se enfoca en la obtención de las imágenes satelitales MODIS necesarias para el análisis. Se seleccionarán imágenes antes y después de los incendios forestales de Córdoba, con fechas clave de junio de 2020 (antes) y noviembre de 2020 (después). Las imágenes se filtrarán por fecha y por la región de interés (ROI) previamente definida. Además, se calculará la **mediana de las imágenes** para reducir el ruido en los datos.


```
Necesito seleccionar imágenes MODIS de la colección MODIS/061/MCD43A4 para analizar incendios en Córdoba, Argentina, en 2020. Sin embargo, el área procesada y visualizada debe limitarse estrictamente al ROI definido (provincia de Córdoba). Proporciona el código para filtrar las fechas y recortar las imágenes seleccionadas al ROI utilizando la función `clip`.
1. Usa las fechas del 1 al 16 de junio de 2020 (antes del incendio) y del 16 al 30 de noviembre de 2020 (después del incendio).
2. Aplica un recorte explícito de las imágenes al ROI después de seleccionarlas y procesarlas.
3. Proporciona el código comentado línea por línea para que pueda entender el propósito de cada operación.
4. Visualiza las imágenes recortadas al ROI y verifica si están limitadas correctamente.
```

> Acción del estudiante: Copia el prompt en ChatGPT, observa la respuesta y ejecuta el código en GEE. Asegúrate de comprender cada paso antes de avanzar.

---

#### Respuesta esperada de ChatGPT
```javascript
// Paso 2: Selección de imágenes MODIS y recorte al ROI

// 1. Cargar la colección de imágenes MODIS MCD43A4
var modisCollection = ee.ImageCollection('MODIS/061/MCD43A4');

// 2. Definir las fechas de interés
var preFireStart = '2020-06-01'; // Fecha de inicio para la imagen previa al incendio
var preFireEnd = '2020-06-16';   // Fecha de fin para la imagen previa al incendio
var postFireStart = '2020-11-16'; // Fecha de inicio para la imagen posterior al incendio
var postFireEnd = '2020-11-30';   // Fecha de fin para la imagen posterior al incendio

// 3. Filtrar la colección MODIS para el período previo al incendio
var preFireImage = modisCollection
  .filterDate(preFireStart, preFireEnd) // Filtrar por fechas
  .filterBounds(cordoba) // Limitar la selección a la región de Córdoba
  .mean() // Promediar las imágenes dentro de este período de tiempo
  .clip(cordoba); // Recortar la imagen al área de la provincia de Córdoba

// 4. Filtrar la colección MODIS para el período posterior al incendio
var postFireImage = modisCollection
  .filterDate(postFireStart, postFireEnd) // Filtrar por fechas
  .filterBounds(cordoba) // Limitar la selección a la región de Córdoba
  .mean() // Promediar las imágenes dentro de este período de tiempo
  .clip(cordoba); // Recortar la imagen al área de la provincia de Córdoba

// 5. Visualizar las imágenes recortadas al ROI para asegurarse de que estén bien limitadas
Map.centerObject(cordoba, 8); // Centrar el mapa en la región de Córdoba
Map.addLayer(preFireImage, {bands: ['Nadir_Reflectance_Band1', 'Nadir_Reflectance_Band4', 'Nadir_Reflectance_Band3'], min: 0, max: 3000}, 'Pre-Fire Image (Jun 2020)');
Map.addLayer(postFireImage, {bands: ['Nadir_Reflectance_Band1', 'Nadir_Reflectance_Band4', 'Nadir_Reflectance_Band3'], min: 0, max: 3000}, 'Post-Fire Image (Nov 2020)');

// 6. Usar la función print() para inspeccionar las propiedades de las imágenes
print('Imagen previa al incendio (Pre-Fire):', preFireImage);
print('Imagen posterior al incendio (Post-Fire):', postFireImage);
```

---

#### Explicación del Código para el Paso 2: Selección de Imágenes MODIS y Recorte al ROI

En este paso, se seleccionan las imágenes de MODIS correspondientes a los períodos antes y después de los incendios en Córdoba. Además, las imágenes se recortan al área de interés para asegurar que el análisis esté enfocado únicamente en la región afectada.

Primero, se carga la colección de imágenes MODIS MCD43A4. Este producto ofrece compuestos de reflectancia de superficie cada 16 días, lo que lo hace adecuado para analizar cambios a lo largo del tiempo. Luego, se definen los rangos de fechas para las imágenes preincendio (junio de 2020) y postincendio (noviembre de 2020). Estas fechas se eligen en función de la cronología de los incendios.

Las imágenes se filtran usando las fechas definidas y la región de Córdoba. Este filtrado asegura que solo se incluyan las imágenes relevantes para el análisis. Para reducir el ruido, las imágenes dentro de cada rango de fechas se promedian. Esto ayuda a obtener una representación más estable de las condiciones en cada período. Posteriormente, las imágenes se recortan al contorno exacto de la provincia de Córdoba utilizando la función `clip()`.

Una vez procesadas las imágenes, se visualizan en el mapa. Las bandas seleccionadas para la visualización son `Nadir_Reflectance_Band1`, `Nadir_Reflectance_Band4` y `Nadir_Reflectance_Band3`, que corresponden a una combinación RGB adecuada para interpretar visualmente los cambios en la vegetación y el suelo.

Finalmente, se utiliza la función `print()` para inspeccionar las propiedades de las imágenes generadas. Esto permite verificar aspectos como las estadísticas de las bandas, el área cubierta y la consistencia de los datos con el ROI definido.

Este paso es esencial para preparar los datos antes de calcular el índice NBR, asegurando que el análisis se realice sobre imágenes representativas y correctamente recortadas al área de estudio. 


---

### Paso 3: Calcular el Índice NBR (Normalized Burn Ratio)

El Índice de Quemadura Normalizada (NBR) es una métrica clave para identificar áreas afectadas por incendios forestales. Este índice utiliza la relación entre las bandas NIR (infrarrojo cercano) y SWIR (infrarrojo de onda corta) para resaltar las áreas quemadas, ya que estas bandas son sensibles a los cambios en la vegetación y el suelo.

En el caso de MODIS MCD43A4, las bandas necesarias para calcular el NBR son:

- `Nadir_Reflectance_Band2` (NIR)
- `Nadir_Reflectance_Band7` (SWIR)

El NBR se calcula utilizando la fórmula:

\[
NBR = \frac{\text{NIR} - \text{SWIR}}{\text{NIR} + \text{SWIR}}
\]

Esta fórmula genera valores entre -1 y 1, donde los valores cercanos a 1 indican vegetación sana, mientras que los valores negativos o bajos reflejan áreas afectadas o no vegetadas.

#### Prompt para ChatGPT - Paso 3

```
Necesito calcular el Índice de Quemadura Normalizada (NBR) para dos imágenes MODIS: una previa y otra posterior a los incendios en Córdoba, Argentina. Usa las bandas `Nadir_Reflectance_Band2` (NIR) y `Nadir_Reflectance_Band7` (SWIR) para calcular el NBR. Proporciona el código paso a paso para calcular este índice para ambas imágenes y explícalo línea por línea.
```

---

#### Código Generado para el Paso 3

```javascript
// Paso 3: Calcular el Índice de Quemadura Normalizada (NBR)

// 1. Calcular el NBR para la imagen previa al incendio
var preFireNBR = preFireImage.expression(
  '(NIR - SWIR) / (NIR + SWIR)', // Fórmula para el cálculo de NBR
  {
    'NIR': preFireImage.select('Nadir_Reflectance_Band2'), // Banda NIR de MODIS
    'SWIR': preFireImage.select('Nadir_Reflectance_Band7') // Banda SWIR de MODIS
  }
).rename('NBR_PreFire'); // Renombrar la banda para identificarla claramente

// 2. Calcular el NBR para la imagen posterior al incendio
var postFireNBR = postFireImage.expression(
  '(NIR - SWIR) / (NIR + SWIR)', // Fórmula para el cálculo de NBR
  {
    'NIR': postFireImage.select('Nadir_Reflectance_Band2'), // Banda NIR de MODIS
    'SWIR': postFireImage.select('Nadir_Reflectance_Band7') // Banda SWIR de MODIS
  }
).rename('NBR_PostFire'); // Renombrar la banda para identificarla claramente

// 3. Visualizar el NBR antes y después del incendio en el mapa
Map.centerObject(cordoba, 8); // Centrar el mapa en la región de Córdoba
Map.addLayer(preFireNBR, {min: -1, max: 1, palette: ['blue', 'white', 'green']}, 'NBR Antes del Incendio (Jun 2020)');
Map.addLayer(postFireNBR, {min: -1, max: 1, palette: ['blue', 'white', 'green']}, 'NBR Después del Incendio (Nov 2020)');

// 4. Imprimir la información de los NBRs para inspeccionar propiedades
print('NBR previo al incendio:', preFireNBR);
print('NBR posterior al incendio:', postFireNBR);
```

---

#### Explicación del Código para el Paso 3: Calcular el Índice de Quemadura Normalizada (NBR)

En este paso, se calcula el Índice de Quemadura Normalizada (NBR) para las imágenes antes y después de los incendios en Córdoba. El NBR es un índice clave para detectar cambios en la vegetación y el suelo, siendo particularmente útil para identificar áreas quemadas.

La fórmula utilizada para calcular el NBR es:

\[
NBR = \frac{\text{NIR} - \text{SWIR}}{\text{NIR} + \text{SWIR}}
\]

Para este análisis, se utilizan las bandas de reflectancia de MODIS:
- **NIR:** `Nadir_Reflectance_Band2` (Infrarrojo cercano).
- **SWIR:** `Nadir_Reflectance_Band7` (Infrarrojo de onda corta).

El cálculo del NBR se realiza mediante la función `expression()`, que permite aplicar la fórmula a cada píxel de la imagen. Este proceso se aplica por separado a las imágenes previas y posteriores al incendio. Cada resultado se renombra para identificar claramente el período correspondiente (`NBR_PreFire` y `NBR_PostFire`).

Después de calcular el NBR, las imágenes se visualizan en el mapa. Para ello, se utiliza una paleta de colores:
- Azul: Valores bajos (suelo desnudo, agua).
- Blanco: Valores intermedios.
- Verde: Valores altos (vegetación saludable).

Esta representación permite interpretar visualmente las condiciones de la vegetación antes y después del evento. Finalmente, la función `print()` se utiliza para inspeccionar las propiedades de las imágenes NBR generadas, facilitando la validación y el control de calidad de los datos.

---

### Paso 4: Calcular la Diferencia de NBR (dNBR)

El siguiente paso en el análisis es calcular la diferencia de NBR (dNBR), que es esencial para identificar las áreas quemadas. El dNBR se calcula restando el NBR posterior al incendio del NBR previo al incendio. Este indicador resalta los cambios en la vegetación y el suelo debido al fuego.

#### Prompt:

```
Necesito calcular la diferencia de NBR (dNBR) para identificar las áreas quemadas en Córdoba, Argentina, durante los incendios de 2020. Usa las imágenes NBR previas y posteriores al incendio calculadas en el paso anterior. Proporciona el código para:
1. Calcular el dNBR restando el NBR posterior al incendio del NBR previo.
2. Asignar un nombre claro a la nueva banda.
3. Visualizar el dNBR en el mapa usando una paleta de colores adecuada.
4. Explica cada línea del código con comentarios para entender su propósito.
```

> Copia este prompt en ChatGPT y utiliza el código generado para continuar con el análisis en GEE. Asegúrate de que la visualización en el mapa sea clara y verifica los valores generados del dNBR para interpretar las áreas quemadas.

#### Explicación del Código para el Paso 4: Calcular la Diferencia de NBR (dNBR)

En este paso, se calcula la Diferencia de NBR (dNBR), que es una métrica clave para identificar las áreas afectadas por incendios forestales. El dNBR mide la variación en el Índice de Quemadura Normalizada (NBR) entre los períodos previos y posteriores al incendio, destacando los cambios significativos en la vegetación y el suelo.

La fórmula para calcular el dNBR es:

\[
dNBR = NBR_{\text{Pre}} - NBR_{\text{Post}}
\]

#### Componentes principales del código:

1. **Cálculo del dNBR**:  
   Se utiliza la función `subtract()` para restar el NBR posterior del NBR previo. Esto genera una nueva imagen en la que cada píxel representa la magnitud del cambio en el NBR. Los valores altos indican áreas con mayor impacto por el incendio, mientras que los valores bajos o negativos indican áreas con pocos cambios o regeneración.

2. **Renombrar la banda**:  
   La nueva banda generada se renombra como `dNBR` para identificarla claramente en el análisis.

3. **Visualización en el mapa**:  
   Se agrega la imagen de dNBR al mapa con una paleta de colores específica:
   - **Azul**: Valores bajos, que representan áreas sin cambios significativos.
   - **Blanco**: Valores intermedios, donde hubo cambios moderados.
   - **Rojo**: Valores altos, que representan áreas severamente quemadas.

4. **Inspección de propiedades**:  
   Se utiliza la función `print()` para explorar las propiedades de la imagen de dNBR, como el rango de valores y las estadísticas de píxeles, lo que permite verificar que el cálculo sea correcto.

Este paso es crucial porque el dNBR proporciona información directa sobre la severidad y la extensión del impacto del incendio en la región de interés (ROI). Con esta información, se pueden realizar análisis más detallados, como la creación de máscaras de áreas quemadas en pasos posteriores.


---

### Paso 5: Crear una Máscara de Áreas Quemadas

En este paso, el objetivo es identificar las áreas quemadas utilizando la diferencia de NBR (dNBR). Esto se logra aplicando un umbral (threshold) que separe los píxeles afectados por el incendio de los que no lo están. Este umbral es clave y puede variar dependiendo de las características del área y de los datos. Por lo tanto, se invita al usuario a experimentar con diferentes valores para determinar el threshold óptimo.


```
Quiero crear una máscara de las áreas quemadas utilizando el índice dNBR calculado previamente. Necesito un fragmento de código que me permita aplicar un umbral inicial de dNBR > 0.66 para identificar áreas severamente afectadas por el incendio. También quiero que el código sea flexible, de modo que pueda probar diferentes valores de threshold para ajustar la detección. Proporciona el código comentado y explica cómo ajustar el umbral.
```

> Acción del estudiante: Copia este prompt en ChatGPT, utiliza el código generado en Google Earth Engine, y ajusta el threshold para evaluar los resultados visuales.

---

#### Código Generado para el Paso 5

```javascript
// Paso 5: Crear una máscara de las áreas quemadas utilizando el umbral de dNBR

// 1. Definir el umbral para la detección de áreas quemadas (puedes cambiar este valor)
var threshold = 0.66; // Umbral para identificar áreas quemadas (puedes modificar este valor)

// 2. Crear la máscara de áreas quemadas (1 = quemada, 0 = no quemada)
var burnedAreaMask = dNBR.gt(threshold) // Comparar dNBR con el umbral
  .selfMask() // Ocultar píxeles que no cumplan la condición (dNBR <= threshold)
  .rename('Burned_Areas'); // Renombrar la banda resultante como 'Burned_Areas'

// 3. Visualizar la máscara de áreas quemadas en el mapa
Map.centerObject(cordoba, 8); // Centrar el mapa en la región de Córdoba
Map.addLayer(burnedAreaMask, 
  {palette: ['red'], min: 0, max: 1}, 
  'Máscara de Áreas Quemadas (dNBR > ' + threshold + ')'
);

// 4. Imprimir la información de la máscara para inspeccionar sus propiedades
print('Máscara de Áreas Quemadas (dNBR > ' + threshold + '):', burnedAreaMask);

```

---

#### Explicación del Código para el Paso 5: Crear una Máscara de Áreas Quemadas

Este paso se enfoca en identificar y visualizar las áreas quemadas aplicando un umbral a la diferencia de NBR (dNBR). La máscara generada es esencial para destacar los píxeles que cumplen con el criterio de cambio significativo tras los incendios.

#### Concepto del Umbral (Threshold)
El umbral define qué tan afectado debe estar un píxel para ser clasificado como quemado. En este ejemplo, el valor inicial de 0.66 se usa como referencia para detectar áreas severamente afectadas. El umbral puede ajustarse para incluir áreas con diferentes niveles de daño.

#### Componentes del Código:
1. **Definición del umbral (`threshold`)**:  
   - El valor inicial se establece en 0.66, pero el usuario tiene la flexibilidad de modificar este valor para evaluar diferentes niveles de afectación. Valores más bajos incluirán áreas con menor daño, mientras que valores más altos se enfocarán en áreas con afectación severa.

2. **Creación de la máscara binaria**:  
   - La función `gt(threshold)` compara cada píxel de dNBR con el umbral. Los píxeles que cumplen la condición (dNBR > threshold) se establecen en 1, mientras que los demás se establecen en 0.  
   - `selfMask()` oculta los píxeles que no cumplen la condición, lo que mejora la visualización.

3. **Renombrar la banda**:  
   - Se utiliza `.rename('Burned_Areas')` para asignar un nombre descriptivo a la banda, facilitando su interpretación y uso posterior.

4. **Visualización de la máscara**:  
   - La máscara se muestra en el mapa con una paleta roja (`palette: ['red']`), destacando claramente las áreas quemadas.  
   - El título de la capa incluye el valor del umbral utilizado, lo que ayuda a rastrear diferentes configuraciones durante el análisis.

5. **Validación mediante inspección**:  
   - La función `print()` permite inspeccionar las propiedades de la máscara generada, como su extensión, estadísticas y geometría, ayudando a verificar la calidad del resultado.

#### Ajustes del Umbral
Se invita al usuario a experimentar con diferentes valores de `threshold` (por ejemplo, 0.4, 0.6, 0.8) para evaluar cómo cambia la detección de áreas quemadas. Esto es crucial para optimizar la identificación de las áreas afectadas según el contexto del análisis.

#### Resultado Esperado
La máscara generada resalta las áreas quemadas en rojo, permitiendo una interpretación visual inmediata. Este resultado prepara el camino para calcular la superficie total quemada y realizar análisis adicionales en los siguientes pasos.


---

### Paso 6: Crear una Máscara de Áreas Quemadas (Eliminando Cuerpos de Agua)

En este paso, se mejora la identificación de áreas quemadas excluyendo los cuerpos de agua. Esto es fundamental, ya que los cuerpos de agua pueden tener valores de dNBR que se asemejan a los de áreas quemadas, generando falsos positivos. Para resolver este problema, se creará una máscara adicional que detecte los cuerpos de agua y se utilizará para excluirlos de la máscara de áreas quemadas.


#### Objetivo
1. Detectar los cuerpos de agua en la región de interés.
2. Crear una máscara de agua y superponerla a la máscara de áreas quemadas.
3. Generar una máscara combinada que solo contenga áreas quemadas excluyendo los cuerpos de agua.



#### Prompt para ChatGPT - Paso 5 (Mejorado con la exclusión de cuerpos de agua)
```
Quiero mejorar la máscara de áreas quemadas utilizando la diferencia de NBR (dNBR). Necesito que primero identifiques los cuerpos de agua dentro de la región de interés y generes una máscara de agua. Luego, utiliza esta máscara de agua para eliminar las áreas de agua de la máscara de áreas quemadas. Proporciona el código necesario para crear la máscara de agua y combinarla con la máscara de áreas quemadas. Explica cada línea del código. 

Ten en cuenta que este es el código hasta aquí:

// Paso 1: Definir la región de interés (ROI)

// 1. Cargar la colección de límites administrativos GAUL de FAO (nivel 1 - provincias/estados)
var gaulCollection = ee.FeatureCollection('FAO/GAUL/2015/level1');

// 2. Filtrar la colección para seleccionar solo las entidades correspondientes a Argentina
var argentina = gaulCollection.filter(ee.Filter.eq('ADM0_NAME', 'Argentina'));

// 3. Filtrar la región de interés para obtener solo la provincia de Cordoba (sin tilde)
var cordoba = argentina.filter(ee.Filter.eq('ADM1_NAME', 'Cordoba'));

// 4. Visualizar la región de Córdoba en el mapa para verificar la geometría
Map.centerObject(cordoba, 8); // Centrar el mapa en Córdoba con un nivel de zoom de 8
Map.addLayer(cordoba, {color: 'red'}, 'Provincia de Córdoba'); // Añadir la capa de Córdoba al mapa en color rojo

// 5. Usar la función print() para mostrar la información de la variable gaulCollection
print('Colección de límites administrativos GAUL (Argentina):', argentina);

// 6. Usar la función print() para mostrar la información de la geometría de Córdoba
print('Geometría de la Provincia de Córdoba:', cordoba);

// Paso 2: Selección de imágenes MODIS y recorte al ROI

// 1. Cargar la colección de imágenes MODIS MCD43A4
var modisCollection = ee.ImageCollection('MODIS/061/MCD43A4');

// 2. Definir las fechas de interés
var preFireStart = '2020-06-01'; // Fecha de inicio para la imagen previa al incendio
var preFireEnd = '2020-06-16';   // Fecha de fin para la imagen previa al incendio
var postFireStart = '2020-11-16'; // Fecha de inicio para la imagen posterior al incendio
var postFireEnd = '2020-11-30';   // Fecha de fin para la imagen posterior al incendio

// 3. Filtrar la colección MODIS para el período previo al incendio
var preFireImage = modisCollection
  .filterDate(preFireStart, preFireEnd) // Filtrar por fechas
  .filterBounds(cordoba) // Limitar la selección a la región de Córdoba
  .mean() // Promediar las imágenes dentro de este período de tiempo
  .clip(cordoba); // Recortar la imagen al área de la provincia de Córdoba

// 4. Filtrar la colección MODIS para el período posterior al incendio
var postFireImage = modisCollection
  .filterDate(postFireStart, postFireEnd) // Filtrar por fechas
  .filterBounds(cordoba) // Limitar la selección a la región de Córdoba
  .mean() // Promediar las imágenes dentro de este período de tiempo
  .clip(cordoba); // Recortar la imagen al área de la provincia de Córdoba

// 5. Visualizar las imágenes recortadas al ROI para asegurarse de que estén bien limitadas
Map.centerObject(cordoba, 8); // Centrar el mapa en la región de Córdoba
Map.addLayer(preFireImage, {bands: ['Nadir_Reflectance_Band1', 'Nadir_Reflectance_Band4', 'Nadir_Reflectance_Band3'], min: 0, max: 3000}, 'Pre-Fire Image (Jun 2020)');
Map.addLayer(postFireImage, {bands: ['Nadir_Reflectance_Band1', 'Nadir_Reflectance_Band4', 'Nadir_Reflectance_Band3'], min: 0, max: 3000}, 'Post-Fire Image (Nov 2020)');

// 6. Usar la función print() para inspeccionar las propiedades de las imágenes
print('Imagen previa al incendio (Pre-Fire):', preFireImage);
print('Imagen posterior al incendio (Post-Fire):', postFireImage);

// Paso 3: Calcular el Índice de Quemadura Normalizada (NBR)

// 1. Calcular el NBR para la imagen previa al incendio
var preFireNBR = preFireImage.expression(
  '(NIR - SWIR) / (NIR + SWIR)', // Fórmula para el cálculo de NBR
  {
    'NIR': preFireImage.select('Nadir_Reflectance_Band2'), // Banda NIR de MODIS
    'SWIR': preFireImage.select('Nadir_Reflectance_Band7') // Banda SWIR de MODIS
  }
).rename('NBR_PreFire'); // Renombrar la banda para identificarla claramente

// 2. Calcular el NBR para la imagen posterior al incendio
var postFireNBR = postFireImage.expression(
  '(NIR - SWIR) / (NIR + SWIR)', // Fórmula para el cálculo de NBR
  {
    'NIR': postFireImage.select('Nadir_Reflectance_Band2'), // Banda NIR de MODIS
    'SWIR': postFireImage.select('Nadir_Reflectance_Band7') // Banda SWIR de MODIS
  }
).rename('NBR_PostFire'); // Renombrar la banda para identificarla claramente

// 3. Visualizar el NBR antes y después del incendio en el mapa
Map.centerObject(cordoba, 8); // Centrar el mapa en la región de Córdoba
Map.addLayer(preFireNBR, {min: -1, max: 1, palette: ['blue', 'white', 'green']}, 'NBR Antes del Incendio (Jun 2020)');
Map.addLayer(postFireNBR, {min: -1, max: 1, palette: ['blue', 'white', 'red']}, 'NBR Después del Incendio (Nov 2020)');

// 4. Imprimir la información de los NBRs para inspeccionar propiedades
print('NBR previo al incendio:', preFireNBR);
print('NBR posterior al incendio:', postFireNBR);

// Paso 4: Calcular la diferencia de NBR (dNBR) para identificar áreas quemadas

// 1. Calcular la diferencia de NBR (dNBR) como la resta entre NBR previo y NBR posterior
var dNBR = preFireNBR.subtract(postFireNBR) // Restar el NBR posterior al NBR previo
  .rename('dNBR'); // Renombrar la banda resultante como 'dNBR'

// 2. Visualizar la dNBR en el mapa
Map.centerObject(cordoba, 8); // Centrar el mapa en Córdoba con un zoom de nivel 8
Map.addLayer(dNBR, 
  {min: -1, max: 1, palette: ['blue', 'white', 'red']}, 
  'dNBR (Diferencia de NBR)'
);

// 3. Imprimir la información de la dNBR para inspeccionar sus propiedades
print('Diferencia de NBR (dNBR):', dNBR);

// Paso 5: Crear una máscara de las áreas quemadas utilizando el umbral de dNBR

// 1. Definir el umbral para la detección de áreas quemadas (puedes cambiar este valor)
var threshold = 0.4; // Umbral para identificar áreas quemadas (puedes modificar este valor)

// 2. Crear la máscara de áreas quemadas (1 = quemada, 0 = no quemada)
var burnedAreaMask = dNBR.gt(threshold) // Comparar dNBR con el umbral
  .selfMask() // Ocultar píxeles que no cumplan la condición (dNBR <= threshold)
  .rename('Burned_Areas'); // Renombrar la banda resultante como 'Burned_Areas'

// 3. Visualizar la máscara de áreas quemadas en el mapa
Map.centerObject(cordoba, 8); // Centrar el mapa en la región de Córdoba
Map.addLayer(burnedAreaMask, 
  {palette: ['red'], min: 0, max: 1}, 
  'Máscara de Áreas Quemadas (dNBR > ' + threshold + ')'
);

// 4. Imprimir la información de la máscara para inspeccionar sus propiedades
print('Máscara de Áreas Quemadas (dNBR > ' + threshold + '):', burnedAreaMask);
```
> **Nota para el estudiante**: A veces debemos recordarle a ChatGPT cuales han sido sus respuestas anteriores para que sea consistente con las respuestas siguientes. En este caso se incluye el código que ya ha generado para que considere cualquier modificacion que nosotros hayamos hecho 

#### Resultado esperado

```javascript
// Paso 6: Identificación de cuerpos de agua y exclusión de la máscara de áreas quemadas

// 1. Calcular el Índice de Agua Diferenciado Normalizado (NDWI) para identificar cuerpos de agua
var ndwi = preFireImage.expression(
  '(GREEN - NIR) / (GREEN + NIR)', // Fórmula para el cálculo de NDWI
  {
    'GREEN': preFireImage.select('Nadir_Reflectance_Band4'), // Banda Verde (MODIS)
    'NIR': preFireImage.select('Nadir_Reflectance_Band2') // Banda NIR (MODIS)
  }
).rename('NDWI'); // Renombrar la banda resultante como 'NDWI'

// 2. Definir el umbral para identificar cuerpos de agua
var waterThreshold = 0.2; // Umbral para la detección de cuerpos de agua (puedes cambiar este valor)

// 3. Crear la máscara de agua (1 = agua, 0 = no agua)
var waterMask = ndwi.gt(waterThreshold) // Identificar píxeles de agua (NDWI > 0.2)
  .rename('Water_Mask'); // Renombrar la banda para identificarla claramente

// 4. Visualizar la máscara de agua en el mapa
Map.addLayer(waterMask, 
  {palette: ['blue'], min: 0, max: 1}, 
  'Máscara de Cuerpos de Agua (NDWI > ' + waterThreshold + ')'
);

// 5. Imprimir la información de la máscara de agua
print('Máscara de Agua (NDWI > ' + waterThreshold + '):', waterMask);

// 6. Visualizar la máscara de áreas quemadas antes de aplicar la máscara de agua
Map.addLayer(burnedAreaMask, 
  {palette: ['red'], min: 0, max: 1}, 
  'Máscara de Áreas Quemadas (antes de excluir agua)'
);

// 7. Crear una máscara lógica que combine la máscara de áreas quemadas y la máscara de agua
var refinedBurnedAreaMask = burnedAreaMask.and(waterMask.not()) // Áreas quemadas que NO están en el agua
  .selfMask() // Ocultar píxeles donde la condición no se cumple (quedan NoData)
  .rename('Refined_Burned_Areas'); // Renombrar la banda para identificarla claramente

// 8. Visualizar la máscara de áreas quemadas refinada (sin agua)
Map.addLayer(refinedBurnedAreaMask, 
  {palette: ['red'], min: 0, max: 1}, 
  'Máscara de Áreas Quemadas Refinada (sin agua)'
);

// 9. Imprimir la información de la máscara de áreas quemadas refinada
print('Máscara de Áreas Quemadas Refinada (sin agua):', refinedBurnedAreaMask);

// 10. Verificar la intersección de las áreas de agua y las áreas quemadas
Map.addLayer(waterMask, {palette: ['blue'], min: 0, max: 1}, 'Máscara de Agua');
Map.addLayer(dNBR, {min: -1, max: 1, palette: ['blue', 'white', 'red']}, 'dNBR');
Map.addLayer(burnedAreaMask, {palette: ['red'], min: 0, max: 1}, 'Máscara de Áreas Quemadas');
```

---

#### Explicación del Código para el Paso 6: Crear una Máscara de Áreas Quemadas (Eliminando Cuerpos de Agua)

**1. Identificar los cuerpos de agua con NDWI**

El NDWI (Índice de Diferencia de Agua Normalizada) permite identificar los cuerpos de agua utilizando la relación entre la banda verde (GREEN) y la banda infrarroja cercana (NIR). La fórmula para calcular el NDWI es:

\[
NDWI = \frac{(GREEN - NIR)}{(GREEN + NIR)}
\]

En este caso, se usa la imagen previa al incendio para calcular el NDWI. La banda verde (Nadir_Reflectance_Band4) y la banda NIR (Nadir_Reflectance_Band2) se utilizan para calcular el índice. Los valores de NDWI cercanos a 1 indican agua, mientras que los valores cercanos a -1 corresponden a suelo o vegetación.

**Lo que hace el código:**
- Calcula el NDWI usando la fórmula.
- Los valores de NDWI se almacenan en una nueva banda llamada **NDWI**.

**Fragmento de código:**
```javascript
var ndwi = preFireImage.expression(
  '(GREEN - NIR) / (GREEN + NIR)', 
  {
    'GREEN': preFireImage.select('Nadir_Reflectance_Band4'), 
    'NIR': preFireImage.select('Nadir_Reflectance_Band2') 
  }
).rename('NDWI'); 
```

**2. Crear una máscara de agua**

Para diferenciar los cuerpos de agua del resto, se aplica un umbral (threshold) al NDWI. Los píxeles con valores de NDWI mayores a **0.2** se consideran agua.

**Lo que hace el código:**
- Define el umbral de agua en **0.2**.
- Crea una máscara que identifica los píxeles de agua con un valor de **1** (agua) y el resto con un valor de **0** (no agua).
- La máscara se llama **Water_Mask**.

**Fragmento de código:**
```javascript
var waterThreshold = 0.2; 
var waterMask = ndwi.gt(waterThreshold) 
  .rename('Water_Mask'); 
```

**3. Eliminar los cuerpos de agua de la máscara de áreas quemadas**

Ahora que se tiene la máscara de agua, se usa para quitar los cuerpos de agua de la máscara de áreas quemadas. Para hacer esto, se excluyen los píxeles de agua de la máscara de áreas quemadas.

**Lo que hace el código:**
- Usa la función `and()` para combinar la máscara de áreas quemadas con la máscara de agua invertida.
- La función `waterMask.not()` invierte la máscara de agua (los píxeles de agua se convierten en **0** y los demás en **1**).
- Se combina la máscara de áreas quemadas con la máscara de agua invertida, eliminando los cuerpos de agua de la máscara de áreas quemadas.
- La nueva máscara se llama **Refined_Burned_Areas**.

**Fragmento de código:**
```javascript
var refinedBurnedAreaMask = burnedAreaMask.and(waterMask.not()) 
  .selfMask() 
  .rename('Refined_Burned_Areas'); 
```

**4. Visualizar la máscara refinada**

Se visualiza la máscara de áreas quemadas refinada para comprobar que se han excluido correctamente los cuerpos de agua. También se muestra la máscara de agua para verificar que ambas se visualizan de forma correcta.

**Lo que hace el código:**
- Muestra la máscara de agua (en azul) para verificar la correcta identificación de los cuerpos de agua.
- Muestra la máscara de áreas quemadas refinada (en rojo) para ver cómo se excluyeron los cuerpos de agua de la máscara.

**Fragmento de código:**
```javascript
Map.addLayer(waterMask, {palette: ['blue'], min: 0, max: 1}, 'Máscara de Agua');
Map.addLayer(refinedBurnedAreaMask, {palette: ['red'], min: 0, max: 1}, 'Máscara de Áreas Quemadas Refinada (sin agua)');
```

### Paso 7: Calcular la Superficie Total Quemada

```
Quiero calcular la superficie total quemada en Córdoba, Argentina, utilizando la máscara de áreas quemadas que excluye los cuerpos de agua. Necesito que el cálculo se realice en hectáreas (ha). 

Para ello, sigue estos pasos:
1. Usa la máscara de áreas quemadas refinada (Refined_Burned_Areas) que ya hemos generado.
2. Calcula la cantidad de píxeles quemados que estén dentro de la región de interés (ROI) de Córdoba.
3. Convierte esta cantidad de píxeles a hectáreas, considerando el área de cada píxel de MODIS.
4. Imprime la superficie total quemada en hectáreas.
5. Proporciona comentarios línea por línea en el código para explicar cada paso.

```

> **Acción del estudiante**: Copia este prompt en ChatGPT y utiliza la respuesta generada en Google Earth Engine. Verifica si la superficie total quemada se muestra correctamente en hectáreas.

#### Resultado esperado

```javascript
// Paso 7: Calcular la superficie total quemada (en hectáreas) en la región de Córdoba

// 1. Definir la resolución espacial de la imagen MODIS (500 m x 500 m)
var pixelArea = 500 * 500; // Cada píxel de MODIS tiene un área de 500m x 500m = 250,000 m²

// 2. Convertir el área de cada píxel de m² a hectáreas (1 ha = 10,000 m²)
var pixelAreaHa = pixelArea / 10000; // Convertir de metros cuadrados (m²) a hectáreas (ha)
print('Área de cada píxel en hectáreas:', pixelAreaHa);

// 3. Contar la cantidad de píxeles quemados dentro de la región de Córdoba
var burnedAreaStats = refinedBurnedAreaMask.reduceRegion({
  reducer: ee.Reducer.sum(), // Suma de los píxeles de la máscara (1 = quemado, 0 = no quemado)
  geometry: cordoba.geometry(), // Limitar el cálculo al área de Córdoba
  scale: 500, // Usar la resolución de la imagen MODIS (500 m)
  maxPixels: 1e13 // Permitir un número máximo de píxeles a procesar
});

// 4. Extraer la cantidad de píxeles quemados de la operación reduceRegion()
var burnedPixelCount = ee.Number(burnedAreaStats.get('Refined_Burned_Areas')); 
print('Cantidad de píxeles quemados:', burnedPixelCount);

// 5. Calcular la superficie total quemada en hectáreas
var burnedAreaHa = burnedPixelCount.multiply(pixelAreaHa); // Multiplicar el número de píxeles quemados por el área de cada píxel en ha
print('Superficie total quemada (hectáreas):', burnedAreaHa);

// 6. Visualizar la máscara de áreas quemadas refinada en el mapa
Map.addLayer(refinedBurnedAreaMask, 
  {palette: ['red'], min: 0, max: 1}, 
  'Máscara de Áreas Quemadas Refinada (sin agua)'
);
```

#### Explicación del Código para el Paso 7: Calcular la Superficie Total Quemada

En este paso, se calcula la superficie total quemada en hectáreas para la región de Córdoba, excluyendo los cuerpos de agua. Este cálculo se basa en la cantidad de píxeles que cumplen con la condición de área quemada (dNBR > umbral) y la conversión de esta cantidad de píxeles a hectáreas.

**1. Definir el área de un píxel en hectáreas**  
Cada píxel de la imagen MODIS tiene una resolución de 500 x 500 metros, lo que equivale a 250,000 m² por píxel. Para convertir esta superficie a hectáreas, se utiliza la conversión estándar de 1 hectárea = 10,000 m².  
Fórmula:  
\[
\text{Área del píxel en hectáreas} = \frac{500 \times 500}{10,000} = 25 \, \text{ha}
\]
Este valor se utiliza más adelante para calcular la superficie total quemada.


**2. Contar los píxeles quemados en la región de Córdoba**  
Para determinar cuántos píxeles representan áreas quemadas, se utiliza la función `reduceRegion()`. Esta función aplica un reductor, en este caso `ee.Reducer.sum()`, que suma todos los píxeles que cumplen con la condición de área quemada (es decir, aquellos con un valor de 1 en la máscara `Refined_Burned_Areas`).  
La operación se limita a la región de interés (ROI) de Córdoba para evitar contar píxeles fuera del área de estudio.  
Parámetros importantes de `reduceRegion()`:
- **reducer**: Suma los valores de los píxeles dentro de la región de Córdoba.
- **geometry**: Define la región de Córdoba para limitar el área de análisis.
- **scale**: Define la escala de los datos (500 m en el caso de MODIS).
- **maxPixels**: Establece la cantidad máxima de píxeles que se permite procesar para evitar errores de límite de píxeles.

El resultado de `reduceRegion()` es un objeto con la suma de los píxeles, que se almacena en la variable `burnedPixelCount`.


**3. Calcular la superficie total quemada**  
Para calcular la superficie quemada, se multiplica la cantidad de píxeles quemados (`burnedPixelCount`) por el área de cada píxel en hectáreas (`pixelAreaHa`), previamente calculado.  
Fórmula:  
\[
\text{Superficie quemada (ha)} = \text{Cantidad de píxeles quemados} \times \text{Área del píxel (ha)} 
\]
Este resultado se imprime en la consola de Google Earth Engine para que el usuario pueda ver la superficie total quemada.


**4. Visualizar la máscara de áreas quemadas refinada**  
Finalmente, se visualiza la máscara de áreas quemadas en el mapa. Esta máscara muestra en color rojo las áreas que se consideran quemadas. Este paso permite al usuario verificar visualmente que las áreas quemadas se encuentran correctamente delimitadas en la región de Córdoba.  
El mapa ayuda a confirmar que las áreas de agua han sido correctamente excluidas y que la superficie quemada se ha calculado adecuadamente.


:::: {.blackbox data-latex=""}
::: {.center data-latex=""}
**Resultado**
:::
Cantidad de píxeles quemados: 8307

Superficie total quemada (hectáreas): 207.696
::::


La imagen \@ref(fig:area-quemada) muestra la mascara final con las áreas quemadas. Compara este resultado con el artículo de wikipedia y saca conclusiones.

<div class="figure">
<img src="figuras/resultado_area_quemada.png" alt="Interfaz principal de Google Earth Engine." width="100%" />
<p class="caption">(\#fig:area-quemada)Interfaz principal de Google Earth Engine.</p>
</div>

### Preguntas al lector

```{=html}
<p> Responde las preguntas a continuación y al finalizar haz clic en Submit. Luego revisa el score para ver si las respuesta fueron correctas</p>

<iframe src="https://docs.google.com/forms/d/e/1FAIpQLScXBdiHSKDk-scTQYurstMJCN6NoRtuJITlDVWmFkhyYFaVIQ/viewform?embedded=true" width="800" height="1000" frameborder="0" marginheight="0" marginwidth="0">Loading…</iframe>
```

---

