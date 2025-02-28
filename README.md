# Prefactibilidad_SUAN
# Análisis de Biomasa y NDVI con Python

Este repositorio contiene scripts y datos para el análisis de biomasa, NDVI y coberturas vegetales utilizando Python. Los datos incluyen imágenes satelitales (Sentinel-2) en diferentes periodos de tiempo, mientras que los scripts permiten calcular índices de vegetación, recortar polígonos y realizar análisis sobre manglares y coberturas.

## 📂 Estructura del Repositorio

```
/Analisis-Biomasa-NDVI
│── 📁 base_datos/              # Datos de entrada (CSV, GeoJSON, KML, Shapefiles, etc.)
│
│── 📁 imagenes/                # Imágenes utilizadas en el análisis
│   ├── 📁 anterior/            # Imágenes previas al análisis
│   ├── 📁 posterior/           # Imágenes después del análisis
│
│── 📁 scripts/                 # Código Python para el análisis
│   ├── análisis_df_manglares.py   # Análisis de datos de manglares
│   ├── análisis_coberturas.py     # Análisis de coberturas vegetales
│   ├── recorte_poligonos_geojson_.py # Recorte de polígonos en GeoJSON
├── README.md               # Información del repositorio
│
```

El análisis de coberturas a partir de imágenes satelitales es una herramienta clave para la teledetección y un enfoque innovador para realizar estudios ambientales que permiten evaluar diversos cambios en la superficie terrestre, el monitoreo de recursos naturales y la planificación territorial. Para ello se hace uso de plataformas que permiten acceder a la información con el fin de realizar el procesamiento de dichas imágenes. 

Entre estas herramientas se encuentra EO Browser, disponible en la plataforma Sentinel Hub, que permite explorar y comparar imágenes de resolución completa a lo largo del tiempo. Además, para llevar a cabo análisis de coberturas de manera eficiente, se puede utilizar Google Colab, una herramienta proporcionada por Google que permite realizar análisis de imágenes satelitales mediante códigos escritos, logrando un procesamiento rápido y preciso. 

## Coberturas de Manglares: Chocó, Cauca, Nariño y Valle del Cauca.
En la región del Pacifico colombiano, los manglares se distribuyen a lo largo de las costas de los departamentos de Chocó,Cauca,Nariño y Valle del Cauca. Estos ecosistemas desempeñan un papel fundamental en la protección del litoral y la captura de carbono. Para el estudio de estas coberturas se utilizaron archivos GeoJSON específicos para cada zona de manglar, los cuales permitieron la delimitación de las zonas de interés, en total fueron 2076 zonas distribuidas a lo largo de estas regiones.  

## 📜 Dependencias
Este proyecto utiliza las siguientes librerías:
```txt
pandas
gdal
geopandas
rasterio
folium
shapely
scikit-learn
xgboost
numpy
matplotlib
seaborn
```
## 🛠 Uso de los Scripts

- `análisis_df_manglares.py`: Analiza los datos de biomasa y NDVI en manglares.
- `análisis_coberturas.py`: Permite evaluar las coberturas de vegetación.
- `recorte_poligonos_geojson_.py`: Recorta y filtra polígonos a partir de archivos GeoJSON.

📊 Visualización de Resultados

Los resultados generados en este proyecto pueden ser visualizados a través de dashboards interactivos en Looker:

Dashboard de Análisis de NDVI y Biomasa: Enlace

Dashboard de Cambios en Cobertura Vegetal: [Enlace](https://lookerstudio.google.com/s/r5w3Z8rDXbI)

Estos dashboards permiten explorar los datos de manera interactiva y realizar análisis visuales sobre la evolución de la biomasa y las coberturas vegetales.

📌 Notas

Se recomienda trabajar en un entorno virtual para evitar conflictos con librerías existentes.

Para procesar grandes volúmenes de imágenes TIFF, asegúrate de contar con suficiente memoria.
