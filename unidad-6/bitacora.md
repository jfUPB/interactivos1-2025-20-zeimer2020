
# Evidencias de la unidad 6

<a name = "actividad1"> <a\>

# actividad 1

#### ¿Qué ocurrió en la terminal cuando ejecutaste npm install? ¿Cuál crees que es su propósito?
 nodejs-test-1@1.0.0 start
> node server.js

Server is listening on http://localhost:3000

creo que el proposito es primero permitirme ur a ver el servidor que acabo de crear y lo que se genera gracias al codigo de visual studio code y luego como registrar que esta haciendo el nodejs

#### ¿Qué mensaje específico apareció en la terminal después de ejecutar npm start? ¿Qué indica este mensaje?
 nodejs-test-1@1.0.0 start
> node server.js

Server is listening on http://localhost:3000
esto me muestra el lugar donde se activa y tambien que el node server esta creandolo


#### Describe lo que ves inicialmente en page1 y page2 en tu navegador.
dos esferas conectandose entre si con dos rayas negras que viajan entre las dos paginas

#### ¿Qué mensajes aparecieron en la terminal del servidor cuando abriste page1 y page2?
me avisa que un usuario se conecto a la pagina para tener registro de lo ocurrido



#### Describe qué sucede en ambas páginas del navegador cuando mueves una de las ventanas. ¿Cambia algo visualmente? ¿Qué mensajes aparecen (si los hay) en la consola del navegador (usualmente accesible con F12 -> Pestaña Consola) y en la terminal del servidor?

muestra el registro de "movimiento" de alguna manera, cada vez que se mueve se supone que se vuelve a dibujar la figura para seguir a la otra pagina o hacer la ilusion de eso, en la terminal ya se muestra como el registro de cada re dibujada

<a name = "actividad2"> <a\>
# Actividad 2


### ¿Puedes identificar otros ejemplos de relaciones Cliente-Servidor en tu vida diaria (no necesariamente digitales)? Por ejemplo, al pedir comida en un restaurante. ¿Quién es el cliente y quién el servidor? ¿Qué se pide y qué se entrega?

por ejemplo los cines, el cliente seria la sala el servidor podria ser el cuartico donde esta el reproductor ademas de que podria ser la registradora

### Toma la URL de tu sitio web favorito. Intenta identificar el protocolo, el nombre de dominio y la ruta (si la hay). ¿Qué crees que pasa si solo escribes el nombre de dominio (ej. www.google.com) sin una ruta específica? ¿Qué “página por defecto” crees que te envía el servidor?

url: https://www.youtube.com/?app=desktop&hl=es

protocolo: youtube usea https 

dominio: youtube.com

lo que pasa si solo se coloca el dmoninion sin ruta es que de todas formas sigue funcionando

¿Qué parte crees que es HTML (ej. los campos de texto, el botón)?

Campos de texto para correo y contraseña
Boton de siguiente
Enlaces como "Olvidaste tu correo" o "Crear cuenta"
Logo de Google

¿Qué parte es CSS (ej. el color del botón, el tipo de letra)?

Color azul del boton
Tipo y tamaño de letra
Espacios en blanco y centrado del formulario
Bordes redondeados de los campos

¿Qué parte es JavaScript (ej. la comprobación de si escribiste algo antes de enviar, el mensaje de “contraseña incorrecta” que aparece sin recargar la página)?

Validar si los campos estan vacios
Mostrar mensajes de error inmediatos
Avisar "contraseña incorrecta" sin recargar la pagina
Redirigir al siguiente paso despues de validar

Compara HTTP con los protocolos seriales que usaste.

¿Por qué crees que HTTP necesita ser más complejo que un simple envío de bytes como hacías con el micro:bit?

HTML: es la parte que arma la estructura, o sea los campos de texto para usuario y contraseña y el boton de login.

CSS: es lo que le da estilo, por ejemplo el color del boton, la fuente del texto y la alineacion de todo.

JavaScript: es lo que pone la logica, como revisar si escribiste algo antes de enviar o mostrar el mensajito de “contraseña incorrecta” sin tener que recargar la pagina.

