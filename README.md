# Audio-Classification-Model

¿Que es un audio o señal de audio?

El audio consiste en la tensión eléctrica o magnética proporcional a un sonido, y éste se genera a través de transductores (Es decir, aquellos elementos que transforman una magnitud física en una señal eléctrica). Estos transductores pueden ser, por ejemplo, los micrófonos.

Poner conector del uso del espectrograma.

El espectrograma permite identificar las diferentes variaciones de la frecuencia y la intensidad del sonido a lo largo de un periodo de tiempo.
Cada eje de un espectrograma se visualiza de diferentes formas:

- El tiempo está representado por el eje horizontal.
- El eje vertical muestra la frecuencia.
- El color que marque el espectrograma ayuda a identificar la intensidad del sonido.

![espectrograma](https://user-images.githubusercontent.com/118764182/209146433-45407e7e-6b75-4e31-9a70-48414049e274.jpg)

Dado que en la actualidad se puede grabar,obtener audio de todo tipo de cosas (animales, maquinaria, personas, etc) de manera "sencilla" y almacenar en gran cantidad, se pueden tratar distintos problemas, ideas relacionados con el audio mediante la creacion de modelos relacionados con la respectiva problematica.

En el siguiente ejercicio vamos a abordar el problema de un cliente relacionado con el monitoreo de torres de alta tension, estas torres por el tiempo y distintos factores generan un sonido caracteristico (Efecto corona).

Lo que se hizo para resolver el problema fue generar un modelo predcitivo mediante el uso del espectrograma para clasificar si una torre iba a fallar o no.

Audios: Hay un total de 198 audios de formato wav con una duración de 30 a 60 segundos y sample rate de 44100 Hz, de los cuales hay 2 tipos

- Audio Normal: Hay 100
- Audio Anomalo: Hay 98

![ACM GRAFICO](https://user-images.githubusercontent.com/118764182/208528333-e0eddadf-9b58-4ca0-be3c-265724144fea.png)


Metadatos:

- File name
- Channels: Number of channels (1 for Mono, 2 for Stereo)
- Sample width: Number of bytes in each sample (1 for 8 bit, 2 for 16 bit, 4 for 32 bit)
- Frame rate/Sample rate: Number of samples per second. Common values are 44100, 48000, 22050, 24000, 12000
- Frame width: Number of bytes for each frame. A frame contains a sample for each channel. frame width = channels * sample width
- Length: Duration in seconds
- Intensity: The loudness in dBFS (db relative to the maximum possible loudness)

Preprocesamiento:

- Frame size: 512, 1024, 2048, 8192 (Valores mas habituales) 
- Hop length: 256, 512, 1024, 2048, 4096 (Valores mas habituales)
- Number of frames: ((samples - frame size) / hop length) + 1
- Window: Hann, Hamming, flattop, boxcar, triang, entre otras. Hann funciona bien el 95% de los casos

El espectragrama da como resultado una matriz de tamaño m x n

m = (frame size / 2) + 1

n = number of frames

Resumen de clasificador.ipnyb:

1) Se guardan las rutas  y los nombres de los audios
2) Se obtienen los metadatos de los audios
3) Se escogen los parametros del preprocesamiento (frame size, hop length, window)
4) Se cargan los audios, se obtiene la Short-time Fourier transform (stft), el espectrograma y se calcula la media de cada fila del espectrograma
5) Se utiliza un modelo de clasificacion en este caso (Multilayer Perceptron) y se obtienen los resultados

![exactitud del modelo](https://user-images.githubusercontent.com/118764182/209143928-696160f8-9b2b-4ac3-8ab3-b94d17ed530e.jpg)

![funcion de perdida](https://user-images.githubusercontent.com/118764182/209144055-e0eae499-5108-4e42-aefa-fb1ef0a04bdf.jpg)



