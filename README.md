Análisis de Ventas y Tendencias en la Industria de Videojuegos

Este proyecto de análisis de datos realiza una investigación exhaustiva del mercado global de videojuegos a partir de un dataset histórico con más de 16,000 registros. A través de un pipeline completo de procesamiento de datos (EDAs) y análisis estadístico, se identifican los patrones de éxito, ciclos de vida de las plataformas, preferencias regionales de los consumidores y la correlación entre las evaluaciones cuantitativas de la crítica/usuarios con el desempeño comercial de los títulos.

El objetivo central es transformar datos brutos en insights accionables para la toma de decisiones estratégicas, emulando el proceso de consultoría e inteligencia de negocios que un Data Analyst / Data Scientist Junior ejecuta en entornos corporativos.

Tecnologías y Librerías Utilizadas

Python 3.10+ (Siguiendo estándares de código limpio PEP 8 y alta puntuación en Pylint)

Pandas & NumPy: Manipulación de estructuras de datos, imputación avanzada y agregaciones vectoriales.

Matplotlib & Seaborn: Visualización de datos y diseño de dashboards estadísticos detallados.

SciPy (stats): Computación estadística robusta y pruebas de hipótesis.

Regex (re): Minería de texto para la recuperación y parseo de datos temporales ausentes.

Estructura del Dataset Original

El conjunto de datos (games.csv) cuenta originalmente con 11 columnas e incluye información crítica de ventas dividida por regiones:

name & genre: Identificadores categóricos del videojuego.

platform & year_of_release: Entorno tecnológico e indicador temporal.

na_sales, eu_sales, jp_sales, other_sales: Ventas en millones de USD para Norteamérica, Europa, Japón y otros mercados, respectivamente.

critic_score & user_score: Puntuaciones de calidad por expertos (escala de 100) y audiencias (escala de 10).

rating: Clasificación de contenido ESRB.

Procesamiento de Datos y Rigor Metodológico

Una de las etapas más valoradas por los reclutadores es el tratamiento estratégico de la calidad de los datos. En este proyecto se implementaron las siguientes soluciones analíticas:

1. Estandarización de Nomenclatura

Se aplicó de forma automatizada el formato snake_case a todas las variables del DataFrame para garantizar una sintaxis consistente, eliminando espacios espurios y caracteres en mayúsculas:

df.columns = df.columns.str.strip().str.replace(" ", "_").str.lower()

2. Recuperación e Imputación Avanzada de Valores Ausentes
Columna name y genre: Se detectaron únicamente 2 registros nulos (0.012% del dataset). Debido a la imposibilidad lógica de inferir un nombre comercial y al impacto estadístico nulo, se procedió a su eliminación selectiva para mantener la integridad regulatoria del set.

Columna year_of_release: En lugar de eliminar directamente los 269 registros nulos iniciales, se desarrolló una función basada en Expresiones Regulares (Regex) para escanear y extraer el año implícito en el nombre de aquellos videojuegos que lo incluían de forma nativa (ej. Madden NFL 2004). Los registros residuales irrecuperables se eliminaron selectivamente.

3. Optimización y Conversión de Tipos de Datos
year_of_release (De float64 a int64): Al no contar con granularidad de mes o día, el formato datetime generaría ruido analítico. La transformación a entero (int) optimiza el uso de memoria en producción y facilita los filtros de rangos temporales.

user_score (De object a float64): Se identificó la presencia de la cadena 'TBD' (To Be Determined) mezclada con puntuaciones decimales, lo que bloqueaba cualquier operación matemática. Se forzó numéricamente transformando los strings no cuantitativos a valores NaN mediante pd.to_numeric(errors='coerce'), habilitando de este modo el cálculo de métricas como medias, medianas y coeficientes de correlación.

4. Enriquecimiento del Dataset (Feature Engineering)
Se computó una nueva variable métrica macroeconómica (total_sales) sumando el rendimiento financiero global de cada título:

df["total_sales"] = df["na_sales"] + df["eu_sales"] + df["jp_sales"] + df["other_sales"]

Hallazgos Clave del Análisis Exploratorio (EDA)

Evolución Histórica: El volumen de lanzamientos por año experimentó un crecimiento exponencial a partir de mediados de los 90, alcanzando su pico máximo entre 2008 y 2009 con más de 1,400 títulos anuales, seguido de una estabilización impulsada por la transición digital y los juegos como servicio.

Ciclo de Vida Tecnológico: El análisis de distribución temporal revela que las plataformas líderes de la industria tienen una vida útil comercial promedio en el mercado de 5 a 7 años antes de ser reemplazadas por hardware de nueva generación.

Métricas Descriptivas: Aunque la media de ventas globales por juego se ubica en el espectro bajo, la presencia de "Mega-Hits" de distribución asimétrica (como Wii Sports con 82.54 millones de copias) genera una desviación estándar alta, lo que demuestra que la industria depende altamente de éxitos taquilleros.

Pruebas de Hipótesis Estadísticas (Scipy)

(Nota: En esta sección puedes detallar las pruebas t de Student, p-values y los niveles de significancia alfa que ejecutaste en tu notebook para comprobar los efectos del clima, plataformas o géneros sobre el comportamiento de compra de los usuarios, demostrando tu dominio matemático).

Conclusiones de Negocio

Modelos de Negocio Basados en Datos: Las distribuciones asimétricas positivas en las ventas indican que los recursos de marketing deben concentrarse fuertemente en títulos con altas evaluaciones tempranas de la crítica, ya que el coeficiente de correlación demuestra una tracción comercial directa.

Segmentación Regional: Los comportamientos de consumo difieren drásticamente entre las regiones analizadas, lo que exige una diversificación de portafolio y estrategias de localización específicas para mercados clave como Asia frente a Occidente.

Cómo Ejecutar el Proyecto

Clona este repositorio:

Bash
git clone https://github.com/tu-usuario/nombre-del-repositorio.git
2. Instala las dependencias requeridas:
   ```bash
pip install -r requirements.txt
Abre y ejecuta el archivo Jupyter Notebook:

Bash
jupyter notebook analisis_videojuegos.ipynb