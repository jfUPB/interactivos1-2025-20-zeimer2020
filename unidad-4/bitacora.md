# Evidencias de la unidad 4

## Código

[Enlace a la aplicación a modificar](URL)
https://editor.p5js.org/generative-design/sketches/HkrbeqqqTJV

Código a modificar:

``` js
// P_2_2_3_01
//
// Generative Gestaltung – Creative Coding im Web
// ISBN: 978-3-87439-902-9, First Edition, Hermann Schmidt, Mainz, 2018
// Benedikt Groß, Hartmut Bohnacker, Julia Laub, Claudius Lazzeroni
// with contributions by Joey Lee and Niels Poldervaart
// Copyright 2018
//
// http://www.generative-gestaltung.de
//
// Licensed under the Apache License, Version 2.0 (the "License");
// you may not use this file except in compliance with the License.
// You may obtain a copy of the License at http://www.apache.org/licenses/LICENSE-2.0
// Unless required by applicable law or agreed to in writing, software
// distributed under the License is distributed on an "AS IS" BASIS,
// WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
// See the License for the specific language governing permissions and
// limitations under the License.

/**
 * form mophing process by connected random agents
 *
 * MOUSE
 * click               : start a new circe
 * position x/y        : direction of floating
 *
 * KEYS
 * 1-2                 : fill styles
 * f                   : freeze. loop on/off
 * Delete/Backspace    : clear display
 * s                   : save png
 */
'use strict';

var formResolution = 15;
var stepSize = 2;
var distortionFactor = 1;
var initRadius = 150;
var centerX;
var centerY;
var x = [];
var y = [];

var filled = false;
var freeze = false;

function setup() {
  createCanvas(windowWidth, windowHeight);

  // init shape
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
  // floating towards mouse position
  centerX += (mouseX - centerX) * 0.01;
  centerY += (mouseY - centerY) * 0.01;

  // calculate new points
  for (var i = 0; i < formResolution; i++) {
    x[i] += random(-stepSize, stepSize);
    y[i] += random(-stepSize, stepSize);
    // uncomment the following line to show position of the agents
    // ellipse(x[i] + centerX, y[i] + centerY, 5, 5);
  }

  if (filled) {
    fill(random(255));
  } else {
    noFill();
  }

  beginShape();
  // first controlpoint
  curveVertex(x[formResolution - 1] + centerX, y[formResolution - 1] + centerY);

  // only these points are drawn
  for (var i = 0; i < formResolution; i++) {
    curveVertex(x[i] + centerX, y[i] + centerY);
  }
  curveVertex(x[0] + centerX, y[0] + centerY);

  // end controlpoint
  curveVertex(x[1] + centerX, y[1] + centerY);
  endShape();
}

function mousePressed() {
  // init shape on mouse position
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

  // pauze/play draw loop
  if (key == 'f' || key == 'F') freeze = !freeze;
  if (freeze) {
    noLoop();
  } else {
    loop();
  }
}


```

[Enlace a la aplicación modificada](URL)

https://editor.p5js.org/zeimer2020/sketches/746R5_qyN

Código modificado:

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

## Video

[Video demostratativo](URL)

https://youtu.be/3A4R9IRAQ7I