<a name = "actividad3"> <a\>
# Actividad 3
experimentos

experimento 1
<img width="1360" height="365" alt="image" src="https://github.com/user-attachments/assets/55a23c5e-ca5b-403f-8286-7e367ac2cd34" />

en efecto funciona, esto lo que me dice es que mientras tenga una ruta de acceso sin importar cual sea el nombre, se puede montar e inicializar el servidor, lo importante es modificar el codigo, tener una ruta y mantener la estructura correctamente, pero mientras tenga nomnbre es posible, ahora, el page1 no funciona mientras el page_uno funcione ya que lo modifique

Experimento 2

El id se mantuvo el mismo hasta que cerre la pagina, mientras tenia iniciada ambas paginas salia este ID

PDto_dy1JOX-tstCAAAB 
constantemente, pero cuando cerre, se cambio a este ID
nkQJcyjxsPeXKowUAAAD

Experimento 3

si muevo tanto la una como la otra pagina 
me muestra esto 

All clients are fully synced
Received win2update from ID: PDto_dy1JOX-tstCAAAB Data: { x: 1051, y: 155, width: 1491, height: 704 }
Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 2
All clients are fully synced
Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 2
All clients are fully synced
Received win2update from ID: PDto_dy1JOX-tstCAAAB Data: { x: 1052, y: 155, width: 1491, height: 704 }
Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 2
All clients are fully synced
Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 2
All clients are fully synced
Received win2update from ID: PDto_dy1JOX-tstCAAAB Data: { x: 1053, y: 155, width: 1491, height: 704 }

luego, cuando hacemos el cambio del experimento clave 

al hacer el cambio del socket.broadcast.emit a socket.emit se desconecata una de las paginas, sin embargo la otra sigue tratando de conectarse pq no sabe que la otra dejo de intentar
<img width="506" height="414" alt="image" src="https://github.com/user-attachments/assets/3ed8a295-ac65-4b3a-9035-738dca16b402" />
<img width="517" height="476" alt="image" src="https://github.com/user-attachments/assets/c9fe3e10-fa3e-4ff2-a75f-dd5af89c2417" />

Experimento 4

pues claramente como era de esperar ahora cuando cambiamos el port a 3001, el port de 3000 deja de funcionar pq no lo estamos enviando ahi, sin embargo el port 3001 comienza a funcionar, si no estamos enviando datos a un puerto, cuando vayamos alla naturalmente no vamos a recibir nada
<img width="930" height="460" alt="image" src="https://github.com/user-attachments/assets/6901ae4b-fecc-48d4-9bc4-5aa34919804f" />

<a name = "actividad4"> <a\>

# Actividad 4 

experimento 1

Refresca la página page2.html. Observa la consola del navegador. ¿Ves algún error relacionado con la conexión? ¿Qué indica?
<img width="775" height="233" alt="image" src="https://github.com/user-attachments/assets/92e1786f-db8d-42ff-ab7a-907a1bc29c82" />

esto nos dice que la conexion fue negada

despues de refrescar los errores desaparecen pero queda una historial 
<img width="809" height="408" alt="image" src="https://github.com/user-attachments/assets/cf20d66d-7c0f-4c78-8562-51ba3b0411c2" />

experimento 2

<img width="561" height="339" alt="image" src="https://github.com/user-attachments/assets/f607de53-87c7-42e8-b4ea-1f8acec42ee4" />
<img width="509" height="460" alt="image" src="https://github.com/user-attachments/assets/238fa0a0-6ee1-4dfe-9bfe-19e85e5facf9" />

lo que pasa es que se desconecto esta parte del metodo, es como si ya no se actualizara correctamente y por eso ocurre esto

experimento 3

esto es lo que registre con los cambios realizados, primero pasa lo de que cambia de oscuro a claro a medida que se acerca o se aleja y tambien gana o pierde grosor, de paso tambien desaparece el de page 2 
<img width="1764" height="565" alt="image" src="https://github.com/user-attachments/assets/d291ef0f-10e6-4c6f-86b5-f3d4fea19399" />
<img width="763" height="382" alt="image" src="https://github.com/user-attachments/assets/5d2e3c59-cef8-461f-b094-0a1e6add5f25" />


