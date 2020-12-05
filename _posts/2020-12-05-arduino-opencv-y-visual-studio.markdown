---
title: Arduino, OpenCV y Visual Studio
date: 2020-12-05 06:42:00 Z
published: false
categories:
- Development
- Robotics
tags:
- Arduino
- OpenCV
- Visual Studio
Field name:
  image:
    url: "/uploads/ArduinoUnoSMDFront.jpg"
---

<div>
    <script>
        $(function() {
            console.log('dom ready');
            $("meta[name='twitter:card']").attr('content', 'summary_large_image')
            $("meta[name='twitter:image']").attr('content', 'https://greentwip.xyz/uploads/ArduinoUnoSMDFront.jpg')

        });
    </script>
</div>
![ArduinoUnoSMDFront.jpg](/uploads/ArduinoUnoSMDFront.jpg)
¿Nunca te has preguntado que podrías hacer con un semiconductor si tuvieras la oportunidad de cambiar el código fuente a tu antojo?

Bueno, pues con Arduino esto es una opción muy real. Arduino es un sistema de tarjetas de hardware abierto, dispositivos embebidos, que te permiten, mediante sus pines de entrada y salida, crear circuitos eléctricos con una facilidad increíble.

En este post vamos a averiguar cómo podemos comunicarnos con Arduino mediante simple comunicación serial. No vamos a adentrarnos en cómo está hecha la biblioteca que usamos para comunicarnos ni tampoco vamos a indagar dentro del sistema de UI que usaremos.

Puedes descargar el proyecto completo desde aquí.

Utilizaremos:

Visual Studio 2019
OpenCV 3.4.1 (compilamos desde la fuente)
[SerialPort](https://github.com/manashmandal/SerialPort) de manashmandal
[cvui](https://dovyski.github.io/cvui/) de dovyski

Podría hacer una lista larga acerca de cómo compilar con CMake, pero por ahora basta y sobra con descargar el proyecto y prestar atención en cada una de las partes del código. 

Si no quieres seguirte todo el post porque estás ansioso y sólo quieres ver el programa en ejecución pues bien, adelante, únicamente abre Arduino_GUI.sln, compila y ejecuta, tardará tal vez algunos cuantos bastantes minutos en compilar todo OpenCV pero estará bien.



