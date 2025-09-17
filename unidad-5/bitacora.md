
# Evidencias de la unidad 5

#### Actividad 2

en texto
<img width="1202" height="202" alt="image" src="https://github.com/user-attachments/assets/8090985d-1d86-48e8-9505-89269958c6f4" />
en hex
<img width="1211" height="197" alt="image" src="https://github.com/user-attachments/assets/dd413e4e-b1d7-4d65-a532-6a53c7162312" />

me imagino que estara relacionado con el tipo de datos que envia el microbit? pues lo que se envia y los que recibe la aplicacion de conexion.

las ventajas que tiene usar lenguaje binario en lugar de ascii es que los datos se guardan tal cual, ocupan menos espacio, el sistema puede leer mas rapido e interpreta insntataneamente pq no debe traducirlo ya que esta en binario

<img width="636" height="43" alt="image" src="https://github.com/user-attachments/assets/562bdb25-d0a2-41ed-92f1-4606dc224324" />

no me queda del todo claro lo que es, sin embargo entiendo por el inicio que sera mas directamente un 2h2b en lenguaje, y cada vez que lo sacudo me da esos simbolos.

Recuerda de la unidad anterior que es posible enviar números positivos y negativos para los valores de xValue y yValue. ¿Cómo se verían esos números en el formato '>2h2B'?


se verian con los simbolos que no se pueden definir en la aplicacion de conexion o directamente ser verian traducidos de otra forma para el programa

Qué ventajas y desventajas ves en usar un formato binario en lugar de texto en ASCII?

se puede notar una diferencia de velocidad clara, cuando lo probaba con el binario era mas instantaneo, sin embargo es mas complejode leer y menos entendible

¿Qué ventajas y desventajas ves en usar un formato ASCII en lugar de binario?

una de las ventajas que veo es que es muchisimo mas facil de entender, es mas intuitivo por asi decirlo, sin embargo se demoraba mas en enviar el mensaje, esto imagino sera por la traduccion que debe hacer el sistema.

#### Actividad 3 

Explica por qué en la unidad anterior teníamos que enviar la información delimitada y además marcada con un salto de línea y ahora no es necesario.

como yo lo interpreto es que era pq en una estabamos viendo


##### Explica por qué en la unidad anterior teníamos que enviar la información delimitada y además marcada con un salto de línea y ahora no es necesario.

lo que entiendo es que se debe a que ahora que usamos binario el programa peude entender mas directamente lo que estamos enviando, ademas de que en binario lo que enviemos pesa muchisimo menos

#### Compara el código de la unidad anterior relacionado con la recepción de los datos seriales que ves ahora. ¿Qué cambios observas?

el tipo de datos que recibe ahora son distintos, me genera un poco de problemas entender como esta reciviendo este tipo de lenguaje pero voy captando que es mas rapido y directo


##### Diferencias entre datos y demas cositas entre cada codigo


al inicio estamos viendo principalmente una verificacion de que tipo de datos recibe, estamos "quemando" los datos y entradas para verificar, uno de los codigos nos da datos mas directos de la posicion del microbit, que botones estan presionadso, si esta listo para dibujar y datos mas especificos, mientras que el otro

<img width="821" height="111" alt="image" src="https://github.com/user-attachments/assets/57086b3e-2f9e-40a2-b825-193c20d5c1f9" />

ya con el otro siendo una version final recibe los datos y el feedback que nos da es mas condensado, recibe los datos del microbit y genera las imagenes pedidas y se guia con el virtual mouse que hacemos con el microbit o mas bien el acelerometro
<img width="1585" height="174" alt="image" src="https://github.com/user-attachments/assets/a6634484-5452-4788-a540-cebb53f7181a" />


### transformacion del codigo generativo para que reciba datos en binario


``` python
from microbit import *
import struct

uart.init(115200)
display.set_pixel(0, 0, 9)

while True:
    xValue = accelerometer.get_x()
    yValue = accelerometer.get_y()
    aState = button_a.is_pressed()
    bState = button_b.is_pressed()
    data = struct.pack('>2h2B', xValue, yValue, int(aState), int(bState))
    checksum = sum(data) % 256
    packet = b'\xAA' + data + bytes([checksum])
    uart.write(packet)
    sleep(100)
```

primero intento de binario en p5:js

<img width="892" height="706" alt="image" src="https://github.com/user-attachments/assets/f2d47965-507f-4c83-a0d0-96c9f095f7e5" />
teniendolo ya conectado con el microbit no se movia, se quedaba ahi abajo la continuidad del programa y no avanzaba, empece a revisar de nuevo el github y busque en internet y me di cuenta de que uno de los errores que estaba cometiendo era que tenia el programa recibiendo binario, pero habia quitado la opcion de que el programa fuera manejable por el microbit, entonces recibia datos en binario pero no tenia como manera de ser controlado por el microbit


