# Unidad 3


## 🛠 Fase: Apply

#### Actividad 6 y 7

https://editor.p5js.org/zeimer2020/sketches/I2kb7N_Fg

``` Python
# Imports go at the top
from microbit import *

uart.init(baudrate=115200)
display.show(Image.HAPPY)
# Code in a 'while True:' loop repeats forever
while True:
    if button_a.was_pressed():
        uart.write("A\n")
    if button_b.was_pressed():
        uart.write("B\n")
    if button_a.is_pressed() and button_b.is_pressed():
        uart.write("S\n")
    if uart.any():
        msg = uart.readline()
        if msg:
            msg = msg.strip()
            if msg.isdigit():
                display.show(msg.decode())
            else:
                if msg == b"C":
                    display.show(Image.HAPPY)
                elif msg == b"E":
                    display.show(Image.SAD)
``` 

profe cuando se usa en el microbit no fui capaz de hacer que se viera el numero completo, solo da numeros del 0 al 9, entonces por ejemplo si es 23 solo muestra el 3 y no se pq, eso ya fue error mio desde el p5:js 

