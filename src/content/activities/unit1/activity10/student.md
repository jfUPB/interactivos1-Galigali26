### Conexión y comunicación entre Micro:bit y p5.js
Conexión: El navegador se conecta al Micro:bit a través de un puerto serial cuando el usuario presiona el botón "Connect to micro:bit".

nvío de datos (Micro:bit → p5.js):

Si presionas el botón A, el Micro:bit envía "A" y dice GALI en la pantalla.
Si presionas el botón B, envía "B" y pone una cara feliz en la pantalla.
Si lo sacudees, envía "C".
p5.js recibe estos datos y cambia el color del cuadrado en la pantalla.
envío de datos (p5.js → Micro:bit):

Si se presiona el botón "Tristeza", p5.js envía "h" al Micro:bit y cuando lo recibe, el Micro:bit muestra una cara de desagrado en la pantalla.

### Código en p5.js
``` js
let port;
let connectBtn;

function setup() {
    createCanvas(400, 400);
    background(220);
    port = createSerial();
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);
    let sendBtn = createButton('Tristeza');
    sendBtn.position(220, 300);
    sendBtn.mousePressed(sendBtnClick);
    fill('white');
    rectMode(CENTER); // Para que el cuadrado se dibuje desde el centro
    rect(width / 2, height / 2, 100, 100);
}

function draw() {
    if (port.availableBytes() > 0) {
        let dataRx = port.read(1);
        if (dataRx == 'A') {
            fill('#9C27B0');   
        }
        else if (dataRx == 'B') {
            fill('#03A9F4'); 
        }
        else {
            fill('#FF5722'); 
        }
        background(220);
        rectMode(CENTER);
        rect(width / 2, height / 2, 100, 100); // Dibuja el cuadrado
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

### Código Micro:bit 

``` py
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
        display.show(Image.HAPPY)
        sleep(500)
    if accelerometer.was_gesture('shake'):
        uart.write('C')
        sleep(500)
    if uart.any():
        data = uart.read(1)
        if data:
            if data[0] == ord('h'):
                display.show(Image.SAD)
                sleep(400)
                
                display.show(Image.CONFUSED)
                sleep(400)
```
