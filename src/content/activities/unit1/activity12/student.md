Le agregué funcionalidad a los botones A, B, C (shake), T (tactil) cada una interpreta diferentes colores en p5.js mientras que en micro:bit agregamos una imagen diferente para cada botón.

### Micro:bit 
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
### p5.js

``` js
let port;
let connectBtn;
let sendBtn;

function setup() {
    createCanvas(400, 400);
    background(220);
    port = createSerial();
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);
    
  
    fill('white');
    ellipse(width / 2, height / 2, 100, 100);
}

function draw() {

    if(port.availableBytes() > 0){
        let dataRx = port.read(1);
        if(dataRx == 'A'){
            fill('red');   
        }
        else if(dataRx == 'B'){
            fill('yellow'); 
        }
        else if(dataRx == 'T'){
            fill('#9C27B0'); 
        }
        else{
            fill('green'); 
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
