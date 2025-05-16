```
<script src="https://unpkg.com/@gohai/p5.webserial@^1/libraries/p5.webserial.js"></script>
```

```p5
const CONFIGURACION = 0;
const ARMADO = 1;
const EXPLOSION = 2;

let estado = CONFIGURACION;
let contador = 20;
let ultimoTiempo = 0;
let secuenciaEsperada = ['A', 'B', 'A', 'Shake'];
let secuenciaActual = [];

let port;
let connectBtn;
let botonReset;
let displayText = "";

function setup() {
  createCanvas(400, 300);
  textAlign(CENTER, CENTER);
  textSize(32);

  // Botón de conexión al micro:bit
  connectBtn = createButton('Connect to micro:bit');
  connectBtn.position(20, 250);
  connectBtn.mousePressed(connectBtnClick);

  // Botón reset para reiniciar EXPLOSION
  botonReset = createButton('Reset');
  botonReset.position(160, 250);
  botonReset.mousePressed(resetear);

  // Inicializar puerto serial
  port = createSerial();
}

function draw() {
  background(220);

  // Mostrar estado y texto en pantalla
  if (estado === CONFIGURACION) {
    actualizarDisplay(contador);
  } else if (estado === ARMADO) {
    let tiempoActual = millis();
    if (tiempoActual - ultimoTiempo >= 1000) {
      ultimoTiempo = tiempoActual;
      if (contador > 0) {
        contador--;
        actualizarDisplay(contador);
      } else {
        estado = EXPLOSION;
        displayText = "BOOM!";
      }
    }

    // Comprobar secuencia
    if (secuenciaActual.length === secuenciaEsperada.length) {
      if (JSON.stringify(secuenciaActual) === JSON.stringify(secuenciaEsperada)) {
        estado = CONFIGURACION;
        contador = 20;
        secuenciaActual = [];
        displayText = "Config";
      } else {
        secuenciaActual = []; // Reinicia secuencia si es incorrecta
      }
    }
  } else if (estado === EXPLOSION) {
    background(255, 0, 0);
    text("BOOM!", width / 2, height / 2);
  }

  // Leer datos serial si está conectado
  if (port && port.opened()) {
    if (port.availableBytes() > 0) {
      let dataRx = port.readUntil('\n').trim();
      if (dataRx) {
        console.log("Recibido:", dataRx);
        manejarDatoRecibido(dataRx);
      }
    }
  }

  // Mostrar displayText en pantalla
  fill(0);
  text(displayText, width / 2, height / 2 - 30);

  // Mostrar estado de conexión
  fill(port && port.opened() ? 'green' : 'red');
  ellipse(width - 20, 20, 15, 15);
}

function actualizarDisplay(tiempo) {
  displayText = tiempo;
}

function manejarDatoRecibido(dato) {
  // Traducir el dato recibido a la secuencia
  if (estado === CONFIGURACION && dato === 'S') {
    // Shake recibido en Config => Cambia a ARMADO
    estado = ARMADO;
    displayText = "Armed";
    ultimoTiempo = millis();
  } else if (estado === ARMADO) {
    // Solo aceptar A, B, Shake (S)
    if (dato === 'A' || dato === 'B' || dato === 'S') {
      if (dato === 'S') secuenciaActual.push('Shake');
      else secuenciaActual.push(dato);
    }
  }
}

function resetear() {
  if (estado === EXPLOSION) {
    estado = CONFIGURACION;
    contador = 20;
    secuenciaActual = [];
    displayText = "Config";
  }
}

function connectBtnClick() {
  if (port && !port.opened()) {
    port.open('MicroPython', 115200);
  } else if (port && port.opened()) {
    port.close();
  }
}


```
