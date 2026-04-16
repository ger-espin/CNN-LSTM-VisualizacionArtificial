# CNN-LSTM-VisualizacionArtificial
Red Neuronal para leer ecuaciones matemáticas escritas a mano.

La red neuronal se basa en una ResNet con cuatro capas convolucionales junto con una LSTM bidireccional pues al tratarse de ecuaciones matemáticas en indispensable que la red guarde contexto de lo que vino antes de la cadena como de lo que viene después

El preprocesamiento de los datos se hizo de tal manera que fuera eficiente computacionalmente.
Los datos de entrada se eligieron basándonos en una gráfica de distribución de cadenas de caracteres y las imágenes se redimensionaron a 128x384 píxeles.

Para entrenar el modelo se utilizaron 12160 imágenes, lo cual pudo haber saturado la CPU impidiendo que entrenara de manera correcta porque al hacer la evaluación de nuestro modelo vemos que empieza a predecir bien y termina arrojando datos incorrectos. Sin embargo, podemos notar que la red aprende la estructura de las ecuaciones, lo cual nos indica que vamos por buen camino.

El trabajo próximo consiste en volver a entrenar la red ahora con menos imágenes y una mayor cantidad de épocas (se utilizaron 20 hasta el momento y la curva de accuracy y loss tendían a los valores esperados).
