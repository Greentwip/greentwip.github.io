---
title: Identificación y Reconocimiento Facial
date: 2020-12-07 08:23:00 Z
published: false
---

Hoy hablaremos acerca de cómo es posible identificar rostros mediante un nivel de certeza en la identificación con un algoritmo no-entrenado que se puede entrenar con imágenes predeterminadas.

Al igual que el post anterior, es necesario utilizar:

Visual Studio 2019
CMake (instalado en el PATH)
Git

Y de igual manera:

El código completo lo puedes encontrar [aquí](https://github.com/Greentwip/OpenCV-Recognition/).

Esto es tan sencillo como clonar con:

```
git clone https://github.com/Greentwip/OpenCV-Recognition
```

Cuando lo clones no olvides llamar en el directorio OpenCV-Recognition:

```
git submodule init
git submodule update
```

Ejecuta setup.bat dentro de opencv para crear los archivos de proyecto necesarios para la compilación.

Una vez generados dirígete a opencv/build/VS2019 abre OpenCV.sln y compila este proyecto de acá (INSTALL):

![opencvinstall.PNG](/uploads/opencvinstall.PNG)

Hacer eso instalará todo lo necesario en la carpeta opencv/build/VS2019 y podrás abrir y compilar Arduino_GUI.sln

Bueno, creo que es suficiente como para empezar.

En el código tenemos el constructor:

![untrained-constructor.PNG](/uploads/untrained-constructor.PNG)

Donde le pasamos la ruta a "haarcascade_frontalface_default.xml", que es el algoritmo que va a identificarnos los rostros.

Después cargamos data/csv.ext, que es un archivo separado por comas que incluye las imágenes de entrenamiento en formato:

```
victor_01_20_20_70_70.jpg
```

No tuve tiempo de investigar que es 20 20 70 70, pero aunque no es muy relevante, puede utilizarse para la ubicación del rostro y de los ojos, al parecer OpenCV lo lee directamente desde el formato del nombre del archivo, 01 es simplemente un identificador de imagen.

Finalmente creamos el modelo de reconocimiento facial y entrenamos con:

```
_model = cv::face::EigenFaceRecognizer::create();

_model->train(_images, _labels);

```

Esto le dará al model información acerca de cómo reconocer los rostros.

Dentro de detect, en UntrainedDetector, tenemos lo siguiente:

![faces-part1.PNG](/uploads/faces-part1.PNG)

Se convierte a escala de grises y luego se detectan los rectángulos de los rostros con:

```
cvtColor(original, gray, cv::COLOR_BGR2GRAY);
_haar_cascade.detectMultiScale(gray, faces);
```

Es importante saber, más delante donde se iteran los rostros detectados uno por uno, que tenemos que estirar o reducir el tamaño del rostro detectado para que concuerden al tamaño de las imágenes que le dimos al modelo que entrenamos.

```
cv::Mat face_resized;
cv::resize(face, face_resized, cv::Size(_im_width, _im_height), 1.0, 1.0, cv::INTER_CUBIC);
```

Podrás buscar el código de arriba más delante en:

![faces-part2.PNG](/uploads/faces-part2.PNG)

Y finalmente obtenemos el índice del rostro detectado y su nivel de certeza:

```
double confidence = 0.0;

int prediction = 0;
_model->predict(face_resized, prediction, confidence);

if (confidence < 11000) {
	prediction = 0;
}
else {
	prediction = 1;
}
```

En un principio no me funcionó el algoritmo con la predicción con el índice correcto (que resulta ser el que le pasas en el archivo separado por comas) y siempre me daba el segundo valor de las dos secuencias de imágenes de entrenamiento. Esto es posible repararlo con imágenes más certeras y reducidas de tamaño (que incluyan el rostro sin cuerpo, por ejemplo), por ahora utilicé el nivel de certeza (confidence) a ser un valor aproximado a 11000 para detectar que no se trataba de Jennette McCurdy sino de mi, el nivel de certeza nos brinda información sobre que tan seguro está el detector de indicarnos si el rostro le pertenece o no a una persona.

En fin. Al terminar simplemente le agregamos un rectángulo verde al rostro que detectamos, face_i es el de tamaño completo, más delante verás que el tamaño completo NO es el que estiramos o reducimos de tamaño sino el que posee la cámara y al cual le asignamos el rectángulo.

![faces-part3.PNG](/uploads/faces-part3.PNG)

Agregamos el texto en la posición superior derecha con:

```
putText(original,
	box_text,
	cv::Point(pos_x, pos_y),
	cv::FONT_HERSHEY_PLAIN,
	1.0,
	CV_RGB(0, 255, 0), 2.0);
```

Y devolvemos la matriz computada al final de la función.

¿El resultado? 

Jennette McCurdy y yo en una linda foto con nuestros nombres.

![predictions-5b8a5f.png](/uploads/predictions-5b8a5f.png)

Recuerda que puedes cambiar el algoritmo de detección de entrenado a sin entrenar con la booleana untrainedRecognition dentro de Arduino_GUI.cpp en:

```
if (untrainedRecognition) {
	if (bSuccess) {
		detection = untrained_detector.detect(frame);
	}
	else {
		detection = frame;
	}

}
else {
	auto rectangles = trained_detector.detect_face_rectangles(frame);
	cv::Scalar color(0, 105, 205);
	int frame_thickness = 4;
	for (const auto& r : rectangles) {
		cv::rectangle(frame, r, color, frame_thickness);
	}

	detection = frame;
}
```

Pero solamente si usas el algoritmo no-entrenado podrás tener la identificación de los rostros.

Más delante, y cuando haya reparado los errores de detección, veremos como activar circuitos en el dispositivo Arduino en base al rostro que se detecta, esto puede ser útil, por ejemplo, para abrir puertas o ejecutar programas según llegue el dueño u otra persona (o incluso bloquear el equipo), las posibilidades son muy amplias.




