# S10----PRUEBA-A-B-TIENDA-ONLINE
Lanzamiento y análisis de prueba A/B para una tienda online. Framework priorización de hipótesis, métricas acumuladas, percentiles y método estadístico Mann-Whitney. 

## Descripción
Lanzamiento y análisis de prueba A/B para una tienda online.

Uso de frameworks para priorizar hipótesis se apoya la decisión de qué prueba A/B lanzar.
Cálculo de metricas acumuladas nos permite ir revisando los progresos de la prueba reduciendo el "Peeking problem", algunas metricas significativas son: 
* ingreso acumulado,
* tamaño de pedido acumulado,
* diferencia relativa en el tamaño de pedido,
*  tasa de conversión de cada grupo.
Cálculo de percentiles y gráficas de dispersión para la identificar valores atípicos. Percentil 99, indica cual es el valor a partir del cual se encuentra solo el 1% de la muestra.
Método de Mann-Whitney para conocer la significaca estadística de la diferencia entre dos poblaciones.


## Herramientas utilizadas
![Python](https://img.shields.io/badge/:Python-024A86?style=for-the-badge&logo=python&logoColor=white&labelColor=101010)</br>
![Matplotlib](https://img.shields.io/badge/Matplotlib-%23ffffff.svg?style=for-the-badge&logo=Matplotlib&logoColor=black)
![NumPy](https://img.shields.io/badge/numpy-%23013243.svg?style=for-the-badge&logo=numpy&logoColor=white)
![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=for-the-badge&logo=pandas&logoColor=white)
![Plotly](https://img.shields.io/badge/Plotly-%233F4F75.svg?style=for-the-badge&logo=plotly&logoColor=white)
![Seaborn](https://img.shields.io/badge/seaborn-%233F4F75.svg?style=for-the-badge&logo=seaborn&logoColor=white)
![SciPy](https://img.shields.io/badge/SciPy-%230C55A5.svg?style=for-the-badge&logo=scipy&logoColor=%white)
![Datetime](https://img.shields.io/badge/datetime-%233F4F75.svg?style=for-the-badge&logo=datetime&logoColor=white)

![Colab](https://img.shields.io/badge/Colab-F9AB00?style=for-the-badge&logo=googlecolab&color=525252)
![Jupyter Notebook](https://img.shields.io/badge/jupyter-%23FA0F00.svg?style=for-the-badge&logo=jupyter&logoColor=white)


## Conclusiones
Se comprueba que los cambios realizados fueron efectivos y el  grupo B como se posiciona como líder. 

A lo largo de los análisis se observa que aunque no hay grandes diferencia en el tamaño promedio de compra entre los grupos, sí hay una clara diferencia en la tasa de conversión siendo mayor la del grupo B; lo cual también incrementa las ganancias que tiene la empresa.


## Profundización técnica
* Exploración datos:
* *  Importación de datos - pd.read_csv('',sep=';')
  *   Nombres de columnas en snake_case
  *   Exploración de datasets - .info(), display(df.head())
  *   Revisión de tipos de datos, valores ausentes y duplicados. - df['col'] = df['col'].map( lambda x: dt.datetime.strptime( x, '%Y-%m-%d'))
  *   Manejo de dataframes - df1 = df.drop(['col1', 'col2', 'col3'], axis=1).groupby('col4', as_index=False).agg({'col5' : pd.Series.nunique}), df.columns=[''.'']
* Lanzamiento de pruebas A/B :
* * Frameworks para priorizar hipótesis :
* * * ICE = (Impacto * Confianza) / Esfuerzo
    * RICE = (Alcance * Impacto * Confianza) / Esfuerzo
* * Análisis de test A/B :
  * * Asegurar que no haya usuarios repetidos en el grupo A y grupo B.
    * Uso de Métricas Acumuladas para evitar "Peeking problem" - por grupo : ingreso acumulado, tamaño de pedido acumulado, diferencia relativa en el tamaño de pedido, tasa de conversión de cada grupo. 
    * * Mariz valores únicos por fecha-grupo : datesGroups = orders[['date','group']].drop_duplicates()
      * Métrica acumulada - varAggregated = datesGroups.apply(lambda x: visits[np.logical_and(visits['date'] <= x['date'], visits['group'] == x['group'])]
    .agg({'date' : 'max', 'group' : 'max', 'visits' : 'sum'}), axis=1).sort_values(by=['date','group'])
* Revisión de valores atípicos:
* * Cálculo de percentiles - np.percentile(df['col'],[95.99]) - Percentil: valor desde el cual se
  * Gráficas de dispersión
  * Eliminar datos atípicos
* Significacia estadística de la diferencia entre los grupos
* * Método de ManWhitney - stats.mannwhitneyu(sampleA, sampleB)[1]
  * Ganancia relativa para el grupo B - sampleB.mean()/sampleA.mean()-1
