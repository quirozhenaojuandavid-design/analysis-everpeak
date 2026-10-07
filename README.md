# 📊 Análisis de Movilidad Urbana y Economía — EverPeak

## 🇪🇸 ES Español

## Descripción del Proyecto

Este proyecto analiza la relación entre los indicadores de **movilidad urbana y actividad económica** en diferentes ciudades de América Latina durante el año 2024.

A partir de la integración de datos de tráfico urbano de **TomTom** e indicadores económicos de **OECD**, se realizó un proceso de exploración, limpieza, transformación, agregación e integración de datos para identificar patrones de congestión y analizar diferencias entre ciudades.

El análisis permitió construir un dataset consolidado con información de movilidad urbana y productividad económica, proporcionando una base para futuros análisis estadísticos y estudios relacionados con transporte, desarrollo urbano y planificación territorial.

## Objetivos del Proyecto

- Explorar y comprender la estructura de las fuentes de datos.
- Evaluar y mejorar la calidad de los datos disponibles.
- Estandarizar nombres y formatos de las variables.
- Garantizar consistencia temporal entre las diferentes fuentes.
- Consolidar los indicadores diarios de tráfico en promedios anuales por ciudad.
- Integrar indicadores de movilidad urbana y actividad económica.
- Identificar diferencias en los niveles de congestión entre ciudades.
- Generar visualizaciones para analizar distribuciones, variabilidad y valores atípicos.
- Obtener un dataset consolidado para futuros análisis de movilidad y desarrollo urbano.

## Datasets Utilizados

### `tomtom_traffic.csv`

Contiene información relacionada con indicadores de tráfico y movilidad urbana por ciudad.

Entre las principales variables utilizadas se encuentran:

- Ciudad
- País
- Fecha de actualización
- `jams_delay`
- `traffic_index_live`
- `jams_length_kms`
- `jams_count`
- `mins_delay`
- `travel_time_live_per_10kms_mins`
- `travel_time_hist_per_10kms_mins`

### `oecd_city_economy.csv`

Contiene indicadores relacionados con la actividad económica de las ciudades.

Entre las principales variables utilizadas se encuentran:

- Ciudad
- País
- PIB per cápita
- Tasa de desempleo
- Año

# Flujo de Trabajo

## 1. Carga y Exploración de Datos

Se importaron las librerías necesarias para el análisis:

- **Pandas**
- **NumPy**
- **Matplotlib**
- **Seaborn**

Posteriormente se cargaron los archivos:

- `tomtom_traffic.csv`
- `oecd_city_economy.csv`

Durante esta etapa se revisaron:

- Estructura general de los DataFrames.
- Tipos de datos.
- Número de registros.
- Presencia de valores nulos.
- Consistencia de nombres y formatos.

### Funciones utilizadas

