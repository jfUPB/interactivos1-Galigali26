```js
from microbit import *
import utime
import music

# Definir estados
CONFIG = 0
ARMED = 1
EXPLODED = 2

# Estado inicial
estado = CONFIG

# Tiempo inicial
countdown_time = 20  # en segundos



# Variables de tiempo
last_tick = utime.ticks_ms()

def mostrar_tiempo(tiempo):
    display.scroll(str(tiempo)) 

def explosion_galaga():
    music.set_tempo(bpm=300)  
    music.play([
        'g5:1', 'e5:1', 'c5:1', 'g4:1', 
        'e4:2', 'c4:2', 'r:1',           
        'g3:3', 'e3:2', 'c3:3', 'r:1'   
    ])

while True:
    if estado == CONFIG:
        mostrar_tiempo(countdown_time)


        if accelerometer.was_gesture("shake"):
            estado = ARMED
            last_tick = utime.ticks_ms()  # Iniciar la cuenta regresiva

    elif estado == ARMED:
        tiempo_actual = utime.ticks_ms()
        
        if tiempo_actual - last_tick >= 1000:  # Cada segundo
            countdown_time -= 1
            mostrar_tiempo(countdown_time)
            last_tick = tiempo_actual
        
        if countdown_time <= 0:
            estado = EXPLODED
            display.show(Image.SKULL)
            explosion_galaga()  
            sleep(2000)
        
    elif estado == EXPLODED:
        if pin_logo.is_touched():
            estado = CONFIG
            countdown_time = 20
            display.clear()  # Limpiar pantalla antes de reiniciar

```
