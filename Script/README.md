# Análisis de Coberturas

Este repositorio contiene el notebook **Análisis_Coberturas.ipynb**, el cual realiza un análisis detallado de coberturas terrestres utilizando imágenes satelitales. Se emplean técnicas de procesamiento de imágenes y análisis de índices de vegetación para evaluar la distribución de diferentes tipos de coberturas.

## Contenido del Notebook

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

## Uso

1. Clona este repositorio:
   ```bash
   git clone https://github.com/tuusuario/Analisis_Coberturas.git
   cd Analisis_Coberturas
   ```

2. Abre el notebook en Google Colab o Jupyter:
   ```bash
   jupyter notebook Análisis_Coberturas.ipynb
   ```

3. Ejecuta cada celda siguiendo el flujo del análisis.

## Contacto

Si tienes preguntas o deseas contribuir, no dudes en abrir un issue o contactarme en [tu email o perfil de GitHub].

---
*Este repositorio es parte de un proyecto de análisis geoespacial para la caracterización de coberturas terrestres mediante imágenes satelitales.*
