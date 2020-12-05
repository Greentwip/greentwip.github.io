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

Si no quieres seguirte todo el post porque estás ansioso y sólo quieres ver el programa en ejecución pues bien, adelante, únicamente abre Arduino_GUI.sln, compila y ejecuta, tardará tal vez algunos cuantos bastantes minutos en compilar todo OpenCV pero estará bien, no olvides cambiar el puerto COM al que se ajuste a tu máquina.


Es importante que a la hora de compilar los sketches cambies la tarjeta Arduino a la que corresponde según tu modelo. Esto se hace desde acá:

![board.png](/uploads/board.png)

La línea más importante tal vez es
```
const char* portName = "\\\\.\\COM4";
```

El formato es extraño, ni yo sé por qué tiene tantas diagonales, lo importante es la parte final, hay que cambiar de
```
COM4
```
Al puerto que visualices en los dispositivos de sistema una vez te hayas instalado todo lo necesario para tu Arduino.

Tenemos de entrada un puntero inteligente, es lo mismo que un puntero sólo que la memoria se maneja de manera automática y por un sistema de referencias *demasiado complicado de explicar* pero fácil de entender.

```
std::shared_ptr<SerialPort> arduino;
```

Ese lo instanciamos por acá:

```
arduino = std::make_shared<SerialPort>(portName);
```

Una vez inicializada la conexión se llama a la función de cvui de inicialización con el nombre de nuestra ventana:

```
cvui::init(WINDOW_NAME, 20);
```

Y más delante la creamos con:

```
cv::namedWindow(WINDOW_NAME, CV_WINDOW_AUTOSIZE);
```

La parte más relevante del código que sigue tal vez sea:

```

		cvui::text(frame, 40, 40, "Click para comunicarse con Arduino");

		if (cvui::button(frame, 300, 80, "Encender")) {
			const char* sendString = "ON\n";
			bool hasWritten = arduino->writeSerialPort(sendString, DATA_LENGTH);
			if (hasWritten) std::cout << "Datos escritos correctamente" << std::endl;
			else std::cerr << "Datos no escritos" << std::endl;
		}


		if (cvui::button(frame, 300, 140, "Apagar")) {
			const char* sendString = "OFF\n";
			bool hasWritten = arduino->writeSerialPort(sendString, DATA_LENGTH);
			if (hasWritten) std::cout << "Datos escritos correctamente" << std::endl;
			else std::cerr << "Datos no escritos" << std::endl;
		}
```

Pues allí creamos la conexión de escritura a nuestro Arduino.

```
cvui::button(frame, 300, 80, "Encender")
```

Es verdadero si ha recibido un click, se crea a través de la matriz con la dimensión especificada, 300 y 80 son las coordenadas "X" y "Y" respectivamente y lo que sigue es simplemente la etiqueta o texto que contiene el botón.

Al sketch de Arduino le tenemos que mandar una cadena de texto con terminación \n porque representa un salto de línea que será posteriormente leído con:

```
  if (Serial.available() > 0){
    receivedString = Serial.readStringUntil('\n');
  }
```

Para enviarle la string tenemos que utilizar la función de SerialPort donde especificamos un tamaño máximo de buffer de tamaño DATA_LENGTH, nuestras strings no podrán ser más grandes que eso, a no ser que lo definamos de otra manera. De todas formas no se necesitan tantos datos para esta clase de dispositivos embebidos.

```
const char* sendString = "ON\n";
bool hasWritten = arduino->writeSerialPort(sendString, DATA_LENGTH);
```

Con eso encendemos el led.

Luego en el sketch:

```
  if (receivedString.equals("ON")) {
    digitalWrite(led, HIGH);
    Serial.print("ON");
    delay(DELAY_TIME);
  }
  else if (receivedString.equals("OFF")) {
    digitalWrite(led, LOW);
    Serial.print("OFF");
    delay(DELAY_TIME);
  }
```

Verifica las strings enviadas y asigna un valor HIGH al led especificado, definido como 13, el led que contiene la tablilla.

```
#define led 13
```




