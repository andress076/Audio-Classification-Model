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

Lo que se hizo para resolver el problema fue utilizar el modelo de clasificacion Multilayer Perceptron haciendo uso del espectrograma para clasificar si una torre iba a fallar o no.

Se proporcionaron un total de 198 audios de formato wav con una duración de 30 a 60 segundos y sample rate de 44100 Hz, de los cuales hay 2 tipos

- Audio Normal: Hay 100, se le asigno la etiqueta 0
- Audio Anomalo: Hay 98, se le asigno la etiqueta 1

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

Multilayer Perceptron es una red neuronal que aprende la relación entre datos lineales y no lineales ("poner mas descripcion").

Para el entrenamiento del modelo se utilizo el 75% de los datos.

Los hiperparametros son los siguientes:

- Batch size = 25
- Hidden units = 16
- dropout = 0.3
- epochs = 50


![estructura red](https://user-images.githubusercontent.com/118764182/210003939-2d29d057-832c-4ea1-b53b-c91ac2468238.png)

Las metricas utilizadas fueron accuracy y la matriz de confusion.

La funcion de perdida utilizada fue binary cross entropy.

## Exactitud del modelo

En el entrenamiento y en el testeo se obtuvo como resultado % y % respectivamente.

![exactitud del modelo](https://user-images.githubusercontent.com/118764182/209143928-696160f8-9b2b-4ac3-8ab3-b94d17ed530e.jpg)


## Funcion de perdida

![funcion de perdida](https://user-images.githubusercontent.com/118764182/209144055-e0eae499-5108-4e42-aefa-fb1ef0a04bdf.jpg)


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
9) Se utiliza el modelo de clasificacion Multilayer Perceptron.
10) Se grafica la exactitud, la matriz de confusion y la funcion de perdida del modelo.

