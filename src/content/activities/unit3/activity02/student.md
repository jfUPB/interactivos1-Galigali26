```
from microbit import *
import utime
import music

CONFIG = 0
ARMED = 1
EXPLODED = 2

estado = CONFIG
countdown_time = 20
last_tick = utime.ticks_ms()

secuencia_correcta = ['A', 'B', 'A', 'SHAKE']
secuencia_ingresada = []

def explosion_galaga():
    music.set_tempo(bpm=300)
    music.play([
        'g5:1', 'e5:1', 'c5:1', 'g4:1',
        'e4:2', 'c4:2', 'r:1',
        'g3:3', 'e3:2', 'c3:3', 'r:1'
    ])

def verificar_secuencia():
    return secuencia_ingresada == secuencia_correcta
    

while True:
    if estado == CONFIG:
        display.scroll(str(countdown_time))
        secuencia_ingresada = []

        if accelerometer.was_gesture("shake"):
            estado = ARMED
            last_tick = utime.ticks_ms()
            display.show(Image.SURPRISED)

    elif estado == ARMED:
        tiempo_actual = utime.ticks_ms()

        if tiempo_actual - last_tick >= 1000:
            countdown_time -= 1
            display.show(str(countdown_time))
            last_tick = tiempo_actual

        # Lectura de entradas
        if button_a.was_pressed():
            secuencia_ingresada.append('A')
        if button_b.was_pressed():
            secuencia_ingresada.append('B')
        if accelerometer.was_gesture("shake"):
            secuencia_ingresada.append('SHAKE')

        if len(secuencia_ingresada) > len(secuencia_correcta):
            secuencia_ingresada.pop(0)

        if len(secuencia_ingresada) == len(secuencia_correcta):
            if verificar_secuencia():
                display.show(Image.HAPPY)
                music.play(music.POWER_UP)
                estado = CONFIG
                countdown_time = 20
                secuencia_ingresada = []
                sleep(1000)
                display.clear()

        if countdown_time <= 0:
            estado = EXPLODED
            display.show(Image.SKULL)
            explosion_galaga()
            sleep(2000)

    elif estado == EXPLODED:
        
        if pin_logo.is_touched():
            estado = CONFIG
            countdown_time = 20
            display.clear()
```
