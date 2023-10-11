## Accidentes aéreos

 Hola!

 Este proyecto tiene como objetivo responder cuales son los principales factores que se encuentran involucrados en los incidentes aéreos desde 1908(17/sept.) hasta 2021(06/jul.).
 En el presente documento se ejecutaron diferentes tecnologías y herramientas para llegar a su fin, tales como :
 - Python (Matplotlib, Seaborn, Pandas y Numpy)
 - Power BI (DAX)
 - GitHub

 # Descripción del proyecto:

## Análisis exploratorio de los datos (EDA):

 Se tomó una base de datos de acceso público de la Organización de Aviación Civil Internacional (OACI) la cual cuenta con registros de más de 100 años de incidentes aéreos alrededor del mundo.
 Inicialmente se procede a realizar una primera aproximación al set de datos, en donde se encuentra que existen muchos valores desconocidos (?) pero que de alguna manera pueden llegar a representar una utilidad debido a que otorgan información parcial sobre algún aspecto de interés del estudio.

## Proceso de ETL
 Se realizan transformaciones a ciertas columnas con el objetivo de que faciliten el análisis posteriormente realizado en Power BI. Por tanto se escogen únicamente columnas como fecha, hora, ruta, operador, tipo de vuelo, tipo de aeronave, total de personas a bordo, pasajeros, tripulación, muertes totales, muertes de pasajeros, muertes de tripulación y bajas en tierra.

 - El siguiente paso realizado dentro del análisis es realizar modificaciones a columnas como Hora, con el fin de tomar únicamente valores que tuvieron lugar entre HH:01 y HH:59 para reducir el tamaño de las categorías a estudiar, obteniendo solamente 25 categorías, explicadas en el archivo 'ETL accidentes aereos.ipynb'. 

 - La columna fecha requiere de una normalización, dado que los datos no presentan una estructura homogénea para poder trabajarla en formato dd/mm/aaaa en Power BI, por tal motivo se ejecutan dichos cambios.

- La columna tipo de aeronave presenta 2469 valores únicos, por tanto se identifican los valores con mayores repeticiones con el fin de tenerlos en cuenta para un análisis posterior.

- Para tipo de vuelo, se toma en cuenta la estrategia del item anterior, dado que existen 3839 valores sin repetir, a pesar de esto es importante resaltar que el valor con mayores repeticiones en el dataset es un valor desconocido con 762 repeticiones, seguido de vuelos de entrenamiento y vuelos de avistamiento. Por otro lado, esta columna no presenta una alta calidad en los datos, dado que también se presentan rutas (i.e. Rio de Janeiro - Sao Paulo) restando valor a la información depositada en esta columna.

- Los operadores de los vuelos son un total 2268 distintos y se tuvieron en cuenta los más representativos para el posterior análisis.

- Para obtener la ubicación de los incidentes, se recurre a la columna Ruta y se realiza una extracción de la información pertinente, dado que esta columna ruta presentaba información como ciudad y en algunos casos, región, las cuales eran irrelevantes para el análisis que se realizaría posteriormente. Por tanto se extrae únicamente la información del páis donde ocurrió el accidente. Sin embargo esta columna es la que mayor limpieza requierió, debido a que se presentan typos que dificultan ejecutar reglas generales de limpieza de datos y se deben tratar 1 a 1.

- Por último se generan algunas medidas estadísticas para poder identificar valores atípicos, no obstante esto es únicamente informativo debido a que en este análisis se priorizó la información publicada oficialmente sobre cualquier otro criterio, principalmente debido a que si bien se encuentran valores atípicos, es el registro oficial y considero este criterio superior.

## Análisis del ETL y EDA:

Distribución de accidentes por número de personas a bordo
![grafico de distribución desde ETL](./Distribución%20total%20de%20personas%20a%20bordo.png)

Distribución de accidentes por número de muertes totales
![grafico de distribución desde ETL](./Distribucion%20muertes%20totales.png)


Se evidencia que las muertes de los pasajeroes es mucho menos probable que las muertes de los tripulantes, dado que no todos los vuelos necesaiamente llevan pasajeros, pero virtualmente todos los vuelos deben llevar por lo menos 1 tripulante y este se trataría del piloto de la aeronave.
Si bien se pueden tratar de vuelos donde no hay pasajeros y esto correspondería a vuelos de cargamento, vuelos militares, vuelos de reconocimiento, pero no vuelos turísticos y/o comerciales donde se espera que exista la presencia de muchos más pasajeros.

Se ejecutó otro análisis exploratorio para poder determinar si existía correlación entre las variables hora, muertes totales y el top 10 de los países con más número de accidentes aéreos.

![Heatmap hora-top10-muertes](./heatmap.png)


