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