```python
.head()
.info()
.describe()
.columns
.dtypes
Limpieza y Preparación de Datos
Estandarización de nombres
Se aplicó el formato snake_case para facilitar el manejo de las variables durante el análisis.
Algunos ejemplos:
Country → country
UpdateTimeUTC → update_time_utc
City → city
GDP/capita → city_gdp_capita
Unemployment % → unemployment_pct

Conversión de fechas
Las columnas de fecha fueron convertidas al formato:
datetime64

Esto permitió realizar operaciones temporales y extraer información relacionada con el año de cada registro.
Conversión de variables numéricas
Se corrigieron diferentes formatos relacionados con:
- Separadores decimales.
- Separadores de miles.
- Símbolos de porcentaje (%).
Posteriormente, las columnas fueron convertidas correctamente a formatos numéricos, principalmente:
float

Funciones utilizadas
.rename().astype().replace().to_datetime()


Filtrado Temporal
A partir de la fecha de actualización de los datos de tráfico se extrajo el año mediante:
traffic['year']


Posteriormente, se filtraron únicamente los registros correspondientes al año:
2024
Este procedimiento permitió garantizar la consistencia temporal entre las fuentes de movilidad y economía utilizadas en el análisis.
Funciones utilizadas
.loc[].copy().dt.year


Agregación y Resumen de Movilidad
Los datos de TomTom contenían múltiples registros diarios para cada ciudad.
Por esta razón, fue necesario consolidar la información mediante el cálculo de promedios anuales por:
- Ciudad
- País
- Año
Se calcularon promedios para diferentes indicadores de movilidad:
- jams_delay
- traffic_index_live
- jams_length_kms
- jams_count
- mins_delay
- travel_time_live_per_10kms_mins
- travel_time_hist_per_10kms_mins
El resultado fue una tabla resumida con una fila por ciudad-año.
Funciones utilizadas
.groupby().agg().mean().reset_index()


Integración de Datasets
Se seleccionaron las variables relevantes de ambas fuentes y se realizó una unión mediante:
pd.merge()


La integración se realizó utilizando:
on=['city', 'year']


y:
how='inner'


Esta integración permitió combinar indicadores de movilidad urbana y actividad económica en un único dataset analítico.
Tipos de unión estudiados
- Inner join
- Left join
- Right join
- Outer join
Análisis Exploratorio de Datos (EDA)
Una vez integradas las fuentes, se realizó un análisis exploratorio para identificar patrones, diferencias y posibles anomalías en los indicadores de movilidad y economía.
Boxplot — Jams Delay
Se utilizó un boxplot para analizar la variable:
Jams Delay
La visualización permitió observar:
- Mediana.
- Promedio.
- Dispersión de los datos.
- Valores atípicos (outliers).
Histograma — PIB per cápita
Se utilizó un histograma para estudiar la distribución del:
PIB per cápita
El análisis permitió observar:
- Distribución de los valores.
- Concentración de observaciones.
- Posibles sesgos.
- Variabilidad entre ciudades.
Gráfico Comparativo
Se construyeron gráficos comparativos para analizar las diferencias entre ciudades en los niveles de congestión urbana.
Funciones utilizadas
sns.boxplot()sns.histplot()plt.bar()plt.title()plt.xlabel()plt.ylabel()plt.xticks()plt.show()


Hallazgos Clave
Congestión Urbana
Los resultados mostraron diferencias significativas en los niveles promedio de congestión urbana entre las ciudades analizadas.
Las ciudades que presentaron mayores niveles promedio de retraso por tráfico fueron:
- Ciudad de México
- São Paulo
- Bogotá
- Lima
Estos resultados sugieren que la congestión continúa siendo un desafío importante para algunas de las principales áreas metropolitanas de América Latina.
Movilidad y Actividad Económica
El análisis evidenció que niveles elevados de actividad económica no necesariamente se traducen en una movilidad urbana más eficiente.
Esto indica que pueden existir otros factores asociados a los niveles de congestión, entre ellos:
- Infraestructura vial.
- Transporte público.
- Densidad poblacional.
- Planificación urbana.
Por lo tanto, los resultados proporcionan una base para desarrollar análisis posteriores sobre la relación entre desarrollo económico, movilidad y planificación urbana.
Resultado Final
Como resultado del proceso de limpieza, transformación, agregación e integración se obtuvo el dataset:
iadb_mobility_economy_2024_clean.csv

Este archivo contiene información integrada de movilidad urbana y productividad económica para el año 2024, preparada para futuros análisis estadísticos, visualizaciones avanzadas y procesos de toma de decisiones relacionados con:
- Transporte.
- Desarrollo urbano.
- Movilidad.
- Planificación territorial.
Notas Técnicas
Exploración de datos
Funciones utilizadas:
.head().info().describe().columns.dtypes


**2. Limpieza de datos**
Funciones utilizadas:
.rename().astype().replace().to_datetime()


Filtrado de información
Funciones utilizadas:
.loc[].copy().dt.year


Agrupación y agregación
Funciones utilizadas:
.groupby().agg().mean().reset_index()


Integración de datos
Función utilizada:
pd.merge()


Tipos de unión estudiados:
- Inner
- Left
- Right
- Outer
Visualización
Funciones utilizadas:
sns.boxplot()sns.histplot()plt.bar()plt.title()plt.xlabel()plt.ylabel()plt.xticks()plt.show()


Herramientas Utilizadas
- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Google Colab
- GitHub
Cómo Ejecutar el Proyecto
1. Clonar el repositorio
git clone [URL_DEL_REPOSITORIO]

2. Abrir el proyecto
Abrir el notebook en Google Colab o Jupyter Notebook.
3. Instalar las dependencias
pip install pandas numpy matplotlib seaborn

4. Ejecutar el notebook
Ejecutar las celdas en orden para reproducir el proceso de:
1. Exploración de datos.
2. Limpieza.
3. Transformación.
4. Filtrado temporal.
5. Agregación.
6. Integración de datasets.
7. Análisis exploratorio.
8. Visualización.
Autor
Juan David Quiroz Henao
Ingeniero Ambiental | Especialista en Derecho Ambiental | Data Analyst
Formación en Data Analytics — TripleTen

# 📊 Urban Mobility and Economic Analysis — EverPeak

## Project Description

This project analyzes the relationship between **urban mobility and economic activity indicators** across different Latin American cities during 2024.

Using urban traffic data from **TomTom** and economic indicators from **OECD**, a data exploration, cleaning, transformation, aggregation, and integration process was conducted to identify congestion patterns and analyze differences between cities.

The analysis resulted in a consolidated dataset containing urban mobility and economic productivity information, providing a foundation for further statistical analysis and studies related to transportation, urban development, and territorial planning.

## Project Objectives

- Explore and understand the structure of the available datasets.
- Evaluate and improve data quality.
- Standardize variable names and formats.
- Ensure temporal consistency across different data sources.
- Consolidate daily traffic indicators into annual city-level averages.
- Integrate urban mobility and economic activity indicators.
- Identify differences in congestion levels between cities.
- Create visualizations to analyze distributions, variability, and outliers.
- Produce a consolidated dataset for future mobility and urban development analysis.

## Datasets Used

### `tomtom_traffic.csv`

Contains information related to urban traffic and mobility indicators by city.

Main variables used include:

- City
- Country
- Update date
- `jams_delay`
- `traffic_index_live`
- `jams_length_kms`
- `jams_count`
- `mins_delay`
- `travel_time_live_per_10kms_mins`
- `travel_time_hist_per_10kms_mins`

### `oecd_city_economy.csv`

Contains economic indicators related to the analyzed cities.

Main variables used include:

- City
- Country
- GDP per capita
- Unemployment rate
- Year

# Workflow

## 1. Data Loading and Exploration

The following libraries were imported for the analysis:

- **Pandas**
- **NumPy**
- **Matplotlib**
- **Seaborn**

The following datasets were then loaded:

- `tomtom_traffic.csv`
- `oecd_city_economy.csv`

During this stage, the following aspects were reviewed:

- Overall DataFrame structure.
- Data types.
- Number of records.
- Missing values.
- Consistency of names and formats.

### Functions Used

```python
.head()
.info()
.describe()
.columns
.dtypes

