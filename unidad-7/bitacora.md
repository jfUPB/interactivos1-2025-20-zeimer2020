
# Evidencias de la unidad 7


<a name = "actividad1"> </a>

### ¿Qué URL de Dev Tunnels obtuviste? ¿Por qué crees que necesitamos usar esta URL en lugar de http://localhost:3000 o la IP local de tu computador para que el celular se conecte?

obvtuve dos, una fue https://n8xm1p1z-3000.use2.devtunnels.ms/mobile/ y la otra era la del loclahost pero habia que colocarle mobile a la del celular y desktop a la otra, entiendo que eran estas dos para que funcionara en cada dispositivo

### Describe brevemente qué hace npm install y npm start.

El npm install se encarga de instalar codigos y funciones del repositorio copiado desde el github en las carpetas designadas, el npm start inicializa los codigos y los servidores que indiquen los codigos y datos descargados del githuh

### ¿Qué mensajes observaste en la terminal del servidor al conectar el cliente de escritorio y el cliente móvil? ¿Eran diferentes los mensajes o identificadores?

 <img width="443" height="78" alt="image" src="https://github.com/user-attachments/assets/44fe80af-7884-42cb-804f-2be1c7d5cccc" />


### Describe el comportamiento observado: ¿Funcionó la interacción? ¿Hubo algún retraso (latencia)?
hubo retraso de latencia pero en mi caso, en los pcs de mis compañeros no tanto, seria por la lenta conexion me imagino

<a name = "actividad2"> </a>


# Actividad 2

### Explica con tus propias palabras: ¿Por que es necesario Dev Tunnels en este escenario y como funciona conceptualmente?
Dev Tunnels expone tu servidor local a internet con una URL publica, atravesando NAT y firewalls; un servicio intermedio reenvia el trafico externo a tu puerto local

### Describe la funcion de touchMoved() y por que se usa la variable threshold en el cliente movil.
touchMoved() detecta arrastres del dedo y dispara actualizaciones; el threshold filtra cambios minimos para evitar ruido y reducir el numero de mensajes

### Compara brevemente Dev Tunnels con simplemente usar la IP local. Cuales son las ventajas y desventajas de cada uno?
IP local: baja latencia y simple, pero solo en la misma red y falla con NAT. Dev Tunnels: accesible desde cualquier red y con https, pero agrega latencia y depende del servicio

### Coloca en tu bitácora capturas de pantalla del sistema completo funcionando. Esto lo puedes hacer abriendo tanto el mobile como el desktop en tu computador y tomando una captura de pantalla de todos los involucrados (celular, computador y terminal).
<img width="594" height="475" alt="image" src="https://github.com/user-attachments/assets/f2f39711-9125-4da6-b8d1-f4fe0c73aa81" />
<img width="382" height="514" alt="image" src="https://github.com/user-attachments/assets/7cd2d769-8e57-4ad5-9815-246665d4b07e" />
<img width="516" height="312" alt="image" src="https://github.com/user-attachments/assets/15ee35af-ff36-40b7-95fd-47fbd6f63bb9" />


<a name = "actividad3"> </a>


# Actividad 3

### ¿Cual es la funcion principal de express.static(‘public’) en este servidor? ¿Como se compara con el uso de app.get(‘/ruta’, …) del servidor de la Unidad 6?
Sirve para mostrar archivos sin rutas manuales, a diferencia de app.get que define rutas una por una

### Explica detalladamente el flujo de un mensaje tactil: ¿Que evento lo envia desde el movil? ¿Que evento lo recibe el servidor? ¿Que hace el servidor con el? ¿Que evento lo envia el servidor al escritorio? ¿Por que se usa socket.broadcast.emit en lugar de io.emit o socket.emit en este caso?
El movil envia con socket.emit, el servidor recibe con socket.on y reenvia con socket.broadcast.emit a los demas

