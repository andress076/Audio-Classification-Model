# Audio-Classification-Model

¿Que es un audio o señal de audio?

El audio consiste en la tensión eléctrica o magnética proporcional a un sonido, y éste se genera a través de transductores (Es decir, aquellos elementos que transforman una magnitud física en una señal eléctrica). Estos transductores pueden ser, por ejemplo, los micrófonos.

Para poder utilizar los audios existen representaciones visuales como:

- Forma de onda
- Espectro
- Espectrograma

De estas 3 representaciones la mas completa es el espectrograma ya que permite identificar las diferentes variaciones de la frecuencia y la intensidad del sonido a lo largo de un periodo de tiempo.

Cada eje de un espectrograma se visualiza de diferentes formas:

- El tiempo está representado por el eje horizontal.
- El eje vertical muestra la frecuencia.
- El color que marque el espectrograma ayuda a identificar la intensidad del sonido.

![espectrograma](https://user-images.githubusercontent.com/118764182/209146433-45407e7e-6b75-4e31-9a70-48414049e274.jpg)


Dado que en la actualidad se puede grabar,obtener audio de todo tipo de cosas (animales, maquinaria, personas, etc) de manera "sencilla" y almacenar en gran cantidad, se pueden tratar distintos problemas, ideas relacionados con el audio mediante la creacion de modelos relacionados con la respectiva problematica.

Por ejemplo:

- Separacion de fuentes: Separacion vocal de una fuente de entrada de audio.
- Reconocimiento automatico de voz: Trancribir automáticamente audio en tiempo real o pregrabado a texto.
- Clasificador de generos musicales: Reconocimiento y etiquetado automatico de generos musicales.

En el siguiente ejercicio vamos a abordar el problema de un cliente relacionado con el monitoreo de torres de alta tension.

Las torres de alta tension por el tiempo y distintos factores generan un sonido caracteristico llamado efecto corona. El efecto corona es un fenómeno que consiste en una descarga eléctrica debido a la ionización del fluido que circunda a un conductor energizado. El ruido provocado consiste en una zumbido constante tipo interferencia de radio provocado por el movimiento de los iones.

Lo requerido era que mediante el audio generado por una torre poder clasificar si iba a fallar o no.

Lo que se hizo para resolver el problema fue utilizar el modelo de clasificacion gaussian naive bayes haciendo uso del espectrograma para clasificar si una torre iba a fallar o no.

Se proporcionaron un total de 198 audios de formato wav con una duración de 30 a 60 segundos y sample rate de 44100 Hz, de los cuales hay 2 tipos

- Audio Normal: Hay 100, se le coloco la etiqueta 0
- Audio Anomalo: Hay 98, se le coloco la etiqueta 1

A continuacion se muestra la arquitectura del ciclo de vida de un modelo de machine learning de un proyecto de analisis de audio.

![Grafico de flujo](https://user-images.githubusercontent.com/118764182/209965842-d5ff8cd9-f430-49a2-8bbb-762a96e865cf.png)


## Metadatos

Caracteristicas genericas que se extrajeron a los audios proporcionados

- File name
- Channels: Number of channels (1 for Mono, 2 for Stereo)
- Sample width: Number of bytes in each sample (1 for 8 bit, 2 for 16 bit, 4 for 32 bit)
- Frame rate/Sample rate: Number of samples per second. Common values are 44100, 48000, 22050, 24000, 12000
- Frame width: Number of bytes for each frame. A frame contains a sample for each channel. frame width = channels * sample width
- Length: Duration in seconds
- Intensity: The loudness in dBFS (db relative to the maximum possible loudness)

## Preprocesamiento

- Frame size: Los valores mas habituales son: 512, 1024, 2048, 8192.
- Hop length: Los valores mas habituales son: 256, 512, 1024, 2048, 4096.
- Number of frames: El numero de frames es igual a lo siguiente: ((samples - frame size) / hop length) + 1
- Window: Existen varias funciones de ventana como: Hann, Hamming, flattop, boxcar, triang, entre otras. Hann funciona bien el 95% de los casos.

Se escogieron los siguientes parametros:

- Frame size = 1024
- Hop lenght = 512
- Window = Hann

El numero de frames va a depender del numero de samples que posea el audio.

## Descripcion del modelo

Gaussian Naive Bayes es un algoritmo de clasificación probabilística basado en la aplicación del teorema de Bayes con fuertes suposiciones de independencia. En el
contexto de la clasificación, la independencia se refiere a la idea de que la presencia de un valor de una característica no influye en la presencia de otro (a 
diferencia de la independencia en la teoría de la probabilidad). Naive se refiere al uso de la suposición de que las características de un objeto son independientes 
entre sí.

Las metricas escogidas son:

- accuracy: Es la fracción de predicciones que el modelo realizó correctamente
- matriz de confusion: Es una herramienta que permite visualizar el desempeño del modelo, no permite ver cuantos aciertos y errores hemos obtenido.

![MATRIZ-CONFUSION](https://user-images.githubusercontent.com/118764182/210014655-b6ad53ee-43c4-421a-8c3a-42d76447168c.png)


## Resultados

Para el accuracy se obtuvo un valor de 100%

Matriz de confusion

![matriz de confusion](https://user-images.githubusercontent.com/118764182/210012922-ab3ba759-ebd0-443b-99a7-0e7424c0c729.png)


## Resumen de clasificador.ipnyb

1) Se guardan las rutas y los nombres de los audios para poder extraer los metadatos y obtener los espectrogramas.
2) Se obtienen los metadatos de los audios.
3) Se escogen los parametros del preprocesamiento (frame size = 1024, hop length = 512, window = Hann)
4) Se cargan los audios
5) Se calcula la Short-time Fourier transform (stft)
6) Por medio de la stft se obtiene el espectrograma, el cual es una matriz de tamaño m x n donde: 
m = (frame size / 2) + 1 ; n = number of frames.
7) Se calcula la media de cada fila del espectrograma y se guarda como "espectrograma scaled", la cual se utiliza para entrenar el modelo.
8) Se dividen los datos en entrenamiento y testeo, para el testeo se utiliza un 25%. 
9) Se utiliza el modelo de clasificacion gaussian naive bayes
10) Se obtienen los resultados de las metricas escogidas (accuracy, confusion matrix)
