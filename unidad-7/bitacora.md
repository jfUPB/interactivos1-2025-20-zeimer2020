
# Evidencias de la unidad 7

### ¿Qué URL de Dev Tunnels obtuviste? ¿Por qué crees que necesitamos usar esta URL en lugar de http://localhost:3000 o la IP local de tu computador para que el celular se conecte?

obvtuve dos, una fue https://n8xm1p1z-3000.use2.devtunnels.ms/mobile/ y la otra era la del loclahost pero habia que colocarle mobile a la del celular y desktop a la otra, entiendo que eran estas dos para que funcionara en cada dispositivo

### Describe brevemente qué hace npm install y npm start.

El npm install se encarga de instalar codigos y funciones del repositorio copiado desde el github en las carpetas designadas, el npm start inicializa los codigos y los servidores que indiquen los codigos y datos descargados del githuh

### ¿Qué mensajes observaste en la terminal del servidor al conectar el cliente de escritorio y el cliente móvil? ¿Eran diferentes los mensajes o identificadores?

 <img width="443" height="78" alt="image" src="https://github.com/user-attachments/assets/44fe80af-7884-42cb-804f-2be1c7d5cccc" />


### Describe el comportamiento observado: ¿Funcionó la interacción? ¿Hubo algún retraso (latencia)?
hubo retraso de latencia pero en mi caso, en los pcs de mis compañeros no tanto, seria por la lenta conexion me imagino

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


# Actividad 3

### ¿Cual es la funcion principal de express.static(‘public’) en este servidor? ¿Como se compara con el uso de app.get(‘/ruta’, …) del servidor de la Unidad 6?
Sirve para mostrar archivos sin rutas manuales, a diferencia de app.get que define rutas una por una

### Explica detalladamente el flujo de un mensaje tactil: ¿Que evento lo envia desde el movil? ¿Que evento lo recibe el servidor? ¿Que hace el servidor con el? ¿Que evento lo envia el servidor al escritorio? ¿Por que se usa socket.broadcast.emit en lugar de io.emit o socket.emit en este caso?
El movil envia con socket.emit, el servidor recibe con socket.on y reenvia con socket.broadcast.emit a los demas

### Si conectaras dos computadores de escritorio y un movil a este servidor, y movieras el dedo en el movil, ¿Quien recibiria el mensaje retransmitido por el servidor? ¿Por que?
Los dos escritorios, porque broadcast no envia al emisor

### ¿Que informacion util te proporcionan los mensajes console.log en el servidor durante la ejecucion?
Muestran conexiones, desconexiones y mensajes recibidos

# Actividad 4

#### Realiza un diagrama donde muestres el flujo completo de datos y eventos entre los tres componentes: móvil, servidor y escritorio. Puedes ilustrar con un ejemplo de coordenadas táctiles (x, y) y cómo viajan a través del sistema.

song = loadnSOund, esto en el prelouad, uas el instrumento de analizis fft, amplitude y el song.connect, en el drop (una funcion que se llamara en cada frame) se le dice al instrumento de analizis que la vaya analizando, a la cancion obviamente, 

# Actividad 5


