# proyecto_EDA_python
Proyecto EDA de Python para el bootcamp de Analisis de Datos de ThePower Education

Análisis Exploratorio de Datos - Campañas de Marketing Bancario

1. Propósito del Proyecto

Este proyecto consiste en un Análisis Exploratorio de Datos (EDA) sobre las campañas de marketing directo de una institución bancaria portuguesa. El objetivo principal es identificar el perfil del cliente que suscribe depósitos a plazo y entender qué factores (económicos, temporales o de contacto) influyen en el éxito de la conversión.

2. Estructura del Repositorio

data/: Contiene los archivos originales en la carpeta "RAW" (bank-additional.csv, customer-details.xlsx) y los archivos procesados en la carpeta "Procesado" (bank.additional-clean.csv, customer-details-clean.csv, tablas_limpias.csv).

notebooks/: Jupyter Notebook con el código de limpieza, transformación y visualización.

README.md: Informe detallado del proyecto y conclusiones.

3. Proceso de Transformación y Limpieza

Se realizaron las siguientes acciones para garantizar la calidad de los datos y poder realizar un análisis de forma correcta y organizada:

- Exploración de los datos: se utilizaron 

Unificación de fuentes: Se combinaron los datos de la campaña con los detalles demográficos de los clientes mediante sus identificadores únicos.

Gestión de Tipos: Conversión de la columna date a formato datetime y manejo de variables categóricas.

Tratamiento de Nulos y Outliers: Se identificaron valores atípicos en la duración de las llamadas y se analizó el valor especial 999 en la variable pdays.

Ingeniería de Variables: * Segmentación de la duración de llamadas (<1m, 1-5m, 5-15m, >15m).

Cálculo de kids_total a partir de Kidhome y Teenhome.

Clasificación de clientes según si fueron contactados previamente.

