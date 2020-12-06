---
title: Reconocimiento Facial con OpenCV
date: 2020-12-06 08:24:00 Z
published: false
categories:
- Development
- Robotics
tags:
- OpenCV
- Algoritmos
- Reconocimiento Facial
- C++
---

En el post anterior logramos configurar OpenCV para utilizarlo con Visual Studio, en esta ocasión comenzaremos un pequeño proyecto sobre cómo detectar rostros mediante una red neural profunda (dnn o Deep Neural Network) precomputada para el reconocimiento facial.

El archivo completo, como de costumbre, lo puedes encontrar aquí.

Esto no es tan complicado como suena y tenemos dos alternativas, reconocimiento facial entrenado y reconocimiento facial sin entrenar.

El reconocimiento sin entrenar hace uso de CascadeClassifier que es una clase de datos que reconoce objetos dentro de un stream de imágenes mientras que el reconocimiento entrenado hace uso de blobs y modelos pre-entrenados, aunque es posible también generar nuestros modelos, entrenarlos y distribuirlos.

FaceDetector es la única clase de la que nos tenemos que preocupar, que es el algoritmo que se comprueba funciona correctamente sin problemas para imágenes dinámicas o variadas, mientras que el algoritmo no entrenado puede funcionar perfecto para imágenes estáticas.

Para no hacer largo el tema tenemos el constructor:

![constructor.PNG](/uploads/constructor.PNG)

La primera parte simplemente carga las rutas, haciendo uso de la cabecera filesystem sólo disponible en C++17, y la segunda parte se encarga de cargar la red neural y comprobar que no existan errores (de todas formas OpenCV simplemente tira una excepción si el formato no es correcto y la ejecución termina).

Los mean values o valores promedio son un cálculo de todas las sesiones de imágenes de entrenamiento en sus canales RGB, es decir Rojo, Verde y Azul en valor promedio de todo lo que se calculó, por lo que en otros modelos entrenados estos valores pueden cambiar y es necesario tomar nota de ellos según se entrene el modelo.

![detect_formatted.PNG](/uploads/detect_formatted.PNG)

En la función detect_face_rectangles lo primero que vemos es network_.setInput, que toma de entrada el blob creado por la imagen que estamos capturando directo de la cámara y hace referencia al nombre de la entrada en nuestro prototxt que es la descripción de la red neural, así se llama "data" y puedes abrir deploy_lowres.prototxt si eres curioso.

Luego viene network_.forward, que realiza una salida con la layer descrita en el prototxt de nombre "detection_out" que es el valor de salida que obtenemos después de todo el procesamiento.

Después se itera la matriz resultante, cada fila de la matriz representa una detección (un rostro encontrado), y si éste supera el nivel de certeza establecido, creamos un rectángulo para dibujar. confidence_threshold_, un valor medio de 0.5 a 1.0 donde 0 es nada de certeza en la detección y 1 es total certeza.

Y ya. Eso es todo lo que se necesita para reconocer un rostro, finalmente asignamos un grosor en los rectángulos que vamos a dibujar y se los dibujamos al frame, imagen capturada desde la cámara.

![detection_show.PNG](/uploads/detection_show.PNG)

Finalmente obteniendo el resultado:

![recognition.png](/uploads/recognition.png)

¿Puedes ver mi rostro?, seguro que también a ti te reconocerá.

Eso ha sido todo por hoy, más delante intentaremos hacer detecciones en imágenes estáticas con y sin entrenamiento. Posiblemente también hagamos uso de Arduino para poder abrir o cerrar circuitos o simular el desbloqueo de un teléfono con reconocimiento facial.

El código se atribuye a Benjamin Wagner, en su post de [Medium](https://medium.com/analytics-vidhya/building-a-face-detector-with-opencv-in-c-8814cd374ea1), gracias a él pudimos crear este post en Español.