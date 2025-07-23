# Unidad 1

## 🔎 Fase: Set + Seek

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
El sistema fisico interactivo que creamos funciona con un micro:bit y un programa en la computadora. El micro:bit detecta si se esta presionando el boton A y envia una letra "A" si el boton esta presionado o "N" si no lo esta. La Pc recibe esa letra por medio de un programa hecho en JavaScript y muestra un cuadro en la pantalla, rojo si recibe "A" y verde si recibe "N". Asi, el sistema detecta una accion fisica, la procesa y da una respuesta visual, lo que lo convierte en un sistema fisico interactivo.

### Actividad 6

link al codigo 

https://editor.p5js.org/zeimer2020/sketches/sCw4B9c37

``` javascript
let port;
let reader;
let x = 200;

function setup() {
  createCanvas(400, 400);

  createButton("Conectar").mousePressed(async () => {
    port = await navigator.serial.requestPort();
    await port.open({ baudRate: 115200 });
    reader = port.readable.getReader();
    leer();
  });
}

function draw() {
  background(220);
  circle(x, 200, 50);
}

async function leer() {
  while (true) {
    const { value, done } = await reader.read();
    if (done) break;
    let letra = new TextDecoder().decode(value).trim();
    if (letra == "A") x -= 10;
    if (letra == "B") x += 10;
    x = constrain(x, 0, width);
  }
}
```
``` python
from microbit import *

uart.init(baudrate=115200)

while True:
    if button_a.is_pressed():
        uart.write("A")
    elif button_b.is_pressed():
        uart.write("B")
    sleep(100)
```


