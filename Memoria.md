
                                                  ###  Smart City Water Analitycs  ####
                                                  
                                                  

**Abstract

The study consisted of two stages, in the first one the datasets were split by months and analyzed separately to evaluate the features presented in each one. To evaluate the representative behavior for city, the dataset will be analyzed to find the water foot print who share the same pattern in behavior. In the second stage, different regression models were applied to the data to find the relation between the demand patterns and the meter account variables. This projects shall be considerer as mixed of real data from official Madrid statictis and random consumption in middle city by neighborhood groups, in order to save the public mottion of this task.

**Introducción

A partir del conocimiento en las técnicas de Data Science existentes, se elegirán las herramientas más adecuadas para la predicción del consumo de redes de distribución de agua de Madrid. Se procesaron diferentes conjuntos de datos afines al estudio, dos de ellos correspondientes a la ciudad de Madrid y otro caso el patrón de consumos heredado de una ciudad tipo de acceso público, incluyendo variables vinculadas a consumos a cuenta del consumidor asociada a los medidores (flow meter) 

El estudio constó de dos etapas, en la primera, los conjuntos de datos se dividieron por temporada y se analizan por separado para evaluar las características presentadas en cada uno. Para evaluar la comportamiento representativo y virtual de la Ciudad de Madrid, se analizaron las etiquetas de agrupamiento para encontrar los grupos que tengan el mismo patrón. En la segunda etapa se aplicaron modelos a los datos para encontrar la relación entre los patrones de demanda y las variables de la cuenta del consumidor.

Los enlaces incluidos en esta memoria obedecen a las restricciones de GitHub para subir archivos > 25 Mb.

**Descripción de los datos de entrada

La base del análisis parte del dataset AguaH.csv rescatado de la comunidad kaggle,  alojado en:

"https://www.kaggle.com/jaeyoonpark/data-imputation-aguah-water-consumption/data"

En algunos notebooks desarrollados hasta la fecha en torno a este data set, se centran sobre todo en la aproximación en la sustitución de los NA/null data en base a criterios como interpolaciones o k- vecinos. Aunque es un ejercicio interesante, podemos trasformar ese código como un ejercicio auxiliar al tfm, pero no como el grueso del proceso de limpieza, que se aborda por estrategias más directas. Los datos en bruto presentan varios problemas en la clase de los registros de consumo (son factores), en las variables que no aportan información o es sesgada, y en la cantidad de datos perdidos, sobre todo en los primeros años de registro 2009-2011, como se puede ver el link de kaggle. La limpieza se explica paso a paso en el script de esta fase. El lenguaje elegido ha sido R por la potencial naturaleza estadística del problema.

Los datos de perfil de consumos totalizados de distritos se han obtenido de la base de datos pública del Ayuntamiento de Madrid

"http://www-2.munimadrid.es/CSE6/control/seleccionDatos?numSerie=14030200040"

El objetivo de proyecto es crear un perfil virtual plausible de consumo en base a la huella de una ciudad media, escalada a Madrid. El espíritu del trabajo es seguir desarrollando y mejorando el modelo con datos reales de fuentes privadas. Esto implica que el grueso del trabajo aquí desarrollado se puede iterar con las data base adecuadas, que para el caso de evaluación de proyecto que nos ocupa, y debido a la idea de mantener públicos y consultables los resultados aquí obtenidos, será abordado en una fase beta. 

**Metodología

Las series de datos disponibles en las bases de los organismos oficiales de Madrid aportan información hasta el 2016.En base a esto se ha escalado el patrón de consumo de los totalizados de distritos de Madrid y adecuado a la serie temporal de datos para el periodo
de 2009-2015. En resumen se han trabajado 85 variables independientes con observaciones entorno a los 178.598 puntos de consumo.

Durante el tratamiento de datos se ha filtrado la información para conseguir el tipo de series (diccionarios) que necesita el modelo de la fase de análisis, y asignado valores a datos NA/null en base a los detalles redactados en el código.

En la fase de análisis se ha empleado diferentes modelos generalizados de regresión logística, tratando los datos como series temporales, adecuadas para el tratamiento de la información con el paquete ARIMA, autogenerador de modelos de regresión más adecuado para una estimación de la serie. Esta opción de modelización pasa por tratar de explicar el comportamiento de una variable, no solo función de los valores que tomó en el pasado (modelos AR) sino a través de los errores al estimar el valor de la variable en los períodos anteriores. Ello da lugar a los modelos de medias móviles (Modelos MA), que están integrados dentro de ARIMA y que son los adecuados para series temporales con periodicidad, asumiendo el diagnostico de varios modelos combinados (lm, gml, etc.). Los detalles y tratamiento de la información se encentran en el código del apartado de Regression model_water analitics.

**Resumen del resultado

Como resultado final encontramos una matriz de predicciones completa para el año 2016, que podemos testear con valores reales totalizados de la serie. La precisión de la predicción se ha calculado en torno a 88.36 %. Hay derivadas interesantes que apuntan los datos, como estimaciones a la baja en torno 10-5 %, que pueden indicar dos patrones, o bien una restricción en la información de la naturaleza de los puntos calientes de la ciudad ( hospitales, instalaciones militares, edificios oficiales, etc) o incluso una huella de fraude de consumidores en la desviación real del consumo al alza que puede ser un spin off interesante de abordar de este proyecto, que sigue vivo, con los registros oficiales y privados de la gestora del agua en Madrid.

Los modelos empleados, aún teniendo margen de mejora, indican una tendencia a la baja en el consumo que puede impactar de forma favorable en la definición de proyectos y modelos de explotación aguas arriba (ETAP, Redes de distribición) y abajo (EDAR, reciclaje de agua) de la ecuación de ciclo integral de agua en las ciudades. Potencial de ahorro y utilización de recursos.

Los data set resultado están diponibles en esta cuenta github y aplicaciones desarrolladas para este proyecto.

**Manual de usuario

Se ha empleado leaflet como dashboard shinyapps.io, para la construcción de cuadros de mando web interactivos. Permite, por ejemplo, crear interfaces para acceder y manipular tablas de datos de predicciones a través de controles de HMTL. El usuario puede visualizar los datos de la serie histórica y las predicciones a través de un mapa interactivo. Hay también un apartado dedicado a la generación de mapas estáticos, donde se ha empleado cartografía formato .shp de la Comunidad de Madrid.

Se implementado también una shinyApp para analizar por distritos, tipo de consumidores y consumos anuales como datos de entrada las distribuciones de datos resultado de la aplicación de los modelos, así como un cluster de distribución, puede consultarse en la siguiente URL:

https://scwa2018.shinyapps.io/scwa_madrid/

https://scwa2018.shinyapps.io/scwa_madrid_cluster/







