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

