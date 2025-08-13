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


### Actividad 2