Data Cleaning and Preparation
Column Name Standardization
The snake_case naming convention was applied to facilitate variable handling during the analysis.
Examples:
Country → country
UpdateTimeUTC → update_time_utc
City → city
GDP/capita → city_gdp_capita
Unemployment % → unemployment_pct

Date Conversion
Date columns were converted to:
datetime64

This allowed temporal operations and year extraction.
Numeric Variable Conversion
Formatting issues related to the following were corrected:
- Decimal separators.
- Thousands separators.
- Percentage symbols (%).
The variables were then converted to appropriate numeric formats, mainly:
float

Functions Used
.rename().astype().replace().to_datetime()


Time Filtering
The year was extracted from the traffic update date using:
traffic['year']


The dataset was then filtered to include only records corresponding to:
2024
This ensured temporal consistency between the mobility and economic datasets used in the analysis.
Functions Used
.loc[].copy().dt.year


Mobility Aggregation and Summary
The TomTom dataset contained multiple daily records for each city.
Therefore, the information was consolidated by calculating annual averages for:
- City
- Country
- Year
Annual averages were calculated for several mobility indicators:
- jams_delay
- traffic_index_live
- jams_length_kms
- jams_count
- mins_delay
- travel_time_live_per_10kms_mins
- travel_time_hist_per_10kms_mins
The resulting table contained one summarized record per city-year.
Functions Used
.groupby().agg().mean().reset_index()