<a name = "actividad5"> <a\>
# Actividad 5 apply


lo que hice fue colocar una pelotica azul compartida en ambas paginas, cuando uno da clickla pelotica azul se movera con mayor velocidad, y si se juntan las page una sobre otra la pelota azul estara como una sola
<img width="1095" height="660" alt="image" src="https://github.com/user-attachments/assets/facc152b-3fb3-4eb2-a40d-8a84048e0490" />

<img width="726" height="328" alt="image" src="https://github.com/user-attachments/assets/f3980803-7fc7-4fa8-bfe2-8d25621bf321" />

```js
const express = require('express');
const http = require('http');
const socketIO = require('socket.io');
const path = require('path');
const app = express();
const server = http.createServer(app); 
const io = socketIO(server); 
const port = 3000;

let page1 = { x: 0, y: 0, width: 100, height: 100 };
let page2 = { x: 0, y: 0, width: 100, height: 100 };
let connectedClients = new Map();
let syncedClients = new Set();

app.use(express.static(path.join(__dirname, 'views')));

app.get('/page1', (req, res) => {
    res.sendFile(path.join(__dirname, 'views', 'page1.html'));
});

app.get('/page2', (req, res) => {
    res.sendFile(path.join(__dirname, 'views', 'page2.html'));
});

io.on('connection', (socket) => {
    console.log('A user connected - ID:', socket.id);
    connectedClients.set(socket.id, { page: null, synced: false });
    
    socket.on('disconnect', () => {
        console.log('User disconnected - ID:', socket.id);
        connectedClients.delete(socket.id);
        syncedClients.delete(socket.id);
        // Notificar a otros clientes que se perdió la sincronización
        socket.broadcast.emit('peerDisconnected');
    });

    socket.on('win1update', (window1, sendid) => {
        console.log('Received win1update from ID:', socket.id, 'Data:', window1);
        if (isValidWindowData(window1)) {
            page1 = window1;
            connectedClients.set(socket.id, { page: 'page1', synced: false });
            socket.broadcast.emit('getdata', { data: page1, from: 'page1' });
            checkAndNotifySyncStatus();
        }
    });

    socket.on('win2update', (window2, sendid) => {
        console.log('Received win2update from ID:', socket.id, 'Data:', window2);
        if (isValidWindowData(window2)) {
            page2 = window2;
            connectedClients.set(socket.id, { page: 'page2', synced: false });
            socket.broadcast.emit('getdata', { data: page2, from: 'page2' });
            checkAndNotifySyncStatus();
        }
    });

    socket.on('requestSync', () => {
        const clientInfo = connectedClients.get(socket.id);
        if (clientInfo?.page === 'page1') {
            socket.emit('getdata', { data: page2, from: 'page2' });
        } else if (clientInfo?.page === 'page2') {
            socket.emit('getdata', { data: page1, from: 'page1' });
        }
    });

    socket.on('confirmSync', () => {
        syncedClients.add(socket.id);
        const clientInfo = connectedClients.get(socket.id);
        if (clientInfo) {
            connectedClients.set(socket.id, { ...clientInfo, synced: true });
        }
        checkAndNotifySyncStatus();
    });    

    socket.on('cometNudge', (impulse) => {
        if (impulse && typeof impulse.ix === 'number' && typeof impulse.iy === 'number') {
            comet.vx += clamp(impulse.ix, -1, 1);
            comet.vy += clamp(impulse.iy, -1, 1);
        }
    });
});

function isValidWindowData(data) {
    return data && 
           typeof data.x === 'number' && 
           typeof data.y === 'number' && 
           typeof data.width === 'number' && data.width > 0 &&
           typeof data.height === 'number' && data.height > 0;
}

function checkAndNotifySyncStatus() {
    const page1Clients = Array.from(connectedClients.entries()).filter(([id, info]) => info.page === 'page1');
    const page2Clients = Array.from(connectedClients.entries()).filter(([id, info]) => info.page === 'page2');
    
    const bothPagesConnected = page1Clients.length > 0 && page2Clients.length > 0;
    const allClientsSynced = Array.from(connectedClients.keys()).every(id => syncedClients.has(id));
    const hasMinimumClients = connectedClients.size >= 2;

    console.log(`Debug - Connected clients: ${connectedClients.size}, Page1: ${page1Clients.length}, Page2: ${page2Clients.length}, Synced: ${syncedClients.size}`);

    if (bothPagesConnected && allClientsSynced && hasMinimumClients) {
        io.emit('fullySynced', true);
        console.log('All clients are fully synced');
    } else {
        io.emit('fullySynced', false);
        console.log(`Sync status: pages=${bothPagesConnected}, synced=${allClientsSynced}, clients=${connectedClients.size}`);
    }
}

let comet = { x: 0.5, y: 0.5, vx: 0.25, vy: -0.18 };
const COMET_DAMPING = 0.999;
const TICK_MS = 16;

setInterval(() => {
    const dt = TICK_MS / 1000;
    comet.x += comet.vx * dt;
    comet.y += comet.vy * dt;

    if (comet.x < 0) { comet.x = 0; comet.vx *= -1; }
    if (comet.x > 1) { comet.x = 1; comet.vx *= -1; }
    if (comet.y < 0) { comet.y = 0; comet.vy *= -1; }
    if (comet.y > 1) { comet.y = 1; comet.vy *= -1; }

    comet.vx *= COMET_DAMPING;
    comet.vy *= COMET_DAMPING;

    io.emit('cometTick', comet);
}, TICK_MS);

function clamp(v, a, b) { return Math.max(a, Math.min(b, v)); }

server.listen(port, () => {
    console.log(`Server is listening on http://localhost:${port}`);
});
```

```js

