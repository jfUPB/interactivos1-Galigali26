


```p5
<script src="https://unpkg.com/@gohai/p5.webserial@^1/libraries/p5.webserial.js"></script>
```

```p5
let port;
let connectBtn;
let aBtn, bBtn, sBtn, tBtn;
let receivedMsg = "";

function setup() {
    createCanvas(400, 400);
    background(220);
    textAlign(CENTER, CENTER);
    textSize(24);

    // Configura el puerto serial
    port = createSerial();
    connectBtn = createButton('Connect to micro:bit');
    connectBtn.position(80, 300);
    connectBtn.mousePressed(connectBtnClick);

    // Botones para enviar eventos
    aBtn = createButton('A');
    aBtn.position(80, 350);
    aBtn.mousePressed(() => sendButtonClick('A'));

    bBtn = createButton('B');
    bBtn.position(160, 350);
    bBtn.mousePressed(() => sendButtonClick('B'));

    sBtn = createButton('S');
    sBtn.position(240, 350);
    sBtn.mousePressed(() => sendButtonClick('S'));

    tBtn = createButton('T');
    tBtn.position(320, 350);
    tBtn.mousePressed(() => sendButtonClick('T'));
}

function draw() {
    background(220);

    // Título
    text("Micro:bit Control Interface", width / 2, 40);

    // Estado de conexión
    if (!port.opened()) {
        connectBtn.html('Connect to micro:bit');
    } else {
        connectBtn.html('Disconnect');

        // Lectura serial
        if (port.availableBytes() > 0) {
            let dataRx = port.readUntil('\n').trim();
            if (dataRx) {
                receivedMsg = dataRx;
                console.log("Recibido:", receivedMsg);
            }
        }
    }

    // Mostrar mensaje recibido
    fill(0);
    text("Mensaje recibido:", width / 2, 150);
    fill('blue');
    text(receivedMsg, width / 2, 190);
}

function connectBtnClick() {
    if (!port.opened()) {
        port.open('MicroPython', 115200);
    } else {
        port.close();
    }
}

function sendButtonClick(letter) {
    if (port.opened()) {
        port.write(letter + '\n');
        console.log("Mensaje enviado:", letter);
    } else {
        console.log("Error: el puerto serial no está abierto.");
    }
}
```
