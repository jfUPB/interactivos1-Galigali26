
Explicación del código
Desglose del código línea por línea
1. Importación de la biblioteca

from microbit import *
Se importa la biblioteca microbit, que proporciona acceso a los botones, la pantalla LED, el acelerómetro y la comunicación serial.

2. Inicialización de la comunicación UART
uart.init(baudrate=115200)
Se configura la comunicación serial a 115200 baudios para enviar datos a un dispositivo externo, como una computadora o un microcontrolador.

3. Mostrar una imagen personalizada en la pantalla al iniciar
display.show(Image('00000:'
                   '33333:'
                   '55555:'
                   '77777:'
                   '99999'))
   
5. Bucle principal (while True)
while True:
Se inicia un bucle infinito para revisar continuamente si el usuario ha presionado un botón o sacudido la Micro:bit.

6. Acción al presionar el botón A
if button_a.is_pressed():
    uart.write('A')  # Envía 'A' por UART
    display.scroll("GALI")  # Muestra el texto "GALI" desplazándose por la pantalla LED
    sleep(500)  # Espera 500 ms para evitar repeticiones rápidas
Si se presiona el botón A:

7. Acción al presionar el botón B
if button_b.is_pressed():
    uart.write('B')  # Envía 'B' por UART
    display.show(Image.SKULL)  # Muestra una calavera en la pantalla LED
    sleep(500)
Si se presiona el botón B:
Se envía la letra 'B' por UART.
Se muestra una imagen de calavera (Image.SKULL) en la pantalla LED.
sleep(500) evita que el código se repita rápidamente.

8. Acción al detectar un movimiento de sacudida

if accelerometer.was_gesture('shake'):
    uart.write('C')  # Envía 'C' por UART
    display.show(Image.DUCK)  # Muestra un pato en la pantalla LED
    sleep(500)
Si la Micro:bit detecta una sacudida (shake):
Se envía la letra 'C' por UART.
Se muestra la imagen de un pato (Image.DUCK).
sleep(500) evita que la acción se repita continuamente con movimientos pequeños.
Resumen de acciones
Acción	Envío UART	Visualización en la pantalla LED
Presionar botón A	'A'	Texto "GALI" desplazándose
Presionar botón B	'B'	Imagen de calavera (Image.SKULL)
Sacudir la Micro:bit	'C'	Imagen de pato (Image.DUCK)

### Micro:bit 
```js
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
        display.scroll("GALI")
        sleep(500)
    if button_b.is_pressed():
        uart.write('B')
        display.show(Image.SKULL)
        sleep(500)
        
    if accelerometer.was_gesture('shake'):
        uart.write('C')
        display.show(Image.DUCK)
        sleep(500)
   
    if uart.any():
        data = uart.read(1)
        if data:
         if data[0] == ord('h'):
            display.show(Image.HOUSE)

```