let currentPageData = {
    x: window.screenX,
    y: window.screenY,
    width: window.innerWidth,
    height: window.innerHeight
}

let previousPageData = {
    x: window.screenX,
    y: window.screenY,
    width: window.innerWidth,
    height: window.innerHeight
};

let remotePageData = { x: 0, y: 0, width: 100, height: 100 };
let point1 = [currentPageData.width / 2, currentPageData.height / 2];
let socket;
let isConnected = false;
let hasRemoteData = false;
let isFullySynced = false;
let connectionTimeout;

function setup() {
    createCanvas(windowWidth, windowHeight);
    frameRate(60);
    socket = io();

    socket.on('connect', () => {
        console.log('Connected with ID:', socket.id);
        isConnected = true;
        socket.emit('win1update', currentPageData, socket.id);
        
        setTimeout(() => {
            socket.emit('requestSync');
        }, 500);
    });

    socket.on('getdata', (response) => {
        if (response && response.data && isValidRemoteData(response.data)) {
            remotePageData = response.data;
            hasRemoteData = true;
            console.log('Received valid remote data:', remotePageData);
            socket.emit('confirmSync');
        }
    });

    socket.on('fullySynced', (synced) => {
        isFullySynced = synced;
        console.log('Sync status:', synced ? 'SYNCED' : 'NOT SYNCED');
    });

    socket.on('peerDisconnected', () => {
        hasRemoteData = false;
        isFullySynced = false;
        console.log('Peer disconnected, waiting for reconnection...');
    });

    socket.on('disconnect', () => {
        isConnected = false;
        hasRemoteData = false;
        isFullySynced = false;
        console.log('Disconnected from server');
    });

    socket.on('cometTick', (c) => {
        if (c && isFinite(c.x) && isFinite(c.y)) {
            cometNorm.x = constrain(c.x, 0, 1);
            cometNorm.y = constrain(c.y, 0, 1);
        }
    });
}

function isValidRemoteData(data) {
    return data && 
           typeof data.x === 'number' && 
           typeof data.y === 'number' && 
           typeof data.width === 'number' && data.width > 0 &&
           typeof data.height === 'number' && data.height > 0;
}