### Si conectaras dos computadores de escritorio y un movil a este servidor, y movieras el dedo en el movil, ¿Quien recibiria el mensaje retransmitido por el servidor? ¿Por que?
Los dos escritorios, porque broadcast no envia al emisor

### ¿Que informacion util te proporcionan los mensajes console.log en el servidor durante la ejecucion?
Muestran conexiones, desconexiones y mensajes recibidos


<a name = "actividad4"> </a>


# Actividad 4

#### Realiza un diagrama donde muestres el flujo completo de datos y eventos entre los tres componentes: móvil, servidor y escritorio. Puedes ilustrar con un ejemplo de coordenadas táctiles (x, y) y cómo viajan a través del sistema.

song = loadnSOund, esto en el prelouad, uas el instrumento de analizis fft, amplitude y el song.connect, en el drop (una funcion que se llamara en cada frame) se le dice al instrumento de analizis que la vaya analizando, a la cancion obviamente, 


<a name = "actividad5"> </a>


# Actividad 5


La cancion va del amor entonces use un electrocardiograma para representar el amor que se siente, ademas se llama i want it that way, de no rendirse y asi entonces pense que seria bueno aumentar o bajar la potencia del mismo

Apply



``` js

const express = require('express');
const http = require('http');
const { Server } = require('socket.io');

const app = express();
const server = http.createServer(app);
const io = new Server(server, { cors: { origin: true, methods: ['GET','POST'], credentials: true } });

app.use(express.static('public'));

io.on('connection', (socket) => {
  console.log('conectado', socket.id);
  socket.on('modeChange', (m) => {
    console.log('modeChange', m);
    io.emit('modeChange', m);
  });
  socket.on('disconnect', () => console.log('bye', socket.id));
});

server.listen(3000, '0.0.0.0', () => console.log('http://localhost:3000'));
```


