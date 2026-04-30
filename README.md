# CNN-LSTM-VisualizacionArtificial

Este proyecto tiene la finalidad de leer ecuaciones escritas a mano para ayudar a las personas con discapacidad visual total o parcial a aprender matemáticas.

El data set que se eligió para trabajar fue: https://www.kaggle.com/datasets/sumit17125/handwritten-images-dataset

En él nos encontramos con 12167 imágenes en blanco y negro con expresiones matemáticas escritas a mano, así como un archivo CSV que relaciona las imágenes con su contenido escrito en código LaTeX. Además de un archivo JSON con varios de los caracteres que conforman la escritura de las ecuaciones.

Lo primero que se hizo fue asegurarnos de que el contenido del JSON estuviera completo cotejándolo con el CSV además de agregar las etiquetas de Inicio de Secuencia <BOS>, Fin de Secuencia <EOS>, Padding <PAD> y una etiqueta para los caracteres desconocidos <UNK>.

Lo siguiente fue explorar la longitud de las cadenas para decir el tamaño estándar que iba a recibir el modelo, por lo que se hizo una gráfica de distribución acompañada de estadísticas:

<img width="580" height="455" alt="Distribucion" src="https://github.com/user-attachments/assets/5a111788-5adf-4e8f-a6a3-073d435caae6" />

Para así decidirse por un total de 50.

Se utilizaron 4 filtros de convolución con un tamaño de 32, 64, 128 y 256 así como dos capas de LSTM Bidireccionales pues se debería de entender la relación compleja de una ecuación matemática.

Se utilizaron 12160 datos de los cuales el 70% fue entrenamiento, el 10% para validación y el 20% restante para prueba.

Los resultados pudieron verse limitados por la capacidad de cómputo de mi máquina y se realizarán pruebas posteriores con menos datos y mayor cantidad de épocas esperando que el "loss" se reduzca y se pueda predecir mejor la ecuación, sin embargo tal parece que la red sí tiene una buena noción de lo que sucede en la imágen.
