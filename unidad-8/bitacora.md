
# Evidencias de la unidad 8



### Documenta los referentes visuales que te inspiren.

<img width="584" height="221" alt="image" src="https://github.com/user-attachments/assets/e5018d84-156d-4db0-b49c-0d99cdb91700" />

### Define el concepto de las visuales que quieres crear.

Electrocardiograma vibrando al ritmo de la musica

### Explica cómo el móvil y el micro:bit controlarán las visuales.

Pues el funcionamiento de el microbit seria el mismo que el del ceular, simplemente el boton A pondria modo 1, el boton b pondria modo 2 y el shake pondria modo 3

# Apply

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

``` js
(() => {
  let port, reader, keepReading = false;

  function setMode(n){
    try{
      if (typeof socketRef !== 'undefined' && socketRef && socketRef.emit) {
        socketRef.emit('modeChange', n);
      }
      if (typeof modeSel !== 'undefined') modeSel = n;
      if (typeof modeText !== 'undefined') modeText = 'MODO ' + n;
      if (typeof modeFlash !== 'undefined') modeFlash = 1;
      updatePanel('modo', 'MODO ' + n);
    }catch(e){}
  }

  function mkButton(){
    const btn = document.createElement('button');
    btn.id = 'btn-microbit-serial';
    btn.textContent = 'Conectar micro:bit';
    Object.assign(btn.style, { position:'fixed', right:'14px', top:'14px', zIndex:9999, padding:'10px 14px', borderRadius:'12px', border:'1px solid #ccc', background:'#ffffffaa', backdropFilter:'blur(6px)', cursor:'pointer', fontFamily:'system-ui,-apple-system,Segoe UI,Roboto,Arial', fontSize:'14px' });
    btn.addEventListener('click', connectSerial);
    document.body.appendChild(btn);
  }

  function mkPanel(){
    const box = document.createElement('div');
    box.id = 'mbit-panel';
    Object.assign(box.style, { position:'fixed', left:'14px', bottom:'14px', zIndex:9999, minWidth:'220px', padding:'10px 12px', borderRadius:'12px', border:'1px solid #223', background:'#0f1622cc', color:'#e7ecef', font:'12px system-ui' });
    box.innerHTML = '<div id="mbit-port">puerto: —</div><div id="mbit-last">ultimo: —</div><div id="mbit-modo">modo: —</div>';
    document.body.appendChild(box);
  }

  function updateBtn(label, disabled){
    const b = document.getElementById('btn-microbit-serial');
    if (!b) return;
    b.textContent = label;
    b.disabled = !!disabled;
    b.style.opacity = disabled ? '0.7' : '1';
  }

  function updatePanel(field, text){
    const ids = { port:'mbit-port', last:'mbit-last', modo:'mbit-modo' };
    const el = document.getElementById(ids[field]);
    if (el) el.textContent = (field==='port'?'puerto: ':(field==='last'?'ultimo: ':'modo: ')) + text;
  }

  async function connectSerial(){
    if (!('serial' in navigator)) { alert('Tu navegador no soporta Web Serial. Usa Chrome/Edge/Opera en localhost o HTTPS.'); return; }
    try{
      port = await navigator.serial.requestPort({ filters: [] });
      const info = port.getInfo ? port.getInfo() : {};
      console.log('serial port info:', info);
      updatePanel('port', JSON.stringify(info) || 'sin info');
      await port.open({ baudRate: 115200 });
      updateBtn('micro:bit conectado (USB)', true);
      keepReading = true;
      readLoop();
      navigator.serial.addEventListener('disconnect', (e) => {
        if (port && e.target === port) { stopReading(); updateBtn('Conectar micro:bit', false); updatePanel('port', 'desconectado'); }
      });
    }catch(err){
      console.error('No se pudo abrir el puerto serie:', err);
      alert('No se pudo conectar al micro:bit por USB. Cierra otros monitores y reintenta.');
    }
  }

  async function readLoop(){
    try{
      const textDecoder = new TextDecoderStream();
      const pipe = port.readable.pipeTo(textDecoder.writable);
      const textReader = textDecoder.readable.getReader();
      reader = textReader;
      let buffer = '';
      while (keepReading){
        const { value, done } = await reader.read();
        if (done) break;
        if (value){
          buffer += value;
          const lines = buffer.split(/\r?\n/);
          buffer = lines.pop() ?? '';
          for (const raw of lines){
            const line = raw.trim();
            if (!line) continue;
            console.log('[micro:bit]', line);
            updatePanel('last', line);
            handleLine(line);
          }
        }
      }
    }catch(err){
      console.error('Error leyendo del puerto serie:', err);
      stopReading();
      updateBtn('Conectar micro:bit', false);
    }
  }

  function stopReading(){
    keepReading = false;
    if (reader){ try{ reader.releaseLock(); }catch{} reader = null; }
    try{ port?.close(); }catch{}
    port = null;
  }

  function handleLine(line){
    const t = line.toUpperCase();
    if (t === 'A' || t === 'M1') { setMode(1); return; }
    if (t === 'B' || t === 'M2') { setMode(2); return; }
    if (t === 'S' || t === 'SHAKE' || t === 'M3') { setMode(3); return; }
  }

  window.addEventListener('DOMContentLoaded', () => { mkButton(); mkPanel(); });
})();
```

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


Autoevaluacion 

5 

aqui atras esta el codigo evidenciando que si lo hice, ademas tambien tengo lo que me inspiro mas arriba
cumpliendo todo lo de la bitacora