``` js
let song, fft, amplitude;
let modeSel=1, ready=false;
let smoothY=[], cols=[[80,200,120],[120,180,255],[230,140,255]];
let prevLvl=0, beatPulse=0, parts=[];
let ctrlX=0.5, ctrlY=0.5, socketRef;
let modeFlash=0, modeText="";

function preload(){
  song = loadSound("../song.mp3", ()=>{ ready=true; }, ()=>{ ready=false; });
}

function setup(){
  createCanvas(windowWidth, windowHeight);
  fft=new p5.FFT(0.9,1024); fft.setInput(song);
  amplitude=new p5.Amplitude(); amplitude.setInput(song);
  song.connect();
  noFill(); strokeWeight(2);
  for(let i=0;i<45;i++){ parts.push({x:random(width),y:random(height),r:random(1.5,3.5),vx:random(-0.25,0.25),vy:random(-0.25,0.25),a:random(80,140)}); }
  socketRef = io();
  socketRef.on('touchData', d=>{ ctrlX=d.x; ctrlY=d.y; });
  socketRef.on('modeChange', m=>{ modeSel=m; modeText="MODO "+m; modeFlash=1; });
}

function draw(){
  background(10,28);
  drawParticles();
  if(ready){ drop(); } else { drawWaiting(); }
  drawModeTag();
}

function drawWaiting(){
  push();
  translate(width/2,height/2);
  noStroke();
  fill(230); textAlign(CENTER,CENTER);
  textSize(16); text("clic o toque para iniciar audio",0,22);
  stroke(220); noFill();
  let r=24;
  arc(0,0,r*2,r*2,frameCount*0.1,(frameCount*0.1)+PI*1.2);
  pop();
}

function drawParticles(){
  let lvl=amplitude.getLevel();
  let boost=map(lvl+beatPulse*0.6,0,0.3,0.9,1.8,true);
  for(let p of parts){
    p.x+=p.vx; p.y+=p.vy;
    if(p.x<-10)p.x=width+10; if(p.x>width+10)p.x=-10;
    if(p.y<-10)p.y=height+10; if(p.y>height+10)p.y=-10;
    let rr=p.r*boost;
    stroke(220,235,230,p.a*0.45); fill(220,235,230,p.a*0.18);
    ellipse(p.x,p.y,rr*2,rr*2);
  }
}

function drop(){
  let wave=fft.waveform(), mid=height*0.5;
  if(smoothY.length!==wave.length) smoothY=new Array(wave.length).fill(mid);
  let lvl=amplitude.getLevel(), c=cols[modeSel-1];
  stroke(c[0],c[1],c[2],230);
  if(lvl>0.12&&lvl>prevLvl) beatPulse=1; beatPulse*=0.9; prevLvl=lvl;

  if(modeSel===1){
    let g=map(lvl,0,0.25,0.5,1.0,true)*map(ctrlY,0,1,0.7,1.3,true);
    let w=width/(wave.length-1);
    beginShape();
    for(let i=0;i<wave.length;i++){
      let x=i*w;
      let sway=sin((i*0.01)+frameCount*0.01+ctrlX*PI)*2;
      let t=mid+(wave[i]*g*height*0.18)+sway;
      smoothY[i]=lerp(smoothY[i],t,0.12);
      vertex(x,smoothY[i]);
    }
    endShape();
  } else if(modeSel===2){
    let w=width/240;
    let spikeAmp=-map(beatPulse,0,1,0,height*0.35)*map(ctrlX,0,1,0.7,1.3,true);
    beginShape();
    for(let i=0;i<240;i++){
      let idx=floor(map(i,0,239,0,wave.length-1));
      let v=wave[idx];
      let q=floor(v*20)/20;
      let base=mid+q*height*0.08;
      let x=i*w;
      let y=base+(((i+floor(ctrlX*60))%30===15)?spikeAmp:0);
      vertex(x,y);
    }
    endShape();
  } else {
    let g=map(lvl,0,0.25,0.7,1.6,true)*map(ctrlY,0,1,0.7,1.3,true);
    let w=width/(wave.length-1);
    strokeWeight(4);
    stroke(c[0],c[1],c[2],180);
    beginShape();
    for(let i=0;i<wave.length;i++){
      let x=i*w;
      let bend=sin((i*0.03)+frameCount*0.02+ctrlX*TWO_PI)*6*(0.3+beatPulse*0.7);
      let y=mid+wave[i]*g*height*0.22+bend;
      vertex(x,y);
    }
    endShape();
    strokeWeight(2);
    stroke(c[0],c[1],c[2],90);
    beginShape();
    for(let i=0;i<wave.length;i++){
      let x=i*w;
      let bend=sin((i*0.03)+frameCount*0.02+ctrlX*TWO_PI)*6*(0.3+beatPulse*0.7);
      let y=mid-(wave[i]*g*height*0.22+bend);
      vertex(x,y);
    }
    endShape();
  }
  stroke(220,230,225,35);
  line(0,mid,width,mid);
}

function drawModeTag(){
  let c=cols[modeSel-1];
  noStroke(); fill(c[0],c[1],c[2],220);
  textSize(14); textAlign(LEFT,TOP);
  text("Modo "+modeSel,12,10);
  if(modeFlash>0){
    push();
    textAlign(CENTER,CENTER);
    textSize(min(width,height)*0.08);
    fill(c[0],c[1],c[2],220*modeFlash);
    text(modeText,width/2,height*0.12);
    pop();
    modeFlash*=0.92;
  }
}

function keyPressed(){ if(key==="1")modeSel=1; if(key==="2")modeSel=2; if(key==="3")modeSel=3; }
function mousePressed(){ userStartAudio(); getAudioContext().resume(); if(!song.isPlaying()) song.loop(); }
function touchStarted(){ userStartAudio(); getAudioContext().resume(); if(!song.isPlaying()) song.loop(); }
function windowResized(){ resizeCanvas(windowWidth, windowHeight); }
```

