1. ¿Cómo se están comunicando el micro:bit y el sketch de p5.js?
La comunicación es serial por USB o Bluetooth (depende de la conexión física).

El micro:bit envía datos en texto ASCII, separados por comas, terminando con un salto de línea (\n).

El sketch p5.js usa la librería createSerial() para abrir un puerto serial y leer esos datos.

2. ¿Qué datos envía el micro:bit?
Según el código, el micro:bit está enviando una línea con 4 valores separados por comas, que representan:


X, Y, ButtonA, ButtonB\n
X: un valor entero que representa la posición horizontal (probablemente un valor analógico o de acelerómetro).
Y: un valor entero que representa la posición vertical.

ButtonA: "true" o "false" si el botón A está presionado o no.
ButtonB: "true" o "false" si el botón B está presionado o no.

Ejemplo de línea recibida:
100,-50,true,false\n

3. ¿Cómo es la estructura del protocolo ASCII usado?
Cada mensaje es una línea de texto ASCII.

Los valores están separados por comas ,.

Terminan con salto de línea \n.

El sketch lee hasta el salto de línea para procesar cada mensaje completo.

"100,-50,true,false\n"
4. Código p5.js que lee los datos y los transforma en coordenadas
Esta es la parte donde se lee la entrada serial y se procesa:


if (port.availableBytes() > 0) {
  let data = port.readUntil("\n");  // lee hasta salto de línea
  if (data) {
    data = data.trim();              // elimina espacios y salto de línea
    let values = data.split(",");    // separa por coma

    if (values.length == 4) {
      microBitX = int(values[0]) + windowWidth / 2;  // convierte a entero y centra en pantalla
      microBitY = int(values[1]) + windowHeight / 2; // convierte a entero y centra en pantalla
      microBitAState = values[2].toLowerCase() === "true";  // convierte texto a booleano
      microBitBState = values[3].toLowerCase() === "true";  // convierte texto a booleano
      updateButtonStates(microBitAState, microBitBState);   // actualiza estados botones
    } else {
      print("No se están recibiendo 4 datos del micro:bit");
    }
  }
}
Explicación:

port.readUntil("\n"): lee una línea completa hasta salto de línea.

data.trim(): limpia espacios y saltos extra.

split(","): separa en un array con los 4 valores.

int() convierte las posiciones X, Y a números.

Se suman windowWidth/2 y windowHeight/2 para centrar los valores en la pantalla de p5.js (porque el micro:bit probablemente envía coordenadas relativas a un centro).

Los estados de botones se convierten a booleanos (true/false).

Se llama a updateButtonStates() para detectar eventos.

5. ¿Cómo se generan los eventos "A pressed" y "B released"?
Esta función compara el nuevo estado recibido del micro:bit con el estado anterior para detectar transiciones (cambios):


function updateButtonStates(newAState, newBState) {
  // Detecta evento "A pressed" (se presiona botón A)
  if (newAState === true && prevmicroBitAState === false) {
    lineModuleSize = random(50, 160);    // genera nuevo tamaño de línea
    clickPosX = microBitX;               // guarda posición click X
    clickPosY = microBitY;               // guarda posición click Y
    print("A pressed");
  }

  // Detecta evento "B released" (se suelta botón B)
  if (newBState === false && prevmicroBitBState === true) {
    c = color(random(255), random(255), random(255), random(80, 100));  // cambia color
    print("B released");
  }

  // Actualiza los estados previos para la siguiente comparación
  prevmicroBitAState = newAState;
  prevmicroBitBState = newBState;
}
Evento "A pressed":

Se detecta si el botón A pasó de false (no presionado) a true (presionado).

Se genera un tamaño de línea aleatorio y se guarda la posición actual del micro:bit.

Evento "B released":

Se detecta si el botón B pasó de true (presionado) a false (no presionado).

Se cambia el color c a uno nuevo aleatorio semi-transparente.

Esta lógica de comparar estados actuales y previos se llama detección de bordes (edge detection) y es común para detectar eventos de pulsación y liberación.



![image](https://github.com/user-attachments/assets/9af96be0-b87a-476f-a171-96db1a5d0ee0)
![image](https://github.com/user-attachments/assets/244ffbc9-aef2-462d-bc81-9953d1a902c4)
