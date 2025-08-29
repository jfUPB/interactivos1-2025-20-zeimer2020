# Evidencias de la unidad 4

## Código

[Enlace a la aplicación a modificar](URL)

Código a modificar:

``` js
'use strict';

if (typeof window.gd === 'undefined') {
  window.gd = {
    timestamp: function () {
      const d = new Date();
      const pad = (n, z = 2) => ('00' + n).slice(-z);
      return d.getFullYear().toString()
        + pad(d.getMonth() + 1)
        + pad(d.getDate()) + '_'
        + pad(d.getHours())
        + pad(d.getMinutes())
        + pad(d.getSeconds());
    }
  };
}

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

const btnX = 10, btnY = 10, btnW = 160, btnH = 30;

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
        if (btnA) filled = false;
        if (btnB) filled = true;
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

  noStroke();
  fill(255);
  rect(btnX, btnY, btnW, btnH, 5);
  stroke(0);
  noFill();
  rect(btnX, btnY, btnW, btnH, 5);
  noStroke();
  fill(0);
  textAlign(CENTER, CENTER);
  textSize(12);
  text(portOpened ? 'micro:bit conectado' : 'Conectar micro:bit', btnX + btnW/2, btnY + btnH/2);
}

function mousePressed() {
  if (mouseX >= btnX && mouseX <= btnX + btnW && mouseY >= btnY && mouseY <= btnY + btnH) {
    if (!portOpened) {
      port = createSerial();
      port.open('MicroPython', 115200);
      portOpened = true;
    }
    return;
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

[Enlace a la aplicación modificada](URL)

Código modificado:

``` js

```

## Video

[Video demostratativo](URL)


