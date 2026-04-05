# proyecto_EDA_python
Proyecto EDA de Python para el bootcamp de Analisis de Datos de ThePower Education

Análisis Exploratorio de Datos - Campañas de Marketing Bancario

1. Propósito del Proyecto

Este proyecto consiste en un Análisis Exploratorio de Datos (EDA) sobre las campañas de marketing directo de una institución bancaria portuguesa. El objetivo principal es identificar el perfil del cliente que suscribe depósitos a plazo y entender qué factores (económicos, temporales o de contacto) influyen en el éxito de la conversión.

2. Estructura del Repositorio

data/: Contiene los archivos originales en la carpeta "RAW" (bank-additional.csv, customer-details.xlsx) y los archivos procesados en la carpeta "Procesado" (bank.additional-clean.csv, customer-details-clean.csv, tablas_limpias.csv).

notebooks/: Jupyter Notebook con el código de limpieza, transformación y visualización.

README.md: Informe detallado del proyecto y conclusiones.

3. Pasos para ejecutar el proyecto

    1. Clonar el repositorio de GitHub donde se encuentra el proyecto.
    2. Abrir la carpeta con el proyecto en VSC.
    3. Crear un entorno virtual.
    4. Instalar librerias desde la terminal utilizando pip install (pandas, matplotlib, seaborn, openpyxl).
    5. Ejecutar el notebook (analisis_eda.ipynb).

4. Proceso de Transformación y Limpieza

Se realizaron las siguientes acciones para garantizar la calidad de los datos y poder realizar un análisis de forma correcta y organizada:

- Importación de librerias y de BBDD: se importan las librerias a utilizar durante el proyecto (pandas, matplotlib y seaborn) y se cargan las BBDD para explorar, limpiar y analizar.

- Exploración de los datos inicial: se realiza la exploración inicial con funciones como columns, head, info, shape, describe y se verifica la presencia de valores duplicados (duplicated) y nulos (isnull).

- Limpieza de datos: se realiza limpieza de las BBDD para su correcta exploración, para ello se eliminaron las columnas innecesarias, se renombraron algunas columnas, se convirtieron valores tipo objects en valores binarios numéricos, se corrigieron los formatos de los valores, etc.

- Tratamiento de Nulos y Outliers: se tratan los valores nulos y outliers identificados en el punto anterior, para ello, se utilizaron diferentes herramientas y recursos tales como:

   - Marital: se rellenaron los valores nulos con la moda, ya que únicamente eran 85 los valores nulos.
   - Age: para rellenar los valores nulos de "age", utilicé la función transform de pandas para aplicar una función lambda que rellena los valores faltantes con la mediana de "age" dentro de cada grupo de "marital". De esta manera, los valores nulos en "age" se rellenan de manera más precisa, teniendo en cuenta la relación entre el estado civil y la edad.
   - Job y Education: para menajar los nulos de "job" y "education" decidí reemplazarlos por la palabra "unknown", ya que consideraba necesario mantener esos valores como desconocidos y no eliminar dichas filas para no perder información valiosa ni inventar ningún dato que pudiera dar información errónea.
   - Default, housing y loan: para tratar los nulos de dichas categorias, decidí rellenarlos con -1, ya que son variables binarias y no quiero introducir una categoría adicional como "unknown", además de que -1 me permitirá identificarlos fácilmente en el análisis posterior.
   - Cons.price.idx: para manejar los nulos, decidí rellenarlos con la media de la columna, ya que no son muchos nulos y la media es una buena opción para este tipo de variable numérica continua.
   - Date: para manejar los nulos de dicha columna, al ser un dato importante para el análisis temporal, y al ser tan poco nulos (248 nulos, el 0.5% del total de filas), decidí eliminar las filas que contienen nulos en esta columna, ya que no afectará significativamente el análisis y me permitirá trabajar con datos completos en las fechas.
   - Euribor3m: para manejar los nulos en la columna, decidí rellenarlos con el último valor conocido, ordenando primero de forma descendente la columna "cons.price.idx", ya que están relacionados ambos datos.

