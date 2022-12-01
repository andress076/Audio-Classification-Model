# Audio-Classification-Model

Audios: Hay un total de 198 audios de formato wav con una duración de 30 a 60 segundos y sample rate de 44100 Hz, de los cuales hay 2 tipos

- Audio Normal: Hay 100
- Audio Anomalo: Hay 98

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

Espectrograma: Es una matriz de tamaño m x n

m = (frame size / 2) + 1

n = number of frames

Resumen de clasificador.ipnyb:

1) Se guardan las rutas  y los nombres de los audios
2) Se obtienen los metadatos de los audios
3) Se escogen los parametros del preprocesamiento (frame size, hop length, window)
4) Se cargan los audios, se obtiene la stft, el espectrograma y se calcula la media de cada fila del espectrograma
5) Se utiliza un modelo de clasificacion en este caso (Multilayer Perceptron) y se obtienen los resultados
