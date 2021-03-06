---
title: "¿Cómo configurar OpenCV con MinGW?"
date: 2020-12-04 04:49:00 Z
categories:
- Development
- Robotics
tags:
- OpenCV
- C++
---

Bien, es momento de un poco de robótica. En los siguientes días estaré publicando sobre programación con Arduino, ¿Suena interesante?

Bien. Esta vez, y antes de adentrarnos al Machine Learning o cualquiera de esas cosas que tal vez no cubra en lo inmediato, configuraremos una simple cámara dentro de una aplicación escrita en C++.

Si no conoces OpenCV bueno... Es una biblioteca de procesamiento de imágenes súper rápida y compatible con una infinidad de sistemas operativos, es capaz de realizar, también, procesamiento inteligente de imágenes, éstas pueden venir de diferentes entradas, Arduino como será en estos casos, pero eso vendrá en un post futuro.

![opencv.png](/uploads/opencv.png)

Esto es meramente demostrativo. En la práctica real NO suele utilizarse Dev-C++ para programar esta clase de programas pero si recién comienzas te ahorrarás mucho y podrás programar de inmediato. El setup recomendado es CMake + Visual Studio (del 2019 para acá).

Si, el título tal vez es clickbait, pero en el fondo Dev-C++ trabaja con MinGW, por lo que esto también te funcionará incluso si trabajas con herramientas como Cygwin.

Necesitarás las bibliotecas de OpenCV 3.4.1(si, también llamadas por vicio librerías) 

Las puedes encontrar directamente desde [este vínculo](https://dl.dropbox.com/s/5nmlr8m9c0vydjk/OpenCV-MinGW-Build-OpenCV-3.4.1-x64.zip?dl=0)

O también las puedes clonar con git desde el repositorio de [huihut](https://github.com/huihut/OpenCV-MinGW-Build/tree/OpenCV-3.4.1-x64/x64/mingw)

```
git clone -b OpenCV-3.4.1 https://github.com/huihut/OpenCV-MinGW-Build.git
```

Si ya instalaste Dev-C++ y creaste un proyecto lo demás es sencillo, tan sólo necesitas crear un proyecto y configurar un par de cosas.

Este será el contenido de main.cpp:

```
#include <stdio.h>
#include <iostream>
#include "opencv2/core/core.hpp"
#include "opencv2/features2d/features2d.hpp"
#include "opencv2/highgui/highgui.hpp"

int main(int argc, char* argv[])
{
	int method = 0;
	cv::VideoCapture cap(0); // open the video capture for reading
	if ( !cap.isOpened() ) // if not success, exit program
	{
		std::cout << "Cannot open the video file" << std::endl;
		return -1;
	}
	
	cv::namedWindow("MyVideo",CV_WINDOW_AUTOSIZE);
	while(1)
	{
		cv::Mat frame;
		bool bSuccess = cap.read(frame);
		cv::imshow("MyVideo", frame);
		if(cv::waitKey(30) == 27)
		{
			std::cout << "esc key is pressed by user" << std::endl;
			break;
		}
	}
	return 0;
}
```

Tendrás que agregar los Include Directories de la siguiente forma (menú Project->Project Options...)

![opencv.png](/uploads/opencv.png)

Luego tendrás que linkear las bibliotecas correspondientes:

![dev-C  -opencv-libraries.PNG](/uploads/dev-C%20%20-opencv-libraries.PNG)

Para eso tendrás que referenciar presionando en el botón "Add library or object", navegar a la carpeta opencv\x64\mingw\lib (te recomiendo usar una ruta para opencv en C:\Binaries o C:\Dev, según tu gusto).

Finalmente copia todo el contenido de opencv\x64\mingw\bin a tu carpeta del proyecto Dev-C++, algo así:

![opencv-binaries-dev_cplusplus.PNG](/uploads/opencv-binaries-dev_cplusplus.PNG)

Si haz seguido bien los pasos todo saldrá bien. Tan sólo selecciona la opción del menú Execute -> Compile y luego Execute -> Run.

Tendrás una ventana con la salida de imagen de tu cámara:

![opencv-dev_cplusplus-execution.PNG](/uploads/opencv-dev_cplusplus-execution.PNG)

Y ya está.


