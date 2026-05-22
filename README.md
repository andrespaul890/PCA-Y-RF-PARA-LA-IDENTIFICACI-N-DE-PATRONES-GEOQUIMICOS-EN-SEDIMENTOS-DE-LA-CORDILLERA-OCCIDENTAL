# INTEGRACIÓN DEL ANÁLISIS DE COMPONENTES PRINCIPALES Y RANDOM FOREST PARA LA IDENTIFICACIÓN DE PATRONES GEOQUÍMICOS EN SEDIMENTOS FLUVIALES DE LA CORDILLERA OCCIDENTAL DEL ECUADOR

**Maestría en Inteligencia de Negocios y Ciencia de Datos — UDLA**  
**Autor:** Andrés Paul Villacís Maita  
**Año:** 2026

---

## Tabla de Contenidos

1. [Descripción del Proyecto](#descripción-del-proyecto)
2. [Estructura del Repositorio](#estructura-del-repositorio)
3. [Sobre los Datos](#sobre-los-datos)
4. [Descripción del Notebook](#descripción-del-notebook)
5. [Cómo Replicarlo](#cómo-replicarlo)
6. [Resultados Obtenidos](#resultados-obtenidos)
7. [Referencias](#referencias)

---

## Descripción del Proyecto
El presente repositorio contiene los pasos para realizar un análisis CON PCA Y RANDOM FOREST para la determinación de zona anomálicas durante la exploración mineral.
Esta investigación desarrolla una metodología para analizar datos geoquímicos de sedimentos fluviales en la Cordillera Occidental del Ecuador, integrando técnicas de datos composicionales (CoDa) y aprendizaje automático no supervisado. El problema central radica en la subutilización de bases de datos masivas y la naturaleza relativa de la geoquímica, que puede generar correlaciones espurias si se analiza con métodos tradicionales.

El PCA mediante el PC1 logra identificar las firmas para cada una de las fajas metalogénicas del Ecuador
| Faja | Firma	| Rasgo diferencial |
|------|--------|-------------------|
|1	Cretácico VMS CuAuAg |	Cu–Zn–Au–Pb–As	| VMS clásico con fuerte componente de metales base |
|2	Paleoceno Eoceno VMS CuAuAg	| Cu–Au–Zn–Pb–Mo	| VMS más heterogéneo y con mayor componente aurífero |
|3	Oligoceno-Mioceno Epitermales Au-Cu	| As–Pb–Hg–Sb–Au	|Firma epitermal más diagnóstica y contrastada |
|4	Mioceno Pórfidos CuMoAu	| Pb–As–Au–Sb–Mo	|Halo hidrotermal/pórfido más difuso |

---

## Sobre los datos
La base de datos correspondiente al presente estudio es de tipo pagada y puede ser condeguirda directamente al Instituto de Investigación Geológico y Energético – Ecuador

### Para replicar el análisis
Se deberá tener un archivo .csv o .xlsx con datos de ensayos geoquímicos. 

#### Para añadir la columna de "Fajas Metalogénicas"
- la base de datos original no contiene la columna que indicá a que Faja metalogénica pertenece cada punto de muestreo, por lo tanto tiene que ser agregada.
- En un software de GIS cargar los .shp con las fajas metalogénicas del mapa del Ecuador.
- Cargar el archivo con la base de datos de puntos con las coordenadas x, y, z.
- Ejecutar las herramientas de análisis GIS para asignar la Faja Metalogénica a cada uno de los puntos.
- Exportar la base de datos modificada.

## Descripción del Notebook
- Importación de librerías
- Carga de base de dato
- Analisis de tipo de datos
- Estadística descriptiva
- Visualización de variables
- Transformación de variables
- LImpieza de variables
- Instalación de librearias para proyección espacial de datos
- Instalación de librearias para CLR y PCA
- Transforación de coordenadas para proyección espacial
- Aplicacion del PCA aplicado por Faja Metalogénica
- Entrenamiento de Random Forest
- Análisis de métricas
- RF para toda la bse y para elementos mineralizantes
- Analisis se sensibilidad 
- Analisis AUC-Roc

## Cómo Replicarlo
### Google Colab
1. En Google Colab subir el notebook `PCA-RF_Analisis de datos Geoquimicos.ipynb`.
2. Subir el archivo de la base de datos modificada a Google Drive
3. Ejecutar el cuaderno

---

## Resultados Obtenidos
FAJA: Cretacico_VMS_Cu-Au-Ag 
- Número de muestras: 2469
- Varianza explicada acumulada:
[0.21678017 0.34816869 0.47462185 0.56500197 0.63212856 0.69044159
 0.74209252 0.7783878  0.80718998 0.83302972]

FAJA: Mioceno_Porfidos-Cu-Mo-Au 
- Número de muestras: 3069
- Varianza explicada acumulada:
[0.23924379 0.36325176 0.45176915 0.53382311 0.60335694 0.65443712
 0.70002196 0.73961778 0.77132132 0.79805611]
 
FAJA: Oligoceno-Mioceno_Epitermales-Au-Cu 
- Número de muestras: 5383
- Varianza explicada acumulada:
[0.2951103  0.4202515  0.50393793 0.57599434 0.63596891 0.68195883
 0.72166911 0.75580496 0.78496028 0.8132731 ]
 
FAJA: Paleoceno-Eoceno_VMS_Cu-Au-Ag 
- Número de muestras: 2232
- Varianza explicada acumulada:
[0.14731756 0.27457621 0.38574526 0.49141598 0.57585981 0.6370395
 0.68456455 0.72722664 0.76454972 0.79927615]


RESUMEN COMPARATIVO BALANCEADO VS NO BALANCEADO

|Faja	|Modelo|Accuracy|Precision_True	|Recall_True	|F1_True	|Support_True	|Precision_False	|Recall_False	|F1_False|
|-----|------|--------|---------------|-------------|---------|-------------|-----------------|-------------|--------|
|0	Cretacico_VMS_Cu-Au-Ag	|No balanceado	|0.967611	|0.846154	|0.440000	|0.578947	|25.0	|0.970894	|0.995736	|0.983158|
|1	Cretacico_VMS_Cu-Au-Ag	|Balanceado	|0.963563	|0.769231	|0.400000	|0.526316	|25.0	|0.968815	|0.993603	|0.981053|
|2	Mioceno_Porfidos-Cu-Mo-Au	|No balanceado	|0.970684	|0.933333	|0.451613	|0.608696	|31.0	|0.971619	|0.998285	|0.984772|
|3	Mioceno_Porfidos-Cu-Mo-Au	|Balanceado	|0.967427	|0.923077	|0.387097	|0.545455	|31.0	|0.968386	|0.998285 |0.983108|
|4	Oligoceno-Mioceno_Epitermales-Au-Cu	|No balanceado	|0.971216	|0.810811	|0.555556	|0.659341	|54.0	|0.976923	|0.993157	|0.984973|
|5	Oligoceno-Mioceno_Epitermales-Au-Cu	|Balanceado	|0.960074	|0.689655	|0.370370	|0.481928	|54.0	|0.967557	|0.991202	|0.979237|
|6	Paleoceno-Eoceno_VMS_Cu-Au-Ag	|No balanceado	|0.957494	|0.666667	|0.272727	|0.387097	|22.0	|0.963470	|0.992941	|0.977984|
|7	Paleoceno-Eoceno_VMS_Cu-Au-Ag	|Balanceado	|0.961969	|0.857143	|0.272727	|0.413793	|22.0	|0.963636	|0.997647	|0.980347|


Analisis de sensibilidad
====================================================
|n_estimators	|accuracy	|precision_anomalia	|recall_anomalia	|f1_anomalia|
|-------------|---------|-------------------|-----------------|-----------|
|0	50	|0.960074	|0.677419	|0.388889	|0.494118
|1	100	|0.959146	|0.678571	|0.351852	|0.463415
|2	200	|0.959146	|0.678571	|0.351852	|0.463415
|3	300	|0.960074	|0.689655	|0.370370	|0.481928
|4	500	|0.959146	|0.666667	|0.370370	|0.476190

## Referencias
- Davies, R. S., Trott, M., Georgi, J., & Farrar, A. (2025). Artificial intelligence and machine learning to enhance critical mineral deposit discovery. Geosystems and Geoenvironment, 4(2). https://doi.org/10.1016/j.geogeo.2025.100361
- Diaz, S., Castillo, E., Mery, N., & Munizaga-Rosas, C. (2025). Analyzing mineral exploration efficiency: too little for too much?? Evidence from project valuations and implied discovery - probabilities. Mineral Economics 2025, 1–13. https://doi.org/10.1007/s13563-025-00539-1
- Egozcue, J. J., Gozzi, C., Buccianti, A., & Pawlowsky-Glahn, V. (2024). Exploring geochemical data using compositional techniques: A practical guide. Journal of Geochemical Exploration, 258(2), 107385. https://doi.org/10.1016/j.gexplo.2024.107385
- Exploración generativa. (n.d.). Retrieved March 25, 2026, from https://www.alsglobal.com/es/geochemistry/generative-exploration
- He, Y., Zhou, Y., Wen, T., Zhang, S., Huang, F., Zou, X., Ma, X., & Zhu, Y. (2022). A review of machine learning in geochemistry and cosmochemistry: Method improvements and applications. In Applied Geochemistry (Vol. 140). Elsevier Ltd. https://doi.org/10.1016/j.apgeochem.2022.105273
- Instituto de Investigación Geológico y Energético. (2000). Base de datos 
geoquímica de sedimentos aluviales del Proyecto PRODEMINCA.
- Liu, H., Harris, J., Sherlock, R., Behnia, P., Grunsky, E., Naghizadeh, M., Rubingh, K., Tuba, G., Roots, E., & Hill, G. (2023). Mineral prospectivity mapping using machine learning techniques for gold exploration in the Larder Lake area, Ontario, Canada. Journal of Geochemical Exploration, 253. https://doi.org/10.1016/j.gexplo.2023.107279
- Mejía, J., & Aliakbari, E. (2026). Annual Survey of Mining Companies, 2025 Mining Companies.
- Nathwani, C. L., Wilkinson, J. J., Fry, G., Armstrong, R. N., Smith, D. J., & Ihlenfeld, C. (2022). Machine learning for geochemical exploration: classifying metallogenic fertility in arc magmas and insights into porphyry copper deposit formation. Mineralium Deposita 2022 57:7, 57(7), 1143–1166. https://doi.org/10.1007/S00126-021-01086-9
- Olade, M. A. (n.d.). INTRODUCTION TO MINERAL DEPOSITS GEOLOGY: (Including Exploration, Mining and Mineral Economics) Paperback.
- Schodde, R. (2025). Mineral Deposit Exploration—Discovery Trends: 1900–2023. SEG Discovery, (142), 19–35. https://doi.org/10.5382/Geo-and-Mining-28
- Simon Macheyeki, A., & Yuan, F. (n.d.). APPLIED GEOCHEMISTRY Advances in Mineral Exploration Techniques.
- Smith, W. D., Zhang, L., Sadeghi, B., Djon, M. L., & Mungall, J. E. (2026). Applications of multivariate geochemistry to mineral deposit characterization: A case study from the Pd-mineralized Lac Des Iles Complex, western Ontario, Canada. Journal of Geochemical Exploration, 285(7), 108036. https://doi.org/10.1016/j.gexplo.2026.108036
- Yang, F., Zuo, R., & Kreuzer, O. P. (2024). Artificial intelligence for mineral exploration: A review and perspectives on future directions from data science. Earth-Science Reviews, 258, 104941. https://doi.org/10.1016/j.earscirev.2024.104941










