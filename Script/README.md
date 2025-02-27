# Análisis de Biomasa y NDVI con Python

Este repositorio contiene scripts y datos para el análisis de biomasa, NDVI y coberturas vegetales utilizando Python. Los datos incluyen imágenes satelitales (Sentinel-2) y de dron (Wingtra) en diferentes periodos de tiempo, mientras que los scripts permiten calcular índices de vegetación, recortar polígonos y realizar análisis sobre manglares y coberturas.

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
│
│── 📁 docs/                    # Documentación y guías
│   ├── README.md               # Información del repositorio
│   ├── INSTALL.md              # Instrucciones de instalación
│   ├── USO.md                  # Cómo ejecutar los scripts
│
│── .gitignore                  # Archivos a excluir del control de versiones
│── requirements.txt            # Librerías necesarias para ejecutar los scripts
│── LICENSE                     # Licencia del proyecto
```

## 🚀 Instalación

Para ejecutar los scripts de este repositorio, sigue estos pasos:

1. Clona este repositorio en tu máquina local:
   ```bash
   git clone https://github.com/tuusuario/Analisis-Biomasa-NDVI.git
   cd Analisis-Biomasa-NDVI
   ```

2. Instala las dependencias necesarias:
   ```bash
   pip install -r requirements.txt
   ```

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

Ejemplo de ejecución:
```bash
python scripts/análisis_coberturas.py
```

## 📌 Notas
- Se recomienda trabajar en un entorno virtual para evitar conflictos con librerías existentes.
- Para procesar grandes volúmenes de imágenes TIFF, asegúrate de contar con suficiente memoria.

## 📜 Licencia
Este proyecto está bajo la licencia MIT. Consulta el archivo `LICENSE` para más información.

---

📧 Para consultas o mejoras, puedes contribuir con un **Pull Request** o contactar a los desarrolladores.





# Análisis de Coberturas

El código realiza un análisis geoespacial para clasificar y cuantificar diferentes tipos de cobertura vegetal (principalmente manglares) en imágenes satelitales. Utiliza índices espectrales como el NDVI (Índice de Vegetación Diferencial Normalizado) y el NDWI (Índice de Agua Diferencial Normalizado) para identificar áreas con diferentes niveles de degradación, así como cuerpos de agua y áreas sin vegetación. Además, calcula métricas como el área en hectáreas, la biomasa total y el promedio de NDVI para cada tipo de cobertura.

## 1. Contenido del Notebook

1. **Carga de Datos**  
   - Importación de imágenes satelitales en formato TIFF.
   - Exploración de los metadatos de las imágenes.

2. **Preprocesamiento**  
   - Corrección radiométrica y normalización.
   - Cálculo del NDVI (Índice de Vegetación de Diferencia Normalizada).

3. **Clasificación de Coberturas**  
   - Segmentación basada en NDVI.
   - Categorización de tipos de cobertura terrestre.

4. **Visualización y Análisis**  
   - Generación de mapas de cobertura.
   - Comparación de coberturas en diferentes períodos de tiempo.

## Requisitos

Para ejecutar este notebook, es necesario contar con:

- Python 3.7+
- Google Colab o Jupyter Notebook
- Las siguientes librerías de Python:
  ```python
  pip install rasterio numpy pandas matplotlib geopandas scikit-learn
  ```
¡Claro! A continuación, te presento un **informe detallado** del código que has compartido. Este informe incluye una descripción de los objetivos, la metodología, las funciones clave y los resultados esperados.

---


---

### **2. Introducción**
El objetivo principal del proyecto es:
- **Clasificar áreas de manglar** en función de su nivel de degradación (baja, media, alta).
- Identificar otras coberturas como **agua, cuerpos sin vegetación**, etc.
- Cuantificar métricas relevantes como:
  - Área en hectáreas.
  - Biomasa total.
  - Promedio de NDVI.
  - Porcentajes relativos de cobertura, biomasa y NDVI.

El análisis se basa en imágenes satelitales en formato `.tiff` que contienen bandas espectrales específicas (B08, B04, B11, B03). Estas bandas son procesadas para calcular los índices espectrales necesarios.

---

### **3. Metodología**

#### **3.1. Datos de Entrada**
- **Imágenes satelitales**: Archivos `.tiff` organizados en dos carpetas (`carpeta_imagenes_1` y `carpeta_imagenes_2`).
- **Estructura de nombres de archivos**: Los nombres siguen un patrón específico que incluye información sobre:
  - Departamento.
  - Fecha.
  - Municipio.
  - Satélite.
  - Banda espectral (B08, B04, B11, B03).

#### **3.2. Procesamiento de Datos**
El código sigue un flujo estructurado:

1. **Agrupación de Imágenes**:
   - La función `agrupar_imagenes` organiza las imágenes por claves únicas basadas en su nombre.
   - Cada clave agrupa las bandas espectrales correspondientes a una misma ubicación y fecha.

2. **Procesamiento de Imágenes**:
   - La función `process_image` carga las bandas espectrales requeridas (B08, B04, B11, B03) y calcula:
     - **NDVI**: Para evaluar la salud de la vegetación.
     - **NDWI**: Para identificar cuerpos de agua.
     - **Máscara**: Para filtrar píxeles válidos (evitar valores negativos o cero).

3. **Clasificación de Cobertura**:
   - La función `clasificar_cobertura` utiliza umbrales de NDVI y NDWI para clasificar los píxeles en categorías:
     - Manglar con degradación baja, media o alta.
     - Sin vegetación.
     - Agua y otros.

4. **Cálculo de Métricas**:
   - **Área en hectáreas**: Se calcula utilizando el tamaño del píxel y la máscara de cobertura.
   - **Biomasa total**: Se estima solo para áreas de manglar usando una fórmula basada en el NDVI.
   - **Promedio de NDVI**: Se calcula para cada tipo de cobertura.

5. **Agregación de Resultados**:
   - Los resultados se almacenan en un DataFrame (`df_temporal`) que contiene métricas para cada tipo de cobertura.
   - Se calculan totales y porcentajes relativos para:
     - Área (%Cobertura).
     - Biomasa (%Biomasa).
     - NDVI (%NDVI).

---

### **4. Funciones Clave**

#### **4.1. `agrupar_imagenes(carpeta)`**
- **Propósito**: Organiza las imágenes por ubicación, fecha y municipio.
- **Entrada**: Carpeta que contiene archivos `.tiff`.
- **Salida**: Diccionario donde cada clave agrupa las bandas espectrales correspondientes.

#### **4.2. `process_image(bandas)`**
- **Propósito**: Calcula los índices espectrales NDVI y NDWI a partir de las bandas espectrales.
- **Entrada**: Diccionario con las rutas de las bandas requeridas.
- **Salida**: Matrices de NDVI, NDWI y una máscara de píxeles válidos.

#### **4.3. `clasificar_cobertura(ndvi, ndwi)`**
- **Propósito**: Clasifica los píxeles en categorías de cobertura según umbrales de NDVI y NDWI.
- **Entrada**: Matrices de NDVI y NDWI.
- **Salida**: Matriz de clasificación con valores enteros que representan cada categoría.

#### **4.4. `calcular_area_hectareas(cobertura)`**
- **Propósito**: Calcula el área en hectáreas de una cobertura específica.
- **Entrada**: Máscara binaria de la cobertura.
- **Salida**: Área en hectáreas.

---

### **5. Resultados Esperados**

#### **5.1. Salida Principal**
El resultado final es un DataFrame (`df_resultados`) que contiene las siguientes columnas:
- **Depto**: Departamento.
- **Municipio**: Municipio.
- **Shape_Leng**: Longitud de la forma asociada.
- **Fecha**: Fecha de la imagen.
- **Ecosistema**: Tipo de ecosistema (en este caso, "Manglar").
- **Cobertura**: Categoría de cobertura (por ejemplo, "Manglar con degradación baja").
- **Superficie(ha)**: Área en hectáreas.
- **%Cobertura**: Porcentaje relativo de cobertura respecto al total.
- **Biomasa Total**: Biomasa estimada.
- **%Biomasa**: Porcentaje relativo de biomasa respecto al total.
- **Promedio NDVI**: Promedio de NDVI para la cobertura.
- **%NDVI**: Porcentaje relativo de NDVI respecto al total.

#### **5.2. Uso Potencial**
Este análisis puede ser utilizado para:
- Monitorear la salud de los manglares a lo largo del tiempo.
- Identificar áreas críticas de degradación.
- Evaluar el impacto de intervenciones ambientales.
- Generar informes para políticas públicas o estudios científicos.

---

### **6. Conclusiones y Recomendaciones**

#### **6.1. Conclusiones**
- El código implementa un flujo completo para analizar imágenes satelitales y clasificar coberturas vegetales.
- Las métricas generadas proporcionan una visión cuantitativa de la distribución de manglares y otras coberturas.
- El uso de índices espectrales (NDVI y NDWI) permite una clasificación precisa y automatizada.

#### **6.2. Recomendaciones**
1. **Validación de Datos**:
   - Verificar que todas las imágenes tengan las bandas requeridas (B08, B04, B11, B03).
   - Asegurarse de que los nombres de archivo sigan el patrón esperado.
2. **Optimización**:
   - Paralelizar el procesamiento de imágenes para mejorar el rendimiento.
3. **Visualización**:
   - Generar mapas de cobertura para complementar los resultados tabulares.
4. **Documentación**:
   - Documentar las fórmulas utilizadas para calcular la biomasa y los umbrales de clasificación.

---



Espero que este informe sea útil para ti... 😊