``` js
'use strict';

var formResolution = 15;
var stepSize = 2;
var distortionFactor = 1;
var initRadius = 150;
var centerX, centerY;
var x = [];
var y = [];
var filled = false;
var freeze = false;

let port;
let accX = 0, accY = 0;
let btnA = false, btnB = false;
let virtMouseX = null, virtMouseY = null;
let easing = 0.08;
let portOpened = false;

function setup() {
  createCanvas(windowWidth, windowHeight);
  centerX = width / 2;
  centerY = height / 2;
  var angle = radians(360 / formResolution);
  for (var i = 0; i < formResolution; i++) {
    x.push(cos(angle * i) * initRadius);
    y.push(sin(angle * i) * initRadius);
  }
  stroke(0, 50);
  strokeWeight(0.75);
  background(255);
}

function draw() {
  if (port && port.available && port.available() > 0) {
    let line = port.readUntil("\n");
    if (line && line.length > 0) {
      line = line.trim();
      const parts = line.split(',');
      if (parts.length === 4) {
        const px = parseInt(parts[0], 10);
        const py = parseInt(parts[1], 10);
        const pa = (parts[2] === 'True' || parts[2] === '1' || parts[2] === 'true');
        const pb = (parts[3] === 'True' || parts[3] === '1' || parts[3] === 'true');
        if (!Number.isNaN(px)) accX = px;
        if (!Number.isNaN(py)) accY = py;
        btnA = !!pa;
        btnB = !!pb;
        const mx = map(accX, -1024, 1024, 0, width, true);
        const my = map(accY, -1024, 1024, 0, height, true);
        if (virtMouseX === null || virtMouseY === null) {
          virtMouseX = mx;
          virtMouseY = my;
        } else {
          virtMouseX += (mx - virtMouseX) * easing;
          virtMouseY += (my - virtMouseY) * easing;
        }
        if (btnA) {
          filled = false;
          console.log("Boton A presionado en el micro:bit");
        }
        if (btnB) {
          filled = true;
          console.log("Boton B presionado en el micro:bit");
        }
      }
    }
  }

  const targetX = (virtMouseX === null) ? mouseX : virtMouseX;
  const targetY = (virtMouseY === null) ? mouseY : virtMouseY;
  centerX += (targetX - centerX) * 0.01;
  centerY += (targetY - centerY) * 0.01;

  for (var i = 0; i < formResolution; i++) {
    x[i] += random(-stepSize, stepSize);
    y[i] += random(-stepSize, stepSize);
  }

  if (filled) {
    fill(random(255));
  } else {
    noFill();
  }

  beginShape();
  curveVertex(x[formResolution - 1] + centerX, y[formResolution - 1] + centerY);
  for (var j = 0; j < formResolution; j++) {
    curveVertex(x[j] + centerX, y[j] + centerY);
  }
  curveVertex(x[0] + centerX, y[0] + centerY);
  curveVertex(x[1] + centerX, y[1] + centerY);
  endShape();
}

function mousePressed() {
  if (!portOpened) {
    port = createSerial();
    port.open('MicroPython', 115200);
    portOpened = true;
  }
  centerX = mouseX;
  centerY = mouseY;
  var angle = radians(360 / formResolution);
  var radius = initRadius * random(0.5, 1);
  for (var i = 0; i < formResolution; i++) {
    x[i] = cos(angle * i) * initRadius;
    y[i] = sin(angle * i) * initRadius;
  }
}

function keyReleased() {
  if (key == 's' || key == 'S') saveCanvas(gd.timestamp(), 'png');
  if (keyCode == DELETE || keyCode == BACKSPACE) background(255);
  if (key == '1') filled = false;
  if (key == '2') filled = true;
  if (key == 'f' || key == 'F') {
    freeze = !freeze;
    if (freeze) noLoop(); else loop();
  }
}

function windowResized() {
  resizeCanvas(windowWidth, windowHeight);
}
```
ya ahora si el codigo se deja controlar por el microbit y recibe los datos en binario, se puede ver abajo en el registro de consola
<img width="854" height="727" alt="image" src="https://github.com/user-attachments/assets/02bd9e39-e0b5-4ed5-8291-c774501b0c13" />

<img width="1765" height="750" alt="image" src="https://github.com/user-attachments/assets/b5cdf54e-8fcf-4b8d-bc11-bc4279ca7349" />

aqui ya se ve como la control con el microbit y abajo coloque para que no codificara los datos en el registro si no que nos los muestre en crudo para poder ver que si esta agarrando todo directamente en binario


https://stackoverflow.com/questions/14430633/how-to-convert-text-to-binary-code-in-javascript

use este link para enterarme de algunas cosas en el jv 


