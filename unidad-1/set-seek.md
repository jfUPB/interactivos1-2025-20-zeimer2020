# Unidad 1

## 🔎 Fase: Set + Seek

### Actividad 1


#### ¿Qué es un sistema físico interactivo?
Un sistema fisico interactivo es un conjunto de sensores y motor de computadora que reaccionan al mundo real, ya sea mover la mano y que cambie la luz o que al hacer algun sonido haya alguna reaccion.

#### ¿Cómo podrías aplicar lo que has visto en tu perfil profesional?
creando espectaculos para conciertos o discotecas.

### Actividad 2



#### ¿Qué es el diseño/arte generativo?

El diseño o arte generativo es una forma de creación en la que se usan algoritmos o sistemas automatizados (como código, inteligencia artificial) para generar obras visuales, sonoras o interactivas, a menudo cosas aleatorias

#### ¿Cómo podrías aplicar lo que has visto en tu perfil profesional?

En galerias de arte, en programas generadores o para algun proyecto de algun tipo de muestra


### Actividad 3


### En este sistemas físico interactivo identifica los inputs, outputs y el proceso.

Inputs: Serial, el codigo. presionar A, B o sacudir

Outputs: Encendido o apagado de las luces leds, mostrar las letras A, B o C en el circulo

Proceso: el Programa y la asimilacion del codigo


### Actividad 4

link a proyecto:
https://editor.p5js.org/zeimer2020/sketches/NEcDb5JVP

``` javascript

function setup() {
  createCanvas(800, 800);
  background(0);
  noStroke();
}

function draw() {
  background(0, 30); 

  for (let i = 0; i < 20; i++) {
   
    fill(
      128 + 127 * sin(frameCount * 0.03 + i), 128 + 127 * sin(frameCount * 0.04 + i), 255+ 127 * sin(frameCount * 0.04 + i),
      150
    );

    if (i < 10) {
      
      circle(
        400 + sin(frameCount * 0.04
                      + i) * 300,
         400 + cos(frameCount * 0.06 + i) * 300,
        20 + sin(frameCount * 0.04 + i) * 10
      );
    } else {square(
        400 + sin(frameCount * 0.06 + i) * 300 ,
       400 + cos(frameCount * 0.04 + i) * 300 ,
  20 + sin(frameCount * 0.05 + i) * 10
      );
    }
  }
}


```

<img width="794" height="732" alt="image" src="https://github.com/user-attachments/assets/ef47e5c7-aaa2-474c-af0a-da46de483d02" />


### Actividad 5

Sistema fisico interactivo creado (parte de la biblioteca importada)

``` javascript
from microbit import *

uart.init(baudrate=115200)

while True:

    if button_a.is_pressed():
        uart.write('A')
    else:
        uart.write('N')

    sleep(100)



```

Este sistema usa el micro:bit para detectar si se presiona el boton A. Si el boton A esta siendo presionado, el micro:bit envia la letra 'A' si no se presiona, envia la letra 'N'.

Todo esto se hace por el programa escrito en Python, que se repite todo el tiempo gracias al while True. Esto lo convierte en un sistema fisico interactivo porque:

Recibe una entrada fisica cuando se presiona un boton, procesa esa informacion con un programa y responde enviando un mensaje a otro dispositivo.






