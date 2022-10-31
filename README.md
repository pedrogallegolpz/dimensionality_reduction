# dimensionality_reduction

Se va a estudiar la capacidad de los autoencoders para reducir la dimensionalidad desde las 512 dimensiones que tenemos originalmente. Los resultados dados por los autoencoders se contrastarán con los correspondientes modelos de PCA y U-MAP. Para ello, se tiene que elegir una dimensión K1 a la que reducir el espacio. Para generalizar se van a estudiar los valores 
				K1 in {16,32,64,128}
 
Como requisito para un buen desempeño de los modelos al reducir dimensionalidad se necesita que cada instancia conserve su vecindario. El vecindario estará formado por los K2 vecinos más cercanos.  Para generalizar también vamos a mover el K2 sobre los valores {2,4,8,16,32,64,128}. Además, una buena reducción hará que un clasificador conserve su clasificación del espacio original en el reducido. Así, haremos varios estudios:
 - Qué porcentaje del K2-vecindario de dimensión original se conserva en el K2-vecindario del espacio reducido para cada instancia.
 - Dado un porcentaje X, ¿qué valor de K2’ se necesita para que el K2’-vecindario del espacio reducido mantenga un X% del K2-vecindario original?
  - ¿Se conserva la clasificación? Clasificaremos las instancias tanto en el espacio original como en el espacio reducido. Compararemos las dos clasificaciones para ver cuánto se han conservado.

### Qué porcentaje del K2-vecindario de dimensión original se conserva en el K2-vecindario del espacio reducido para cada instancia.
Vemos los resultados para cada K1-espacio.
Vemos los resultados para cada K1-espacio. 
 
 
 - K1=16

 - K1=32

 - K1=64

 - K1=128

 
En este primer estudio resalta el desempeño de U-MAP, que se queda lejos de conseguir los resultados de sus competidores. Por otro lado, entre el AutoEncoder y PCA tenemos resultados similares. Para K2 más pequeños el autoencoder mejora a PCA. Sin embargo, para un K2 mayor (por ejemplo de 64 y 128) es PCA quien consigue mejores resultados. Esto va a ayudar a concluir que cuando se requiere una reducción de dimensionalidad a un número muy pequeño de características es mejor opción el autoencoder. 
 
#### Dado un porcentaje X, ¿qué valor de K2’ se necesita para que el K2’-vecindario del espacio reducido mantenga un X% del K2-vecindario original?
 
Para este apartado se va a fijar el valor de K2 (número de vecinos en el espacio original) y nos vamos a mover con K2’ (número de vecinos en el espacio reducido). 
En este caso se van a mostrar los valores para los K1-espacio (espacio reducido de dimensión K1) con K1=16 y K1=128.

 - K1=16 y distancia coseno


 
 
 - K1=16 y MSE
 



 
 - K1=128 y distancia coseno


 
 - K1=128 y MSE

 


Para un K1=16 los modelos de autoencoder mejoran a PCA, sin embargo para un K1=128 pasa al contrario. Volviendo a tener una conclusión parecida al apartado anterior. Además, se puede observar como la distancia coseno beneficia al autoencoder en el 128-espacio.



### ¿Se conserva la clasificación? Clasificaremos las instancias tanto en el espacio original como en el espacio reducido. Compararemos las dos clasificaciones para ver cuánto se han conservado.
 
Para este apartado se han utilizado dos modelos: 
 - Random Forest
 - Regresión Logística
 
Se han escogido las 6 clases más representativas de los 20000 documentos escogidos para esta prueba. Sobre estas clases se ha entrenado un modelo de Random Forest en distintos espacios de dimensionalidad. Esta tabla representa los resultados del accuracy en test para cada dimensión:
 


##### RANDOM FOREST

|| | | N-SPACE (ORIGINAL=0.6815) | | |
||:-------------------:|---|---|---|---|
||  2| 4| 8 | 16 | 32| 
||:-------------------:|---|---|---|---|
|PCA| 0.3899 | 0.5795 | 0.6196 | 0.6702 | 0.6794 |
|AUTOENCODER| 0.5354 | 0.6219 | 0.6655 | 0.6738 | 0.6758 |












##### REGRESIÓN LOGÍSTICA


N-SPACE (ORIGINAL = 0.6961)


2
4
8
16
32
PCA
0.4303
0.575
0.5892
0.6461
0.6686
AUTOENCODER
0.4339
0.5835
0.6196
0.6528
0.6688



 
La conclusión en este apartado está en la línea de lo que estábamos viendo en los anteriores. Cuando la reducción de dimensionalidad es muy grande (reducimos a una dimensión muy pequeña) el autoencoder sigue comportándose mejor, conservando gran parte de su clasificación original. 


Juntando los resultados podemos concluir que PCA tiene un buen desempeño a la hora de reducir dimensionalidad en este problema hasta cierta dimensión, donde empieza a verse superado por el Autoencoder. Esto implica que nuestras características tienen cierta componente lineal y muchas de estas características tienen una alta correlación. Así, el AutoEncoder es un modelo capaz de detectar tanto estas dependencias lineales como otras más complejas, permitiendo reducir la dimensión hasta valores muy pequeños conservando gran parte de la información que PCA no es capaz de conservar.



