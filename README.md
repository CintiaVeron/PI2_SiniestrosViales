# <h1 align=center> **PROYECTO INDIVIDUAL Nº2** -Siniestros Viales en CABA  </h1> 

## ** Descripción de la Temática**⚠️ 🚧

El problema de los siniestros viales, también conocidos como accidentes de tráfico o accidentes de tránsito, es significativo en ciudades como Buenos Aires debido al alto volumen de tráfico y densidad poblacional. Estos incidentes pueden resultar en daños materiales, lesiones graves o incluso la muerte de los involucrados. En Argentina, los siniestros viales representan una preocupación importante, ya que causan un alto número de muertes cada año, superando incluso a otras formas de violencia. Entre 2018 y 2022, se registraron 19.630 muertes en siniestros viales en todo el país, equivalente a un promedio de 11 personas por día. Estas cifras son alarmantes y subrayan la necesidad de medidas efectivas para abordar este problema. La prevención de siniestros viales requiere una combinación de educación vial, cumplimiento de normas de tráfico, mejora de la infraestructura vial y promoción de vehículos más seguros. Es fundamental seguir de cerca las estadísticas e implementar políticas efectivas para reducir las tasas de mortalidad relacionadas con los siniestros viales.
 [Datos oficiales](https://data.buenosaires.gob.ar/dataset/victimas-siniestros-viales)

## **Objetivo del Proyecto**⚠️ 🚧

En el rol de Data Analyst, el Observatorio de Movilidad y Seguridad Vial (OMSV), centro de estudios que se encuentra bajo la órbita de la Secretaría de Transporte del Gobierno de la Ciudad Autónoma de Buenos Aires, nos solicita la elaboración de un proyecto de análisis de datos, con el fin de generar información que le permita a las autoridades locales tomar medidas para disminuir la cantidad de víctimas fatales de los siniestros viales. Para ello, nos disponibilizan un dataset sobre homicidios en siniestros viales acaecidos en la Ciudad de Buenos Aires durante el periodo 2016-2021

 Por todo ello, el estudio del problema para la prevención y disminución de Siniestros viales es escencialmente importante para las autoridades.

##**Proceso de Analisis**

## **ETL (Extraction, Transformation, and Loading)**⚠️ 🚧

En este proceso lo que se realizo es la importación de los datos desde la fuente brindada, con el fin de revisar los archivos xlsx, ver su formato , las cantidad de columnas y filas, una vez completa la revisión se realiza las siguientes transformaciones
  •	Homicidios.xlsx: se observa que posee varias hojas:
  'HECHOS', 'DICCIONARIO_HECHOS', 'VICTIMAS', 'DICCIONARIO_VICTIMAS'

Se realiza un merge con los datos de las hojas “HECHOS” Y “VICTIMAS”, agregando a la hoja de hechos los datos de  'ROL', 'SEXO', 'EDAD' y 'FECHA_FALLECIMIENTO'

Se guarda en archivo xslx 

### EDA (EXPLORATORY DATA ANALYSIS)⛔
Se importan las librerías necesarias y se analizan valores nulos , outliers y duplicados, así como también se realiza análisis estadísticos y visualizaciones de los datos para explorar las relaciones entre las variables e identificar patrones o tendencias en los datos.

valores nulos:

Se encontraron valores nulos en las columnas Altura,Cruce y calle . Se optó por eliminar la columna altura debido a al % de valores nulos con respecto a su totalidad.(Porcentaje de valores nulos en la columna Altura: 81.45%)
En la columna Cruce , se imputo con la palabra "NO" modificando los valores Nulos , haciendo referencia que quizas el accidente No fue en un cruce de calles o no hay informacion al respecto.

valores duplicados: encontramos 21 valores duplicados en la columna ID , por lo que decidimos eliminar los duplicados y dejar solo valores unicos en dicha columna.

conversion de Columnas 
Se realiza cambios en  los tipos de datos de las columnas 
Nro Victimas numericos
Fecha date 
hora time
comuna numerico
Edad numerico

Outliers :
Como conclusión de outliers en la columna Numeros de victimas:
se utilizo un diagrama de cajas para visualizar la distribucion de la  columna con el total de n° de victimas , se verifica que , la mayoria de la cantidad de victimas esta en el primer cuartil , y que como outliers podemos observar que son pocos los valores donde la cantidad de victimas son 2 o 3.

### INSIGTHS⛔

Cantidad de Victimas por comuna:

podemos observar que en la comuna 1, 4 y 9 son las mayor parte de los accidentes, cuando lo llevemos al dashboard podremos observar que zona es y servirá para tomar medidas que disminuyan los mismos 


Cantidad de Victimas por Genero:

Verificamos que la mayor parte de victimas son personas de genero masculino con un 76% y genero femenino 23,02%, dejando un 0,8 % donde nuestro dataset no tiene datos del genero de la victima, esto puede deberse a que en nuestro dataset tenemos mas conductores hombres que mujeres.

DISTRIBUCION CRUZADA ENTRE VICTIMAS Y SEXO:

Basándonos en la distribución cruzada entre el tipo de víctima y el sexo mostrada en el gráfico de barras apiladas, podemos hacer las siguientes conclusiones:

Mayor número de víctimas en Moto: La categoría de víctimas en moto tiene el mayor número de casos, y la mayoría de las víctimas son hombres. Esto sugiere que los accidentes de motocicleta son una preocupación significativa en términos de seguridad vial.

Víctimas peatones y en auto: Las categorías de víctimas que involucran peatones y ocupantes de automóviles también muestran una predominancia del género masculino, aunque la diferencia entre hombres y mujeres no es tan pronunciada como en el caso de las víctimas en moto.

Otras categorías: Algunas categorías como "OBJETO FIJO" y "MOVIL" tienen un número bajo de víctimas, mientras que "CARGAS" no tiene víctimas femeninas. Esto podría sugerir que estos tipos de accidentes son menos comunes o tienen características específicas que los hacen menos propensos a afectar a ciertos géneros.

Estas son algunos de los insigths que se pudieron observar, el resto se encuentra en el archivo EDA.

Finalizamos el proceso guardando el dataset en formato CSV en la ruta "PI2_Siniestros_Viales\csv\homicidio_Eda.csv"

### Conexion a SQL  ⛔

Creamos un script de python en un jupyter notebook, para realizar la conexion con MYSQL :
"PI2_Siniestros_Viales\conexion_sql.ipynb"

Aquí está el flujo de trabajo del script:

1-mporta la biblioteca mysql.connector para conectarse a la base de datos MySQL.
2-Se establece la conexión con la base de datos MySQL utilizando la función connect() de mysql.connector.
3-Define una consulta SQL para crear una tabla llamada 'homicidio' en la base de datos MySQL. La estructura de la tabla se basa en las columnas del archivo Excel.
4Ejecuta la consulta SQL utilizando el método execute() del cursor.
5Confirma los cambios en la base de datos utilizando el método commit() y cierra la conexión utilizando el método close()

Desde MYsql se importan los datos a la tabla creada con el script.


### Indicadores de Rendimiento Clave KPI⛔



##**KPI N1**

SE OBTIENEN LOS DATOS DE POBLACION AL 2021 DESDE https://www.indec.gob.ar/indec/web/Nivel4-Tema-2-24-85
3.078.836

Reducir en un 10% la tasa de homicidios en siniestros viales de los últimos seis meses, en CABA, en comparación con la tasa de homicidios en siniestros viales del semestre anterior.

Definimos a la tasa de homicidios en siniestros viales como el número de víctimas fatales en accidentes de tránsito por cada 100,000 habitantes en un área geográfica durante un período de tiempo específico. Su fórmula es: (Número de homicidios en siniestros viales / Población total) * 100,000

Conclusion:



1. Tendencia general: Se observa una variación en la tasa de homicidios en siniestros viales a lo largo de los años y semestres. Algunos años muestran aumentos significativos, mientras que otros muestran disminuciones.

2.Cambios por semestre: Dentro de cada año, los semestres muestran diferencias en la tasa de homicidios en siniestros viales. Algunos semestres muestran aumentos, mientras que otros muestran disminuciones en comparación con el semestre anterior.

3.Variación por año: Hay años donde se observa una tendencia general de aumento o disminución en la tasa de homicidios en siniestros viales. Por ejemplo, en el año 2018, se observa un aumento significativo en la tasa en comparación con el año anterior.

Últimos seis meses del 2021: La tasa de homicidios en siniestros viales en los últimos seis meses del año 2021 muestra una disminución del 24% en comparación con el semestre anterior por lo que esta reduccion supera  el objetivo del 10% propuesto.

En general, estos resultados sugieren que se han producido cambios en la tasa de homicidios en siniestros viales a lo largo del tiempo, lo que indica la importancia de implementar medidas efectivas para mejorar la seguridad vial y reducir el número de víctimas en la ciudad.



##**KPI N2**

Reducir en un 7% la cantidad de accidentes mortales de motociclistas en el último año, en CABA, respecto al año anterior.

Definimos a la cantidad de accidentes mortales de motociclistas en siniestros viales como el número absoluto de accidentes fatales en los que estuvieron involucradas víctimas que viajaban en moto en un determinado periodo temporal. Su fórmula para medir la evolución de los accidentes mortales con víctimas en moto es: (Número de accidentes mortales con víctimas en moto en el año anterior - Número de accidentes mortales con víctimas en moto en el año actual) / (Número de accidentes mortales con víctimas en moto en el año anterior) * 100

Conclusion :
Los resultados muestran una disminución significativa en el número de víctimas totales de siniestros viales, pasando de 150 en 2016 a 97 en 2021. Sin embargo, la cantidad de víctimas en moto ha experimentado fluctuaciones significativas a lo largo de los años, con una tendencia a la baja en general, especialmente destacada en 2020 con una disminución del 40% en comparación con el año anterior. En 2021, se observa un aumento notable del 53.33% en el número de víctimas en moto, lo que indica un cambio significativo en la seguridad vial para este grupo de usuarios.

#**KPI n3**

Reducir en un 2% la cantidad de accidentes mortales de peatones  en el último año, en CABA, respecto al año anterior.

Definimos a la cantidad de accidentes mortales de peatones en siniestros viales como el número absoluto de accidentes fatales en los que estuvieron involucradas víctimas peatones en un determinado periodo temporal. Su fórmula para medir la evolución de los accidentes mortales con víctimas en auto es: (Número de accidentes mortales con víctimas peatones en el año anterior - Número de accidentes mortales con víctimas peatones en el año actual) / (Número de accidentes mortales con víctimas en moto en el año anterior) * 100


Conclusion:
En el año 2021, el número total de siniestros  fue 97, y el número de víctimas en accidentes de peatones fue 33.
En comparación con el año 2020, hubo una disminución del 2,94% en el número de víctimas peatones,podríamos decir que se ha cumplido con el objetivo de reducir los accidentes en al menos un 2%. Esto sugiere que podríamos implementar medidas para reducir aun mas las victimas peatones , observando por ejemplo cual serian los acusados que tienen como victimas mas peatones.



### TABLERO DE VISUALIZACION POWER BI⛔

UNA VEZ CREADO LA BASE E IMPRTADO LOS DATOS EN MYSQL , SE IMPORTAN LOS DATOS A POWER BI PARA LAS VISUALIZACIONES

EL DASHCBOARD CONSTA DE 4 PAGINAS DONDE SE ENTREGARAN LAS VISUALIZACION DEL ANALISIS IMPLEMENTADO:

PORTADA----RESUMEN---DATOSGEOGRAFICOS---OBEJTIVOS 

 lo pueden ver ACCEDIENDO al  ARCHIVO "Dashboard_Siniestros_Viales.pbix


