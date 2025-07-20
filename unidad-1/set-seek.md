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
https://editor.p5js.org/zeimer2020/sketches/u9FS5sDCy



``` javascript

function setup() {
  createCanvas(400, 400);
  
}

function draw() {
  background(100,30);

  
  fill(random(255), random(255), random(255), 50);
 
  if (random(0,1) < 0.5) {
    circle(random(0,400), random(0,400), random(10,70));
  } else {
    square(random(0,400), random(0,400), random(10, 42));
  }
}
```

<img width="405" height="396" alt="image" src="https://github.com/user-attachments/assets/6a028cc9-a70a-4da2-89e3-5c1f0df9d6ea" />











