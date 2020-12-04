---
title: "¿Cómo configurar OpenCV con MinGW?"
date: 2020-12-04 04:49:00 Z
published: false
---

Bien, es momento de un poco de robótica. En los siguientes días estaré publicando sobre programación con Arduino, ¿Suena interesante?

Bien. Esta vez, y antes de adentrarnos al Machine Learning o cualquiera de esas cosas que tal vez no cubra en lo inmediato, configuraremos una simple cámara dentro de una aplicación escrita en C++.

Si no conoces OpenCV bueno... Es una biblioteca de procesamiento de imágenes súper rápida y compatible con una infinidad de sistemas operativos, es capaz de realizar, también, procesamiento inteligente de imágenes, éstas pueden venir de diferentes entradas, Arduino como será en estos casos, pero eso vendrá en un post futuro.

![opencv.png](/uploads/opencv.png)

Esto es meramente demostrativo. En la práctica real NO suele utilizarse Dev-C++ para programar esta clase de programas pero si recién comienzas te ahorrarás mucho y podrás programar de inmediato. El setup recomendado es CMake + Visual Studio (del 2019 para acá).

Necesitarás las bibliotecas de OpenCV 3.4.1(si, también llamadas por vicio librerías) 

Las puedes encontrar directamente desde [este vínculo](https://dl.dropbox.com/s/5nmlr8m9c0vydjk/OpenCV-MinGW-Build-OpenCV-3.4.1-x64.zip?dl=0)

O también las puedes clonar con git desde el repositorio de [huihut](https://github.com/huihut/OpenCV-MinGW-Build/tree/OpenCV-3.4.1-x64/x64/mingw)

```
git clone -b OpenCV-3.4.1 https://github.com/huihut/OpenCV-MinGW-Build.git
```

Si ya instalaste Dev-C++ y creaste un proyecto lo demás es sencillo, tan sólo necesi