5. Guardar archivos limpios: una vez finalizada la limpieza, se guardaron los datasets en su versión procesada para facilitar su reutilización en futuros análisis. Además, se realizó la unión de ambas tablas mediante la columna ID, lo que permitió integrar la información y llevar a cabo análisis y visualizaciones que relacionan variables de ambos conjuntos de datos. Dicha tabla, también fue guardada en la carpeta de "Procesado".

6. EDA (Análisis Exploratorio de Datos): Una vez finalizada la limpieza y almacenados los datasets procesados, se llevó a cabo el análisis exploratorio de los datos. Para ello, se utilizaron distintos tipos de visualizaciones, como countplots, histograms, boxplots, heatmaps, lineplot y violin plots, entre otros, con el objetivo de identificar patrones, relaciones y tendencias relevantes en la información.

A partir de este análisis, se obtuvieron las siguientes conclusiones:

A. Correlaciones y Factores Económicos
El mapa de calor reveló que la duración de la llamada es el factor interno con mayor correlación positiva con la conversión. En el ámbito macroeconómico, el Euribor a 3 meses muestra una fuerte relación inversa: a menor tasa de interés, mayor es la probabilidad de que el cliente contrate el producto.  Por otro lado, también vemos una relación inversamente proporcional muy fuerte entre el pday y la conversión, cuantos menos días pasaron desde el último contacto, mayor es la probabilidad de éxito.

B. Duración de la Interacción (duration)
La duración de la última llamada es unos de los factores internos más determinante del éxito. El mapa de calor muestra una correlación de 0.41 con la conversión. Los diagramas de caja (boxplots) y violín confirman que la mediana de tiempo es significativamente superior en los casos de éxito. Existe un "umbral de conversión" identificado en los gráficos de barras apiladas: las llamadas menores a 60 segundos tienen éxito nulo. Sin embargo, en el segmento de >15 minutos, la tasa de éxito supera el 50%. La duración no es un gasto, sino una inversión. Las llamadas largas indican un proceso de persuasión efectivo que el banco debe incentivar.

C. Análisis de Recencia (pdays)
El análisis de los días transcurridos desde el último contacto revela una diferencia muy grande entre captación y retención. El valor 999 (clientes nuevos, nunca antes contactados) domina el volumen del dataset pero presenta la tasa de conversión más baja. En contraste, los clientes re-contactados en menos de 27 días muestran tasas de éxito masivas (visto en los gráficos de barras de proporción). La familiaridad con la marca y el seguimiento oportuno reducen la fricción de venta. Un cliente que ya conoce el producto tiene una probabilidad de conversión hasta 5 veces mayor que uno contactado por primera vez.

D. Influencia del Contexto Macroeconómico (euribor3m)
El éxito de la campaña está condicionado por el entorno financiero externo. El boxplot de euribor3m muestra que las conversiones exitosas se concentran cuando el tipo de interés está cerca del 1.3%. Por el contrario, los rechazos masivos ocurren con tasas cercanas al 4.8%. En entornos de tipos bajos, los productos de ahorro tradicionales se vuelven más atractivos o el coste de oportunidad para el cliente es menor. El banco es más eficiente cuando el mercado financiero es estable y con tasas moderadas.

E. Patrones Temporales y Estacionales (date)
La evolución histórica (2015-2019) permite planificar la carga de trabajo. Los gráficos lineales por año muestran una estacionalidad cíclica. El mes de Octubre destaca consistentemente como un periodo de alta conversión, mientras que Septiembre suele registrar los valles de rendimiento. El comportamiento de compra sigue ciclos anuales. La estabilidad de la conversión (entre el 9% y 14%) a pesar de los años indica un modelo de negocio sólido pero dependiente del calendario.

