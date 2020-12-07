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

