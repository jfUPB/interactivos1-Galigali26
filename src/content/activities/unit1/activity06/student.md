### Punto 15: A y B micro:bit.
En la pantalla del programa p5.js, el círculo cambia de color.
Rojo:A
Amarillo:B
El micro:bit detecta que presiona un botón y manda la letra correspondiente por serial(UART).
En p5.js recibe esa letra y dependiendo de cual sea cambia el color del circulo y muestra el texto.

### Punto 16: Sacudir micro:bit.
Si sacudo el micro:bit, detecta el movimiento y envía la letra c.
El micro:bit, tiene un acelerómetro que detecta cuando lo sacudes.
Cuando eso sucede, manda la letra C por serial.
El programa p5.js lo recibe y al no ser a ni b , entra en la última opción por defecto y cambia el color a verde.

### Punto 17: Presiona el botón "Send Love"
Si presiono el botón  en la interfaz, la computadora le envía la información a micro:bit la letra h.
La respuesta es que el micro:bit muestra un corazón por un momento en la pantalla.
Luego cambia a una cara feliz.
El botón en p5.js está porgramado para mandar la letra h por serial cuando la presiono.
El micro:bit recibe esa letra, la identifica y cambia su pantalla para mostrar primero el corazón y luego la cara feliz.

