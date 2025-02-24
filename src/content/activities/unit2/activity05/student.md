Creación con botón llamado error que emite LED de fantasma con musicalización terrorífica.

### Micro:Bit
```js
from microbit import *
import music

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
        sleep(500)
   
    if uart.any():
        data = uart.read(1)
        if data:
            if data[0] == ord('h'):
                display.show(Image.GHOST)
                music.play(music.DADADADUM)
      ```
### p5.js
```js

let port;
let connectBtn;

function setup() {
    createCanvas(400, 400);
    background(150);
    port = createSerial();
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);
    let sendBtn = createButton('Error');
    sendBtn.position(220, 300);
    sendBtn.mousePressed(sendBtnClick);
    fill('white');
    ellipse(width / 2, height / 2, 100, 100);
}

function draw() {

    if(port.availableBytes() > 0){
        let dataRx = port.read(1);
        if(dataRx == 'A'){
            fill('red');   
        }
        
        background(220);
        ellipse(width / 2, height / 2, 100, 100);
        fill('black');
        text(dataRx, width / 2, height / 2);
    }    


    if (!port.opened()) {
        connectBtn.html('Connect to micro:bit');
    } 
    else {
        connectBtn.html('Disconnect');
    }
}

function connectBtnClick() {
    if (!port.opened()) {
        port.open('MicroPython', 115200);
    } else {
        port.close();
    }
}

function sendBtnClick() {
    port.write('h');
}
```
### Importación de librerías

from microbit import *
import music
Se importan las librerías necesarias para controlar el Micro:bit. microbit permite manejar la pantalla, botones y sensores, mientras que music se usa para reproducir sonidos.

Inicialización del puerto serial (UART)

uart.init(baudrate=115200)
Se configura la comunicación UART con una velocidad de 115200 baudios para enviar y recibir datos entre el Micro:bit y otro dispositivo.

Mostrar una imagen de primeras personalizada en la pantalla LED 

display.show(Image('00000:'
                   '33333:'
                   '55555:'
                   '77777:'
                   '99999'))
Se muestra un patrón de números en la pantalla LED. Cada fila contiene valores que representan el brillo de los LEDs (0 = apagado, 9 = máximo brillo).

Bucle principal (while True)
Se ejecuta de forma continua para verificar eventos en los botones y la comunicación serial.

Manejo del botón A

if button_a.is_pressed():
    uart.write('A')
    display.scroll("GALI")
    sleep(500)
Si el botón A es presionado, se envía la letra 'A' por UART.
Luego, el mensaje "GALI" se desplaza en la pantalla LED.
Se usa sleep(500) para dar un pequeño retraso y evitar múltiples lecturas seguidas.

Recepción de datos por UART

if uart.any():
    data = uart.read(1)
    if data:
        if data[0] == ord('h'):
            display.show(Image.GHOST)
            music.play(music.DADADADUM)
Si hay datos en el puerto serial (uart.any()), se lee un byte (uart.read(1)).
Si el dato recibido es la letra 'h', se muestra la imagen de un fantasma en la pantalla LED.
Además, se reproduce la melodía DADADADUM de la librería music.