Dataset Integration
Relevant variables from both sources were selected and combined using:
pd.merge()


The datasets were merged using:
on=['city', 'year']


and:
how='inner'


This integration combined urban mobility and economic activity indicators into a single analytical dataset.
Join Types Studied
- Inner join
- Left join
- Right join
- Outer join
Exploratory Data Analysis (EDA)
Once the datasets were integrated, an exploratory analysis was performed to identify patterns, differences, and potential anomalies across mobility and economic indicators.
Boxplot — Jams Delay
A boxplot was used to analyze:
Jams Delay
The visualization allowed the analysis of:
- Median.
- Mean.
- Data dispersion.
- Outliers.
Histogram — GDP per Capita
A histogram was used to analyze the distribution of:
GDP per capita
The analysis helped evaluate:
- Distribution.
- Concentration of observations.
- Potential skewness.
- Variability between cities.
Comparative Chart
Comparative charts were created to examine differences in urban congestion levels across the analyzed cities.
Functions Used
sns.boxplot()sns.histplot()plt.bar()plt.title()plt.xlabel()plt.ylabel()plt.xticks()plt.show()


Key Findings
Urban Congestion
The results showed significant differences in average urban congestion levels across the analyzed cities.
The cities with the highest average traffic delay levels were:
- Mexico City
- São Paulo
- Bogotá
- Lima
These results suggest that congestion remains a significant challenge for some of the largest metropolitan areas in Latin America.
Mobility and Economic Activity
The analysis showed that higher levels of economic activity do not necessarily translate into more efficient urban mobility.
This indicates that other factors may influence congestion levels, including:
- Road infrastructure.
- Public transportation.
- Population density.
- Urban planning.
These findings provide a foundation for further analysis of the relationship between economic development, mobility, and urban planning.
Final Result
The data cleaning, transformation, aggregation, and integration process resulted in the following consolidated dataset:
iadb_mobility_economy_2024_clean.csv

This file contains integrated information on urban mobility and economic productivity for 2024, prepared for further statistical analysis, advanced visualization, and decision-making processes related to:
- Transportation.
- Urban development.
- Mobility.
- Territorial planning.
Technical Notes
Data Exploration
Functions used:
.head().info().describe().columns.dtypes


Data Cleaning
Functions used:
.rename().astype().replace().to_datetime()


Data Filtering
Functions used:
.loc[].copy().dt.year


Grouping and Aggregation
Functions used:
.groupby().agg().mean().reset_index()


Data Integration
Function used:
pd.merge()


Join types studied:
- Inner
- Left
- Right
- Outer
Visualization
Functions used:
sns.boxplot()sns.histplot()plt.bar()plt.title()plt.xlabel()plt.ylabel()plt.xticks()plt.show()


Tools Used
- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Google Colab
- GitHub
How to Run the Project
1. Clone the Repository
git clone [REPOSITORY_URL]

2. Open the Project
Open the notebook using Google Colab or Jupyter Notebook.
3. Install Dependencies
pip install pandas numpy matplotlib seaborn

4. Run the Notebook
Run the notebook cells in order to reproduce the following workflow:
1. Data exploration.
2. Data cleaning.
3. Data transformation.
4. Time filtering.
5. Data aggregation.
6. Dataset integration.
7. Exploratory data analysis.
8. Data visualization.
Author
Juan David Quiroz Henao
Environmental Engineer | Environmental Law Specialist | Data Analyst
Data Analytics Training — TripleTen
```
