Implementé la funcionalidad solicitada separando claramente la detección de eventos (entrada desde sensores y puerto serial) del control de la bomba (la máquina de estados). Para esto:

Variables de evento:
Usé evento_ocurrido (booleano) para indicar si ocurrió un evento.

(,el .Usé evento (string) para guardar cuál fue el evento: 'A', 'B', 'S' o 'T'.

Función tareaEventos():
Revisa si se presionó un botón, se agitó el micro:bit, se tocó el logo o llegó un dato por el serial.
Si detecta un evento, actualiza evento y pone evento_ocurrido = True.
Solo se procesa un evento por ciclo (para evitar conflictos).

Función tareaBomba():
Es la máquina de estados (CONFIGURACION, ARMADO, EXPLOSION).
Solo actúa cuando evento_ocurrido es True, lee el evento, actúa según el estado, y luego consume el evento (poniendo evento_ocurrido = False).

Así, la lógica de la bomba es independiente de la fuente del evento (sensor o serial).

```
from microbit import *
import utime
import music

# Estados
CONFIGURACION = 0
ARMADO = 1
EXPLOSION = 2

estado = CONFIGURACION
contador = 20
ultimo_tiempo = utime.ticks_ms()

evento_ocurrido = False
evento = ""

secuencia = ['A', 'B', 'A', 'S']
indice_secuencia = 0
tiempo_ultima_secuencia = utime.ticks_ms()

def actualizar_display(tiempo):
    display.show(str(tiempo))

def explotar():
    display.show(Image.SKULL)
    music.play(music.POWER_DOWN)
    sleep(1000)
    display.clear()

def tareaEventos():
    global evento_ocurrido, evento

    if not evento_ocurrido: 
        if button_a.was_pressed():
            evento = 'A'
            evento_ocurrido = True
        elif button_b.was_pressed():
            evento = 'B'
            evento_ocurrido = True
        elif accelerometer.was_gesture("shake"):
            evento = 'S'
            evento_ocurrido = True
        elif pin_logo.is_touched():
            evento = 'T'
            evento_ocurrido = True
        elif uart.any():
            byte = uart.read(1)
            if byte:
                evento = byte.decode('utf-8').strip().upper()
                evento_ocurrido = True

def tareaBomba():
    global estado, contador, ultimo_tiempo
    global evento_ocurrido, evento, indice_secuencia

    if estado == CONFIGURACION:
        actualizar_display(contador)

        if evento_ocurrido:
            if evento == 'A' and contador < 60:
                contador += 1
            elif evento == 'B' and contador > 10:
                contador -= 1
            elif evento == 'S':
                estado = ARMADO
                display.scroll("Armed")
                ultimo_tiempo = utime.ticks_ms()
                indice_secuencia = 0

            actualizar_display(contador)
            evento_ocurrido = False  # Consumir evento

    elif estado == ARMADO:
        tiempo_actual = utime.ticks_ms()

        if evento_ocurrido:
            if evento == secuencia[indice_secuencia]:
                indice_secuencia += 1
            else:
                indice_secuencia = 0  # Reset si se rompe la secuencia

            evento_ocurrido = False  # Consumir evento

        if indice_secuencia == len(secuencia):
            estado = CONFIGURACION
            contador = 20
            display.scroll("Reset")
            indice_secuencia = 0

        if tiempo_actual - ultimo_tiempo >= 1000:
            ultimo_tiempo = tiempo_actual
            if contador > 0:
                contador -= 1
                actualizar_display(contador)
            else:
                estado = EXPLOSION

    elif estado == EXPLOSION:
        explotar()

        while True:
            if pin_logo.is_touched():
                evento = 'T'
            elif uart.any():
                byte = uart.read(1)
                if byte:
                    evento = byte.decode('utf-8').strip().upper()

            if evento == 'T':
                estado = CONFIGURACION
                contador = 20
                display.scroll("Reset")
                evento = ""
                evento_ocurrido = False
                break

            sleep(50)

uart.init(baudrate=115200)
sleep(500)
display.scroll("Config")


while True:
    tareaEventos()
    tareaBomba()
```
