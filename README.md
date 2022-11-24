# Audio-Classification-Model

Audios: Tenemos 2 Tipos de audios

- Audio Normal
- Audio Contaminado

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

Espectrograma:

Espectogram.shape = (x,y) --> x = (frame size / 2) + 1 , y = Number of frames