function checkWindowPosition() {
    currentPageData = {
        x: window.screenX,
        y: window.screenY,
        width: window.innerWidth,
        height: window.innerHeight
    };

    if (currentPageData.x !== previousPageData.x || currentPageData.y !== previousPageData.y || 
        currentPageData.width !== previousPageData.width || currentPageData.height !== previousPageData.height) {

        point1 = [currentPageData.width / 2, currentPageData.height / 2]
        socket.emit('win1update', currentPageData, socket.id);
        previousPageData = currentPageData;
    }
}

function draw() {
    background(220);
    
    if (!isConnected) {
        showStatus('Conectando al servidor...', color(255, 165, 0));
        return;
    }
    
    if (!hasRemoteData) {
        showStatus('Esperando conexión de la otra ventana...', color(255, 165, 0));
        return;
    }
    
    if (!isFullySynced) {
        showStatus('Sincronizando datos...', color(255, 165, 0));
        return;
    }

    drawCircle(point1[0], point1[1]);
    checkWindowPosition();
    
    let vector1 = createVector(currentPageData.x, currentPageData.y);
    let vector2 = createVector(remotePageData.x, remotePageData.y);
    let resultingVector = createVector(vector2.x - vector1.x, vector2.y - vector1.y);
    
    stroke(50);
    strokeWeight(20);
    drawCircle(resultingVector.x + remotePageData.width / 2, resultingVector.y + remotePageData.height / 2);
    line(point1[0], point1[1], resultingVector.x + remotePageData.width / 2, resultingVector.y + remotePageData.height / 2);

    renderComet();
}

function showStatus(message, statusColor) {
    textSize(24);
    textAlign(CENTER, CENTER);
    noStroke();
    fill(0, 0, 0, 150); // Negro semi-transparente
    rectMode(CENTER);
    let textW = textWidth(message) + 40;
    let textH = 40;
    rect(width / 2, 1*height / 6, textW, textH, 10);
    fill(statusColor);
    text(message, width / 2, 1*height / 6);
}

function drawCircle(x, y) {
    fill(255, 0, 0);
    ellipse(x, y, 150, 150);
}

function windowResized() {
    resizeCanvas(windowWidth, windowHeight);
}

let cometNorm = { x: 0.5, y: 0.5 };

function renderComet() {
    const cx = cometNorm.x * width;
    const cy = cometNorm.y * height;
    noStroke();
    fill(0, 120, 255);
    ellipse(cx, cy, 24, 24);
}

function mousePressed() {
    if (!isFullySynced) return;
    const dx = (mouseX - width / 2) / width;
    const dy = (mouseY - height / 2) / height;
    const scale = 0.6;
    socket.emit('cometNudge', { ix: dx * scale, iy: dy * scale });
}
```

```js
let currentPageData = {
    x: window.screenX,
    y: window.screenY,
    width: window.innerWidth,
    height: window.innerHeight

}

let previousPageData = {
    x: window.screenX,
    y: window.screenY,
    width: window.innerWidth,
    height: window.innerHeight
};

let remotePageData = { x: 0, y: 0, width: 100, height: 100 };
let point2 = [currentPageData.width / 2, currentPageData.height / 2];
let socket;
let isConnected = false;
let hasRemoteData = false;
let isFullySynced = false;
let connectionTimeout;

