# analysis-everpeak
Flujo de trabajo desarrollado
1. Carga y exploración de datos

Se importaron las librerías necesarias:

pandas
numpy
matplotlib
seaborn

Posteriormente se cargaron los archivos:

tomtom_traffic.csv
oecd_city_economy.csv

Durante esta etapa se revisó:

Estructura general de los DataFrames.
Tipos de datos.
Número de registros.
Presencia de valores nulos.
Consistencia de nombres y formatos.
2. Limpieza y preparación de datos
Estandarización de nombres

Se aplicó el formato snake_case para facilitar el manejo de variables.

Ejemplos:

Country → country
UpdateTimeUTC → update_time_utc
City GDP/capita → city_gdp_capita
Unemployment % → unemployment_pct
Conversión de fechas

Las columnas de fecha fueron convertidas a formato:

datetime64

para permitir operaciones temporales.

Conversión de variables numéricas

Se corrigieron:

Separadores decimales.
Separadores de miles.
Símbolos de porcentaje (%).

Esto permitió convertir correctamente las columnas a:

float
3. Filtrado temporal

A partir de la fecha de actualización del tráfico se extrajo el año:

traffic['year']

Posteriormente se filtraron únicamente los registros correspondientes al año:

2024

garantizando consistencia temporal entre ambas fuentes.

4. Agregación y resumen de movilidad

Debido a que TomTom contiene múltiples registros diarios por ciudad, fue necesario consolidar la información.

Se calcularon promedios anuales por:

city
country
year

para variables como:

jams_delay
traffic_index_live
jams_length_kms
jams_count
mins_delay
travel_time_live_per_10kms_mins
travel_time_hist_per_10kms_mins

El resultado fue una tabla resumida con una fila por ciudad-año.

5. Integración de datasets

Se seleccionaron las variables relevantes de ambas fuentes y se realizó una unión mediante:

pd.merge()

utilizando:

on=['city','year']

y

how='inner'

Esta integración permitió combinar indicadores de movilidad y economía en un único dataset analítico.

6. Análisis exploratorio y visualización

Se construyeron diferentes visualizaciones para identificar patrones y anomalías:

Boxplot

Utilizado para analizar:

Jams Delay

permitiendo identificar:

Mediana.
Promedio.
Valores atípicos (outliers).
Dispersión de los datos.
Histograma

Aplicado sobre:

PIB per cápita

para estudiar:

Distribución.
Concentración de valores.
Posibles sesgos.
Gráfico comparativo

Utilizado para comparar indicadores entre ciudades y observar diferencias en los niveles de congestión.

Hallazgos principales

Los resultados mostraron diferencias significativas en los niveles de congestión urbana entre las ciudades analizadas.

Las ciudades con mayores niveles promedio de retraso por tráfico fueron:

Ciudad de México
São Paulo
Bogotá
Lima

Estos resultados sugieren que la congestión continúa siendo un desafío importante para algunas de las principales áreas metropolitanas de América Latina.

Asimismo, el análisis evidenció que altos niveles de actividad económica no necesariamente se traducen en una movilidad eficiente, lo que indica la influencia de factores adicionales como infraestructura vial, transporte público, densidad poblacional y planificación urbana.

Notas técnicas aprendidas: 
Exploración de datos

Funciones utilizadas:

.head()
.info()
.describe()
.columns
.dtypes
Limpieza de datos

Funciones utilizadas:

.rename()
.astype()
.replace()
.to_datetime()
Filtrado de información

Funciones utilizadas:

.loc[]
.copy()
.dt.year
Agrupación y agregación

Funciones utilizadas:

.groupby()
.agg()
.mean()
.reset_index()
Integración de datos

Funciones utilizadas:

pd.merge()

Tipos de unión estudiados:

inner
left
right
outer
Visualización

Funciones utilizadas:

sns.boxplot()
sns.histplot()
plt.bar()
plt.title()
plt.xlabel()
plt.ylabel()
plt.xticks()
plt.show()
Resultado final

Se obtuvo un dataset consolidado denominado:

iadb_mobility_economy_2024_clean.csv

Este archivo contiene información integrada de movilidad urbana y productividad económica para el año 2024, lista para análisis estadísticos, visualizaciones avanzadas y procesos de toma de decisiones relacionados con transporte, desarrollo urbano y planificación territorial.
