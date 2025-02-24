### Micro:Bit
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
        sleep(500)
    if button_b.is_pressed():
        uart.write('B')
        sleep(500)
```




### Código en p5
``` py
let port;
let connectBtn;
let sendBtn;
let circleX;

function setup() {
    createCanvas(400, 400);
    background(220);
    port = createSerial();
    
    connectBtn = createButton('conectar a micro:bit');
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);

    circleX = width / 2; 
}

function draw() {
    background(220);
    fill('white');
    ellipse(circleX, height / 2, 100, 100);
    
    if (port.availableBytes() > 0) {
        let dataRx = port.read(1);
        if (dataRx == 'A') {
            circleX -= 20; 
        } else if (dataRx == 'B') {
            circleX += 20; 
        }
        circleX = constrain(circleX, 50, width - 50); 
    }

    if (!port.opened()) {
        connectBtn.html('conectar a micro:bit');
    } else {
        connectBtn.html('Desconectar');
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
### Explicación:

El código en p5.js conecta el Micro:bit y usa sus botones para mover un círculo en la pantalla:

Inicializa la conexión serial y dibuja un círculo en el centro.
Escucha datos del Micro:bit:
Si recibe 'A', mueve el círculo a la izquierda.
Si recibe 'B', lo mueve a la derecha.
Constrain() para evitar que el círculo salga de la pantalla.
Incluye botones para conectar/desconectar el Micro:bit y enviar datos.
En resumen: El Micro:bit actúa como un control remoto para mover el círculo en p5.js.