function setup() {
    createCanvas(windowWidth, windowHeight);
    frameRate(60);
    socket = io();

    socket.on('connect', () => {
        console.log('Connected with ID:', socket.id);
        isConnected = true;
        socket.emit('win2update', currentPageData, socket.id);
        
        setTimeout(() => {
            socket.emit('requestSync');
        }, 500);
    });

    socket.on('getdata', (response) => {
        if (response && response.data && isValidRemoteData(response.data)) {
            remotePageData = response.data;
            hasRemoteData = true;
            console.log('Received valid remote data:', remotePageData);
            socket.emit('confirmSync');
        }
    });

    socket.on('fullySynced', (synced) => {
        isFullySynced = synced;
        console.log('Sync status:', synced ? 'SYNCED' : 'NOT SYNCED');
    });

    socket.on('peerDisconnected', () => {
        hasRemoteData = false;
        isFullySynced = false;
        console.log('Peer disconnected, waiting for reconnection...');
    });

    socket.on('disconnect', () => {
        isConnected = false;
        hasRemoteData = false;
        isFullySynced = false;
        console.log('Disconnected from server');
    });

    socket.on('cometTick', (c) => {
        if (c && isFinite(c.x) && isFinite(c.y)) {
            cometNorm.x = constrain(c.x, 0, 1);
            cometNorm.y = constrain(c.y, 0, 1);
        }
    });
}

function isValidRemoteData(data) {
    return data && 
           typeof data.x === 'number' && 
           typeof data.y === 'number' && 
           typeof data.width === 'number' && data.width > 0 &&
           typeof data.height === 'number' && data.height > 0;
}

function checkWindowPosition() {
    currentPageData = {
        x: window.screenX,
        y: window.screenY,
        width: window.innerWidth,
        height: window.innerHeight
    };

    if (currentPageData.x !== previousPageData.x || currentPageData.y !== previousPageData.y || 
        currentPageData.width !== previousPageData.width || currentPageData.height !== previousPageData.height) {

        point2 = [currentPageData.width / 2, currentPageData.height / 2]
        socket.emit('win2update', currentPageData, socket.id);
        previousPageData = currentPageData; 
    }
}

function draw() {
    background(220);
    
    if (!isConnected) {
        showStatus('Conectando al servidor...', color(255, 165, 0));
        return;
    }
    
    if (!hasRemoteData) {
        showStatus('Esperando conexión de la otra ventana...', color(255, 165, 0));
        return;
    }
    
    if (!isFullySynced) {
        showStatus('Sincronizando datos...', color(255, 165, 0));
        return;
    }

    drawCircle(point2[0], point2[1]);
    checkWindowPosition();
    
    let vector2 = createVector(remotePageData.x, remotePageData.y);
    let vector1 = createVector(currentPageData.x, currentPageData.y);
    let resultingVector = createVector(vector2.x - vector1.x, vector2.y - vector1.y);
    
    stroke(50);
    strokeWeight(20);
    drawCircle(resultingVector.x + remotePageData.width / 2, resultingVector.y + remotePageData.height / 2);
    line(point2[0], point2[1], resultingVector.x + remotePageData.width / 2, resultingVector.y + remotePageData.height / 2);

    renderComet();
}

function showStatus(message, statusColor) {
    textSize(24);
    textAlign(CENTER, CENTER);
    noStroke();
    fill(0, 0, 0, 150); // Negro semi-transparente
    rectMode(CENTER);
    let textW = textWidth(message) + 40;
    let textH = 40;
    rect(width / 2, 1*height / 6, textW, textH, 10);
    fill(statusColor);
    text(message, width / 2, 1*height / 6);
}

function drawCircle(x, y) {
    fill(255, 0, 0);
    ellipse(x, y, 150, 150);
}

function windowResized() {
    resizeCanvas(windowWidth, windowHeight);
}

let cometNorm = { x: 0.5, y: 0.5 };

function renderComet() {
    const cx = cometNorm.x * width;
    const cy = cometNorm.y * height;
    noStroke();
    fill(0, 120, 255);
    ellipse(cx, cy, 24, 24);
}

function mousePressed() {
    if (!isFullySynced) return;
    const dx = (mouseX - width / 2) / width;
    const dy = (mouseY - height / 2) / height;
    const scale = 0.6;
    socket.emit('cometNudge', { ix: dx * scale, iy: dy * scale });
}
```

Autoevaluacion

mi nota es 5

ya que realice todas las actividades de esta unidad

actividad 1
[evidencia](#actividad1)
actividad 2
[evidencia](#actividad2)
actividad 3
[evidencia](#actividad3)
actividad 4
[evidencia](#actividad4)
actividad 5
[evidencia](#actividad5)











