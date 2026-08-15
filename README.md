# Laboratorio 4: Monitoreo de Cianobacterias en Lagos de Guatemala con Sentinel-2

Este repositorio contiene el desarrollo del Laboratorio 4, cuyo objetivo es estimar y analizar la concentración de cianobacterias en los lagos de Atitlán y Amatitlán a partir de imágenes satelitales Sentinel-2, obtenidas mediante la API de SentinelHub. El análisis combina procesamiento de datos raster, cálculo de índices espectrales, análisis temporal y análisis espacial para caracterizar el comportamiento de las floraciones algales en ambos cuerpos de agua a lo largo de distintas fechas de muestreo.

## Contenido del notebook

El notebook principal, Lab4_GeoEspaciales.ipynb, está organizado en las siguientes secciones.

La primera parte establece la conexión con Sentinel Hub, define las credenciales necesarias a través de variables de entorno y configura las coordenadas de los dos lagos de estudio junto con las fechas de las imágenes utilizadas.

La segunda parte descarga las bandas espectrales necesarias para el análisis, correspondientes a B03, B04, B05, B08 y la máscara de clasificación de escena SCL, y las almacena localmente en formato numpy dentro de la carpeta datos_sentinel.

La tercera parte calcula los índices espectrales utilizados en el análisis. El índice NDVI se obtiene a partir de las bandas B08 y B04, el índice NDWI se obtiene a partir de las bandas B03 y B08, y la estimación de clorofila a asociada a la presencia de cianobacterias se calcula mediante el índice NDCI, construido a partir de las bandas B04 y B05, aplicando una máscara de agua derivada del NDWI para descartar píxeles de tierra.

La cuarta parte desarrolla el análisis temporal, calculando el promedio de concentración de clorofila a por fecha y por lago, identificando las fechas con mayores valores registrados y visualizando la evolución de la concentración a lo largo del periodo de estudio.

La quinta parte corresponde al análisis espacial, donde se generan mapas estáticos e interactivos de la distribución de cianobacterias dentro de cada lago, se comparan mapas entre distintas fechas y se interpretan los patrones espaciales observados, incluyendo la identificación de zonas de acumulación persistente.

La sexta parte evalúa la relación entre los índices espectrales y la concentración de cianobacterias mediante correlaciones estadísticas y matrices de correlación.

La séptima parte realiza un análisis comparativo entre ambos lagos, evaluando la intensidad y frecuencia de las floraciones, discutiendo posibles causas ambientales asociadas a la actividad humana en las cuencas, y presentando una tabla resumen de evidencia.

La octava parte amplía el análisis exploratorio evaluando la extensión espacial de la floración en cada fecha, identificando zonas persistentes de acumulación y su significado ambiental, comparando la distribución de valores entre fechas mediante histogramas, boxplots y mapas de diferencia, explorando la existencia de un patrón estacional asociado al ciclo de lluvias, e integrando la interpretación de todos los resultados obtenidos.

## Requisitos

El notebook requiere una cuenta activa en Sentinel Hub con credenciales de cliente configuradas mediante un archivo de entorno. Las librerías principales utilizadas incluyen numpy, pandas, rasterio, sentinelhub, matplotlib, folium, seaborn, scipy y pillow.

Antes de ejecutar el notebook es necesario crear un archivo .env en la raíz del proyecto con las siguientes variables.

```
SH_CLIENT_ID=tu_client_id
SH_CLIENT_SECRET=tu_client_secret
```

Estas credenciales se obtienen desde el panel de Sentinel Hub Dashboard, en la sección de OAuth clients.

## Instalación

Las dependencias pueden instalarse directamente desde las primeras celdas del notebook mediante pip, o de forma manual ejecutando el siguiente comando en el entorno de trabajo.

```
pip install python-dotenv sentinelhub rasterio folium pandas numpy matplotlib seaborn scipy pillow
```

## Estructura de datos generada

Al ejecutar el notebook se crea automáticamente la carpeta datos_sentinel, con una subcarpeta por cada lago y, dentro de esta, una subcarpeta por cada fecha de muestreo. En cada una de estas subcarpetas se almacenan los arreglos numpy correspondientes a las bandas descargadas, lo que permite reutilizar los datos sin necesidad de volver a consultar la API en ejecuciones posteriores.

## Lagos y fechas analizadas

El análisis se realiza sobre dos lagos de Guatemala. El lago de Atitlán se evalúa en once fechas distribuidas entre enero de 2025 y julio de 2026. El lago de Amatitlán se evalúa igualmente en once fechas distribuidas entre enero de 2025 y junio de 2026. Las coordenadas de cada lago y el listado completo de fechas se encuentran definidos en la sección de configuración inicial del notebook.

## Salidas generadas

Durante la ejecución del notebook se generan distintos productos visuales guardados como archivos de imagen y html, entre ellos la composición en falso color de verificación de las bandas descargadas, los mapas de distribución espacial de cianobacterias por lago y fecha, un mapa interactivo en formato html para el lago de Amatitlán, la gráfica de evolución temporal de la concentración promedio de clorofila a, la matriz de correlación entre índices espectrales, la comparación de distribución de valores entre lagos, y la tabla resumen de evidencia correspondiente al análisis comparativo entre lagos.

## Hallazgos principales

El análisis muestra que la concentración de cianobacterias y la extensión espacial de las floraciones difieren de manera notable entre ambos lagos, siendo consistentemente mayores en el lago de Amatitlán que en el lago de Atitlán. Esta diferencia se asocia principalmente a la mayor presión antropogénica sobre la cuenca de Amatitlán, derivada de la descarga de aguas residuales domésticas e industriales provenientes de la ciudad capital, lo que incrementa el aporte de fósforo y nitrógeno disponibles para el crecimiento de cianobacterias. El análisis espacial identifica además zonas de acumulación persistente dentro de cada lago, cuya ubicación resulta coherente con posibles fuentes de nutrientes cercanas a la orilla, y el análisis temporal sugiere una posible influencia estacional asociada al ciclo de lluvias de la región.

## Autoría

Trabajo desarrollado como parte del Laboratorio 4 del curso, con apoyo de consulta técnica externa para la interpretación de las causas ambientales asociadas a la proliferación de cianobacterias en ambos lagos.
