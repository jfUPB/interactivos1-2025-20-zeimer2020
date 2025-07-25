# Unidad 1

## 🛠 Fase: Apply

### Actividad 5

``` javascript
from microbit import *

uart.init(baudrate=115200)

while True:

    if button_a.is_pressed():
        uart.write('A')
    else:
        uart.write('N')

    sleep(100)

  let port;
  let connectBtn;
  let connectionInitialized = false;

  function setup() {
    createCanvas(400, 400);
    background(220);
    port = createSerial();
    connectBtn = createButton("Connect to micro:bit");
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);
  }

  function draw() {
    background(220);

    if (port.opened() && !connectionInitialized) {
      port.clear();
      connectionInitialized = true;
    }

    if (port.availableBytes() > 0) {
      let dataRx = port.read(1);
      if (dataRx == "A") {
        fill("red");
      } else if (dataRx == "N") {
        fill("green");
      }
    }

    rectMode(CENTER);
    rect(width / 2, height / 2, 50, 50);

    if (!port.opened()) {
      connectBtn.html("Connect to micro:bit");
    } else {
      connectBtn.html("Disconnect");
    }
  }

  function connectBtnClick() {
    if (!port.opened()) {
      port.open("MicroPython", 115200);
      connectionInitialized = false;
    } else {
      port.close();
    }
  }
```
El sistema fisico interactivo que creamos funciona con un microbit y un programa en la computadora. El microbit detecta si se esta presionando el boton A y envia una letra A si el boton esta presionado o N si no lo esta. La Pc recibe esa letra por medio de un programa hecho en javascript y muestra un cuadro en la pantalla, rojo si recibe A y verde si recibe N. Asi, el sistema detecta una accion fisica, la procesa y da una respuesta en la pantalla.

### Actividad 6

link al codigo 

https://editor.p5js.org/zeimer2020/sketches/sCw4B9c37

``` javascript
let port;
let connectBtn;
let connectionInitialized = false;
let dirX = 200;

function setup() {
  createCanvas(400, 400);
  background(200);
  port = createSerial();
  connectBtn = createButton('Connect to micro:bit');
  connectBtn.position(80,300);
  connectBtn.mousePressed(connectBtnClick);
}

function draw() {
  background(220);

  if (port.opened() && !connectionInitialized) {
    port.clear();
    connectionInitialized = true;
  }
  if (port.availableBytes() > 0 ){
    let dataRx = port.read(1);
    if (dataRx == 'A' && dirX > 50){
      dirX -= 10;
    }
    else if (dataRx == 'B' && dirX < 350){
      dirX += 10;
    } 
  }
    stroke(100)
    fill('purple')
    ellipseMode(RADIUS);
    ellipse(dirX, height / 2, 50, 50);
    if (!port.opened()){
      connectBtn.html("Connect to Micro:bit");
    } else{
      connectBtn.html("Disconnect");
    }

  text(dirX, 50, 50)
}
function connectBtnClick(){
  if(!port.opened()){
    port.open('MicroPython', 115200);
    connectionInitialized = false;
  } else {
    port.close();
  }
}
```
``` python
from microbit import *
uart.init(baudrate=115200)

display.show(Image.HAPPY)

while True:
    if (button_a.is_pressed()):
        uart.write('A')
    if (button_b.is_pressed()):
        uart.write('B')
    else:
        uart.write('N')
    sleep(100)
```

Este codigo hace que el microbit pueda mover un circulo en la pantalla del computador cuando se oprime el boton A del microbit, este manda una letra A, y si se oprime el boton B, manda una B. En el computador hay un programa que dibuja un circulo y, al darle al boton Conectar, empieza a escuchar lo que manda el microbit. Si llega una A, el circulo se va a la izquierda si llega una B, se va a la derecha. Es como si el microbit fuera un control para mover el circulo a los lados.
