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