``` js
const socket = io();
let lastSend=0, minDt=16, lastX=0.5, lastY=0.5, thr=0.01;
const pad = document.getElementById('pad');
const hint = document.querySelector('.hint');

socket.on('connect', ()=>{ if(hint) hint.textContent='Conectado · Presiona con tu dedo para controlar'; });
socket.on('connect_error', e=>{ if(hint) hint.textContent='Sin conexion · Revisa la URL'; });

function sendPos(nx, ny){
  const now = performance.now();
  if(now-lastSend<minDt) return;
  if(Math.abs(nx-lastX)<thr && Math.abs(ny-lastY)<thr) return;
  lastSend=now; lastX=nx; lastY=ny;
  socket.emit('touchData', {x:nx, y:ny});
}

function toNorm(clientX, clientY){
  const rect = pad.getBoundingClientRect();
  const nx = Math.min(1, Math.max(0, (clientX-rect.left)/rect.width));
  const ny = Math.min(1, Math.max(0, (clientY-rect.top)/rect.height));
  return {nx, ny};
}

function onPointer(e){
  const p = e.touches && e.touches[0] ? e.touches[0] : e;
  const {nx, ny} = toNorm(p.clientX, p.clientY);
  sendPos(nx, ny);
}

pad.addEventListener('pointerdown', onPointer);
pad.addEventListener('pointermove', onPointer);
pad.addEventListener('touchstart', onPointer, {passive:true});
pad.addEventListener('touchmove', onPointer, {passive:true});

function bind(btn, mode){
  const send = ()=> socket.emit('modeChange', mode);
  btn.addEventListener('pointerdown', e=>{ e.preventDefault(); send(); });
  btn.addEventListener('click', send);
  btn.addEventListener('touchstart', e=>{ e.preventDefault(); send(); }, {passive:false});
}
bind(document.getElementById('m1'), 1);
bind(document.getElementById('m2'), 2);
bind(document.getElementById('m3'), 3);
```
``` html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="utf-8"/>
  <meta name="viewport" content="width=device-width, initial-scale=1"/>
  <script src="https://cdn.jsdelivr.net/npm/p5@1.11.0/lib/p5.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/p5@1.11.0/lib/addons/p5.sound.min.js"></script>
  <script src="/socket.io/socket.io.js"></script>
  <style>html,body{margin:0;background:#0b0f12}</style>
</head>
<body>
  <main></main>
  <script src="sketch.js"></script>
</body>
</html>
```
``` html
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="utf-8"/><meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=no"/>
<script src="/socket.io/socket.io.js"></script>
<style>
  html,body{margin:0;height:100%;background:#0b0f12;color:#e7ecef;font-family:system-ui}
  .wrap{display:flex;flex-direction:column;gap:16px;align-items:center;justify-content:center;height:100%}
  .row{display:flex;gap:12px}
  button{padding:14px 20px;border-radius:12px;border:0;background:#1a2430;color:#e7ecef;font-size:18px}
  .conn{opacity:.85}
</style>
</head>
<body>
  <div class="wrap">
    <div class="row">
      <button id="m1">Modo 1</button>
      <button id="m2">Modo 2</button>
      <button id="m3">Modo 3</button>
    </div>
    <div class="conn" id="conn">conectando…</div>
  </div>
  <script>
    const sock = io();
    const connEl = document.getElementById('conn');
    sock.on('connect', ()=> connEl.textContent = 'conectado · '+sock.id);
    sock.on('connect_error', e=> connEl.textContent = 'sin conexion · '+(e.message||'error'));
    const send = m => sock.emit('modeChange', m);
    document.getElementById('m1').addEventListener('click', ()=>send(1));
    document.getElementById('m2').addEventListener('click', ()=>send(2));
    document.getElementById('m3').addEventListener('click', ()=>send(3));
  </script>
</body>
</html>
```


# Autoevaluacion 

1: [evidencias](#actividad1)
2:[evidencias](#actividad2)
3:[evidencias](#actividad3)
4:[evidencias](#actividad4)
5:[evidencias](#actividad5)

nota: 4













