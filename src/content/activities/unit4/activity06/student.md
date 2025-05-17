Solución a la actividad
¿Qué es un protocolo de comunicación y por qué es importante en la comunicación serial?
Es básicamente un conjunto de reglas que se establecen entre dos dispositivos para lograr una conexión. En la comunicación serial, estas reglas definen cómo se envían y reciben los datos, permitiendo que ambos dispositivos se entiendan correctamente.

¿Por qué se separan los datos con comas en el protocolo ASCII que exploramos?
Porque si no se separan los datos con comas, se enviarían uno junto al otro (por ejemplo: 969652TrueFalse969652TrueFalse), lo cual dificulta su lectura y análisis desde la consola. Las comas permiten identificar fácilmente cada valor por separado.

¿Por qué es necesario terminar los datos con un carácter que marque el fin del mensaje?
Porque el carácter de fin de línea (\n) o "enter" indica al programa que ha terminado un paquete de datos. Esto es fundamental para que el puerto serial interprete correctamente el mensaje. Si no se incluye, puede generarse un sobrecupo en el puerto o los datos pueden no enviarse adecuadamente.

¿Por qué fue necesario usar una máquina de estados en la aplicación modificada de p5.js?
Porque permite estructurar mejor la lógica del programa según diferentes situaciones (estados), facilitando la lectura y organización del código, especialmente cuando hay múltiples interacciones posibles con el micro:bit y el usuario.

¿Cómo se formatean los datos en el micro:bit para ser enviados por el puerto serial?
Se convierten a cadenas de texto (strings), separados por comas y terminados en un salto de línea. Esto asegura que puedan ser entendidos fácilmente por el programa receptor (como uno hecho en p5.js).

¿Qué significa que los datos enviados por el micro:bit están codificados en ASCII?
Significa que los datos están representados como caracteres según el estándar ASCII, lo cual facilita su compatibilidad con múltiples plataformas y lenguajes de programación, ya que es un lenguaje universal para representar texto.

¿Por qué es necesario en la aplicación de p5.js preguntar si hay bytes disponibles en el puerto serial antes de leerlos?
Porque aunque el puerto esté abierto, los datos no llegan constantemente. Verificar con port.availableBytes() > 0 evita errores de lectura y asegura que solo se procesen datos cuando realmente hay algo disponible, como en el ejemplo del portero que solo abre si hay alguien tocando.

¿Cómo se elimina el retorno de carro o salto de línea de un string en p5.js?
Usando el método .trim() o .replace(). El primero elimina espacios y saltos de línea al principio y al final de la cadena:

data = data.trim();
Si una cadena tiene información separada por espacios y quieres dividir dicha información en varias cadenas individuales ¿Qué función de p5.js usarías?
La función split(), por ejemplo:


let values = data.split(" ");
¿Por qué es necesario en la aplicación del caso de estudio convertir las cadenas a números enteros antes de usarlas en el sketch de p5.js?
Porque las cadenas y los números son tipos de datos distintos. Si no se convierten a enteros, no se pueden utilizar en cálculos matemáticos ni manipulaciones gráficas correctamente.

Si el micro:bit tiene los siguientes datos: xValue: 123, yValue: 756, aState: False, bState: True ¿Qué bytes se enviarían por el puerto serial?
Se enviarían como:


123,756,False,True\n
Esto representa: posición en el eje X (123), eje Y (756), botón A no presionado, botón B presionado.

¿Qué aprendiste nuevo del micro:bit que no sabías antes?
Sabía que se podía interactuar con botones y sensores desde p5.js, pero no que era posible usar el giroscopio del micro:bit de esta manera. Esto abre muchas posibilidades creativas para experiencias interactivas.

¿Qué aprendiste nuevo de p5.js que no sabías antes?
Aprendí que se pueden integrar múltiples funcionalidades en un solo programa de forma sencilla, como cambiar colores o formas con solo presionar teclas (1–9). Esto lo hace muy dinámico y fácil de expandir. Por ejemplo:

if (key === "1") c = color(181, 157, 0);
if (key === "2") c = color(0, 130, 164);
if (key === "3") c = color(87, 35, 129);