F. Perfil del Cliente
Edad: El volumen más alto de conversiones exitosas se concentra en el rango de 28 a 42 años. Este segmento muestra la mayor densidad de puntos naranjas en los gráficos de dispersión y las barras de frecuencia más altas para Conversion=1.Existe un segundo repunte de efectividad en los clientes mayores de 60 años (visto en el scatter plot y boxplot de edad). Aunque representan un volumen total menor, su tasa de conversión es proporcionalmente alta.

Hijos e ingresos: La cantidad de hijos y los ingresos no son un factor determinante a tener en cuenta a la hora de dirigir la campaña a cierto grupo de la población, ya que no hay una correlación directa entre los hijos y la conversión, ni entre los ingresos y la conversión, tal y como podemos identificar en el gráfico boxplot que relaciona la cantidad de hijos (suma entre kidhome y teenhome) con la conversión y el que relaciona la misma con los ingresos.

Ocupación: en el gráfico de countplot que relaciona la conversión con la columna de "job" podemos ver que la conversión es muy alta en personas con ocupación de administrador, técnico y trabajadores manuales. Sin embargo, también representan las categorias donde mayor tasa de participación hubo. Es por ello, que se calculó la tasa de conversión por ocupación y la misma muestra que los estudiantes y jubilados presentan las tasas de conversión más altas, aunque con menor volumen de clientes. Por otro lado, perfiles como administrativos y técnicos, aunque con tasas de conversión moderadas, representan los segmentos más relevantes en términos absolutos debido a su gran volumen. Finalmente, grupos como trabajadores manuales y servicios muestran baja eficiencia, ya que concentran muchos contactos pero generan pocas conversiones, lo que indica una posible necesidad de optimizar o reducir esfuerzos en estos segmentos.

7. Conclusiones Fundamentadas y Recomendaciones

Tras un exhaustivo análisis exploratorio de los datos, se concluye que el éxito en la suscripción de depósitos a plazo no depende de un único factor aisladamente, sino de una interacción crítica entre la gestión operativa y el contexto externo.

Desde una perspectiva operativa, la duración de la interacción y la recencia del contacto (pdays) han demostrado ser los pilares del éxito; la capacidad de retener al cliente en una conversación de calidad (superior a los 5 minutos) y la implementación de una estrategia de seguimiento en periodos menores a 30 días multiplican exponencialmente las probabilidades de conversión frente a los contactos "fríos".

A nivel macroeconómico, se evidencia una sensibilidad directa al mercado: entornos con un Euribor bajo favorecen la captación de depósitos, lo que permite al banco sincronizar sus campañas más agresivas con estos periodos de oportunidad. Finalmente, aunque variables como el nivel de ingresos o la carga familiar no han mostrado un peso determinante, la segmentación por ocupación y edad permite diferenciar entre un segmento de alto volumen operativo y un nicho de alta eficiencia.

En definitiva, para maximizar la conversión de futuras campañas, se debe transicionar de un modelo de contacto masivo hacia una estrategia de precisión, priorizando el seguimiento oportuno, la calidad de la llamada y la alineación con los indicadores económicos del mercado.

Los clientes objetivos se podrían dividir en dos grandes grupos:

    A. El Cliente de Volumen (Rentabilidad por Cantidad)
Edad: Adultos jóvenes de 28 a 42 años.
Ocupación: Administrativos y Técnicos. Aunque su tasa de éxito es moderada, representan el grueso de las conversiones totales por su alta participación.
Situación Familiar: Indiferente (ya que confirmamos que los hijos no discriminan el éxito), aunque el volumen tiende a concentrarse en hogares con 0 o 1 hijo.

    B. El Cliente de Eficiencia (Rentabilidad por Calidad)
Edad: Adultos mayores de 60 años.
Ocupación: Jubilados. Tienen las tasas de conversión más altas del dataset; es decir, de cada 10 llamadas a este grupo, "sí" responden muchas más que en otros grupos.
Situación Familiar: Perfiles con mayor capacidad de ahorro percibida (asociado a la etapa vital de jubilación).








