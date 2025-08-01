# Unidad 2

## 🔎 Fase: Set + Seek

### Actividad 1 

```  python
from microbit import *
import utime

class Pixel:
    def __init__(self,pixelX,pixelY,initState,interval):
        self.state = "Init"
        self.startTime = 0
        self.interval = interval
        self.pixelX = pixelX
        self.pixelY = pixelY
        self.pixelState = initState

    def update(self):

        if self.state == "Init":
            self.startTime = utime.ticks_ms()
            self.state = "WaitTimeout"
            display.set_pixel(self.pixelX,self.pixelY,self.pixelState)

        elif self.state == "WaitTimeout":
            if utime.ticks_diff(utime.ticks_ms(),self.startTime) > self.interval:
                self.startTime = utime.ticks_ms()
                if self.pixelState == 9:
                    self.pixelState = 0
                else:
                    self.pixelState = 9
                display.set_pixel(self.pixelX,self.pixelY,self.pixelState)

pixel1 = Pixel(0,0,0,1000)
pixel2 = Pixel(4,4,0,500)

while True:
    pixel1.update()
    pixel2.update()

```

Describe detalladamente cómo funciona este ejemplo.

Este programa hace que dos pixeles de la micro:bit parpadeen de forma independiente usando tiempo y una maquina de estados. Cada pixel tiene una posicion, un estado (encendido o apagado) y un intervalo que indica cada cuanto debe cambiar

¿Cuáles son los estados en el programa?

 Al comenzar, cada pixel se inicializa y se enciende, luego entra en un estado de espera donde revisa si ya paso el tiempo necesario. Si es asi, cambia su brillo y reinicia el conteo del tiempo

¿Cuáles son los eventos/inputs en el programa?

Solo hay un evento: el paso del tiempo. No hay entradas como botones o sensores. Las acciones que realiza el programa son prender o apagar el pixel, cambiar su brillo y actualizar el tiempo

¿Cuáles son las acciones en el programa?

El uso de estados y temporizadores permite que los pixeles funcionen al mismo tiempo sin usar pausas que bloqueen el programa, lo que lo hace eficiente y facil de ampliar.


### Actividad 2

Escribe el código que soluciona este problema en tu bitácora.
Identifica los estados, eventos y acciones en tu código.


``` python
# Imports go at the top
from microbit import *

estado = "rojo"

# Code in a 'while True:' loop repeats forever
while True:
     if estado == "rojo":
        display.clear()
        display.set_pixel(2, 0, 9)
        sleep(3000)
        estado = "verde"
     elif estado == "verde":
        display.clear()
        display.set_pixel(2, 2, 9)
        sleep(3000)
        estado = "amarillo" 
     elif estado == "amarillo":  
        display.clear()
        display.set_pixel(2, 4, 9)
        sleep(1000)
        estado = "rojo"
```

Los estados presentes en este caso serian amarillo rojo y verde, el unico evento que maneja es el sleep pa que duerman los leds y cambien entre colores, luego ya las acciones serian limpiar la pantalla, encender un pixel, esperar x tiempo antes de hacer la ultima accion que seria cambiar de estado

### Activiada 3


``` python
from microbit import *
import utime

STATE_INIT = 0
STATE_HAPPY = 1
STATE_SMILE = 2
STATE_SAD = 3

HAPPY_INTERVAL = 1500
SMILE_INTERVAL = 1000
SAD_INTERVAL = 2000

current_state = STATE_INIT
start_time = 0
interval = 0

while True:
    # pseudoestado STATE_INIT
    if current_state == STATE_INIT:
        display.show(Image.HAPPY)
        start_time = utime.ticks_ms()
        interval = HAPPY_INTERVAL
        current_state = STATE_HAPPY
    elif current_state == STATE_HAPPY:
        if button_a.was_pressed():
            # Acciones para el evento
            display.show(Image.SAD)
            # Acciones de entrada para el siguiente estado
            start_time = utime.ticks_ms()
            interval = SAD_INTERVAL
            current_state = STATE_SAD
        if utime.ticks_diff(utime.ticks_ms(), start_time) > interval:
            # Acciones para el evento
            display.show(Image.SMILE)
            # Acciones de entrada para el siguiente estado
            start_time = utime.ticks_ms()
            interval = SMILE_INTERVAL
            current_state = STATE_SMILE
    elif current_state == STATE_SMILE:
        if button_a.was_pressed():
            display.show(Image.HAPPY)
            start_time = utime.ticks_ms()
            interval = HAPPY_INTERVAL
            current_state = STATE_HAPPY
        if utime.ticks_diff(utime.ticks_ms(), start_time) > interval:
            display.show(Image.SAD)
            start_time = utime.ticks_ms()
            interval = SAD_INTERVAL
           current_state = STATE_SAD
    elif current_state == STATE_SAD:
        if button_a.was_pressed():
            display.show(Image.SMILE)
            start_time = utime.ticks_ms()
            interval = SMILE_INTERVAL
            current_state = STATE_SMILE
        if utime.ticks_diff(utime.ticks_ms(), start_time) > interval:
            display.show(Image.HAPPY)
            start_time = utime.ticks_ms()
            interval = HAPPY_INTERVAL
            current_state = STATE_HAPPY
```

Explica por qué decimos que este programa permite realizar de manera concurrente varias tareas.

el programa simula tareas concurrentes al manejar tiempo y eventos sin detenerse, permitiendo respuestas simultaneas


Identifica los estados, eventos y acciones en el programa


los estados son init, happy, smile, sad. Los eventos son boton a y paso del tiempo. Las ccciones son mostrar imagen y cambiar estado.


Describe y aplica al menos 3 vectores de prueba para el programa. Para definir un vector de prueba debes llevar al sistema a un estado, generar los eventos
y observar el estado siguiente y las acciones que ocurrirán. Por tanto, un vector de prueba tiene unas condiciones iniciales del sistema, unos resultados
esperados y los resultados realmente obtenidos. Si el resultado obtenido es igual al esperado entonces el sistema pasó el vector de prueba, de lo contrario
el sistema puede tener un error.

el vector 1 init muestra happy y pasa a happy, pasa la prueba. el vector 2 en happy presionar a muestra sad y pasa a sad, pasa la prueba. vector 3: en smile sin presionar pasa el tiempo, muestra sad y cambia a sad y pasa la prueba








