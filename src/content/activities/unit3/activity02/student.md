Definición de la secuencia correcta:
Definí una lista llamada secuencia_correcta que contiene el orden exacto de las acciones necesarias para desactivar la bomba:


secuencia_correcta = ['A', 'B', 'A', 'SHAKE']

Captura de las acciones del usuario:
Durante el estado ARMED, cada vez que el usuario presiona el botón A, el botón B, o agita el micro:bit, se registra el evento en una lista llamada secuencia_ingresada. Esto se hace con button_a.was_pressed(), button_b.was_pressed() y accelerometer.was_gesture("shake").

Control del tamaño de la secuencia ingresada:
Para que solo se guarden las últimas 4 acciones, se verifica que la lista no exceda el tamaño de la secuencia correcta. Si lo hace, se elimina el primer elemento:


if len(secuencia_ingresada) > len(secuencia_correcta):
    secuencia_ingresada.pop(0)
    
Verificación de coincidencia:
Una vez que la lista secuencia_ingresada tiene 4 elementos, se compara con la secuencia correcta mediante la función verificar_secuencia(). Si coinciden:

Se muestra una imagen de felicidad (Image.HAPPY)

Se reproduce un sonido de éxito (music.POWER_UP)

La bomba vuelve al estado de configuración (CONFIG)

Se reinicia el tiempo de cuenta regresiva a 20 segundos

Si la secuencia no es correcta, la bomba continúa su cuenta regresiva sin interrupción.

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
