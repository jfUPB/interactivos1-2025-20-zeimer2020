# Unidad 2


## 🛠 Fase: Apply

### Actividad 4



### Actividad 5

``` python

# Imports go at the top
from microbit import *
import music
import utime

# Code in a 'while True:' loop repeats forever
# Estados
STATE_CONFIG = 0
STATE_ARMED = 1
STATE_EXPLODED = 2


current_state = STATE_CONFIG
current_time = 20  # se supone que esto es el tiempo y si no funciona me pego un tiro
countdown = 0
start_time = utime.ticks_ms()
last_tick = utime.ticks_ms()
# Code in a 'while True:' loop repeats forever
while True:
    now = utime.ticks_ms()
    if current_state == STATE_CONFIG:
        display.show(str(current_time))
        if button_a.was_pressed():
            if current_time < 60:
                 current_time += 1
        if button_b.was_pressed():
            if current_time > 10:
                current_time -= 1
        if accelerometer.was_gesture("shake"):
            countdown = current_time
            last_tick = now
            display.show(str(countdown))
            current_state = STATE_ARMED
    elif current_state == STATE_ARMED:
        if utime.ticks_diff(now, last_tick) >= 1000:
            countdown -= 1
            last_tick = now
            if countdown > 0:
                display.show(str(countdown))
            else:
                display.show(Image.SKULL)
                music.play(music.WEDDING)
                current_state = STATE_EXPLODED
    elif current_state == STATE_EXPLODED:
        if pin_logo.is_touched():
            current_time = 20
            current_state = STATE_CONFIG
            music.stop()
            display.clear()
        else:
            #
            if utime.ticks_diff(now, last_tick) >= 500:
                if display.get_pixel(2, 2) == 0:
                    display.show(Image.SKULL)
                else:
                    display.clear()
                last_tick = now
```

