Pondré de ejemplo la actividad 12 de la unidad 1, ahí tuvimos 3 interacciones diferentes, botones, acelerometro y táctil:
¿Qué queríamos comprobar?
Queríamos verificar que el Micro:bit puede enviar datos a través de su puerto serial (UART) cuando se presionan los botones A y B, se detecta un movimiento de agitación o se toca el pin logo.

¿Cuál fue nuestra hipótesis?
Si el Micro:bit detecta la interacción del usuario mediante botones, movimiento o toque en el pin logo, entonces enviará un carácter específico ('A', 'B', 'C' o 'T') por UART y cambiará la imagen en su pantalla.

### MICRO:BIT
``` js
from microbit import *

uart.init(baudrate=115200)
display.show(Image('00000:'
                   '33333:'
                   '55555:'
                   '77777:'
                   '99999'))

while True:
    if button_a.is_pressed():
        uart.write('A')
        display.show(Image.GHOST)
        sleep(500)
    if button_b.is_pressed():
        uart.write('B')
        display.show(Image.SKULL)  
        sleep(500)
    if accelerometer.was_gesture('shake'):
        display.show(Image.HAPPY) 
        uart.write('C')
        sleep(500)
    if pin_logo.is_touched():  
        uart.write('T')
        display.show(Image.SAD) 
```

Descripción de los resultados
Al presionar el botón A, el Micro:bit enviaba la letra 'A' por UART y mostraba la imagen de un fantasma en la pantalla.
Al presionar el botón B, el Micro:bit enviaba la letra 'B' por UART y mostraba una calavera.
Al agitar el Micro:bit, este enviaba la letra 'C' y mostraba una cara feliz.
Al tocar el pin_logo, el Micro:bit enviaba la letra 'T' y mostraba una cara triste en la pantalla.
### Análisis de los resultados
El Micro:bit respondió correctamente a cada interacción, cambiando la imagen en su pantalla y enviando los datos esperados por UART.
El uso de sleep(500) después de cada acción evitó la repetición no deseada de los envíos de datos.
La detección del toque en el pin_logo funcionó correctamente, aunque, a diferencia de los botones, este no tiene una acción de "soltar", lo que podría hacer que el Micro:bit envíe múltiples veces la letra 'T' si el pin se mantiene tocado.
### Conclusiones
El Micro:bit puede detectar y diferenciar varias interacciones del usuario y enviar información correspondiente a través de UART.
La representación visual en la pantalla permite confirmar que cada evento se ejecutó correctamente.
Se podría mejorar el código agregando una espera (sleep) tras la detección del pin_logo para evitar múltiples envíos de 'T'.
También se podría implementar la lectura de datos recibidos para permitir comunicación bidireccional.
