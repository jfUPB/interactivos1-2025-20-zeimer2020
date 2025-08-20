# Unidad 3

## 🔎 Fase: Set + Seek

### Actividad 1

``` python
# Imports go at the top
from microbit import *
import utime

display.clear()

class Semaforo:
    def __init__(self,x,y,tr,ty,tg):
        self.x = x
        self.y = y
        self.tr = tr
        self.ty =ty
        self.tg = tg
        self.startTime = utime.ticks_ms()
        self.state = 'WaitInRed'
        display.set_pixel(self.x,self.y,9)

    def update(self):
        if self.state == 'WaitInRed':
            if utime.ticks_diff(utime.ticks_ms(),self.startTime) >= self.tr:
                display.set_pixel(self.x,self.y,0)
                display.set_pixel(self.x,self.y+1,9)
                self.startTime = utime.ticks_ms()
                self.state = 'WaitInYellow'

        elif self.state == 'WaitInYellow':
            if utime.ticks_diff(utime.ticks_ms(),self.startTime) >= self.ty:
                display.set_pixel(self.x,self.y+1,0)
                display.set_pixel(self.x,self.y+2,9)
                self.startTime = utime.ticks_ms()
                self.state = 'WaitInGreen'

        elif self.state == 'WaitInGreen':
            if utime.ticks_diff(utime.ticks_ms(),self.startTime) >= self.tg:
                display.set_pixel(self.x,self.y+2,0)
                display.set_pixel(self.x,self.y,9)
                self.startTime = utime.ticks_ms()
                self.state = 'WaitInRed'

semaforo1 = Semaforo(0,0,5000,2000,3000)
semaforo2 = Semaforo(1,0,3000,1000,2000)
semaforo3 = Semaforo(2,0,4000,3000,2000)

while True:
    semaforo1.update()
    semaforo2.update()
    semaforo3.update()
```

#### Qué ventajas tiene usar una clase (class) en este caso para representar un semáforo?

es mas facil de manejar y llamar a la accion a cada semaforo, que tener que colocar el codigo una y otra vez para cada caso distinto, simplemente se colocan ligeras variaciones para cuando se llama a los semaforos y asi podemos ver los 3 semaforos al mismo tiempo

#### Puedes ver cómo la técnica de programación con máquinas de estado y el uso de funciona no bloqueantes te permite que varios semáforos funcionen al mismo tiempo?

si, ya que en el microbit se logra ver como es todos los semaforos funciona al mismo tiempo a su propia forma

#### Actividad 5

``` python
# Imports go at the top
from microbit import *
import utime

display.clear()

class GestorEvento:
    def __init__(self):
        self.valor = 0

    def set_valor(self, nuevo):
        self.valor = nuevo

    def reset_valor(self):
        self.valor = 0

    def get_valor(self):
        return self.valor


class ControlSerial:
    def __init__(self):
        uart.init(baudrate=115200)

    def ejecutar(self):
        if uart.any():
            dato = uart.read(1)
            if dato:
                if dato[0] == ord('A'):
                    evento.set_valor('A')
                elif dato[0] == ord('B'):
                    evento.set_valor('B')
                elif dato[0] == ord('S'):
                    evento.set_valor('S')
                elif dato[0] == ord('T'):
                    evento.set_valor('T')


class ControlBotonera:
    def __init__(self):
        pass

    def ejecutar(self):
        if button_a.was_pressed():
            evento.set_valor('A')
        elif button_b.was_pressed():
            evento.set_valor('B')
        elif accelerometer.was_gesture('shake'):
            evento.set_valor('S')
        elif pin_logo.is_touched():
            evento.set_valor('T')


class ControlBomba:
    def __init__(self):
        self.CLAVE = ['B', 'A', 'B']
        self.intentos = [''] * len(self.CLAVE)
        self.posClave = 0
        self.tiempo = 20
        self.inicio = utime.ticks_ms()
        self.estado = 'CONFIG'
        display.clear()
        display.show(self.tiempo, wait=False)

    def ejecutar(self):
        if self.estado == 'CONFIG':
            if evento.get_valor() == 'A':
                evento.reset_valor()
                self.tiempo = min(self.tiempo + 1, 60)
                display.show(self.tiempo, wait=False)

            if evento.get_valor() == 'B':
                evento.reset_valor()
                self.tiempo = max(10, self.tiempo - 1)
                display.show(self.tiempo, wait=False)

            if evento.get_valor() == 'S':
                evento.reset_valor()
                self.inicio = utime.ticks_ms()
                self.estado = 'ARMADA'

        elif self.estado == 'ARMADA':
            if utime.ticks_diff(utime.ticks_ms(), self.inicio) > 1000:
                self.inicio = utime.ticks_ms()
                self.tiempo -= 1
                display.show(self.tiempo, wait=False)
                if self.tiempo == 0:
                    display.show(Image.SKULL)
                    self.estado = 'EXPLOTO'

            if evento.get_valor() == 'A':
                evento.reset_valor()
                self.intentos[self.posClave] = 'A'
                self.posClave += 1

            if evento.get_valor() == 'B':
                evento.reset_valor()
                self.intentos[self.posClave] = 'B'
                self.posClave += 1

            if self.posClave == len(self.intentos):
                correcta = True
                for i in range(len(self.intentos)):
                    if self.intentos[i] != self.CLAVE[i]:
                        correcta = False
                        break
                if correcta:
                    self.tiempo = 20
                    display.show(self.tiempo, wait=False)
                    self.posClave = 0
                    self.estado = 'CONFIG'
                else:
                    self.posClave = 0

        elif self.estado == 'EXPLOTO':
            if evento.get_valor() == 'T':
                evento.reset_valor()
                self.tiempo = 20
                display.show(self.tiempo, wait=False)
                self.inicio = utime.ticks_ms()
                self.estado = 'CONFIG'


evento = GestorEvento()
serial_ctrl = ControlSerial()
botonera_ctrl = ControlBotonera()
bomba_ctrl = ControlBomba()

while True:
    serial_ctrl.ejecutar()
    botonera_ctrl.ejecutar()
    bomba_ctrl.ejecutar()
```


Vectores de prueba tabla y diagrama

<img width="546" height="653" alt="image" src="https://github.com/user-attachments/assets/18520bbd-c9f8-46a6-98c3-4bd2c14895cd" />


<img width="826" height="380" alt="image" src="https://github.com/user-attachments/assets/589f5945-3d9a-4782-ad07-2b255302649b" />












