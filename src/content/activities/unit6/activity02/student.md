1. Pausa activa: ¿Cómo te conectas a Internet? ¿Qué pasa si esa rampa se corta?
En casa uso Wi-Fi para conectarme a Internet, mientras que en la Universidad suelo usar una conexión por cable Ethernet, que suele ser más estable y rápida. Esa “rampa de acceso” es esencial para conectar mi dispositivo a la red global.

Si esa rampa se corta, por ejemplo si el router Wi-Fi deja de funcionar o si el cable Ethernet se desconecta, mi computadora pierde acceso a Internet y no podría navegar, enviar correos o usar apps que dependen de la red. Esto muestra que Internet no es mágico, depende de infraestructura física que debe estar intacta.

2. Pausa activa: Ejemplos de relaciones Cliente-Servidor en la vida diaria
Un ejemplo muy claro es un restaurante. El cliente es la persona que llega a pedir comida (el usuario). El servidor es el mesero que recibe el pedido y lo lleva a la cocina (servidor en sentido literal) para que preparen el platillo, y luego lo trae de vuelta al cliente.

También en una tienda, el comprador (cliente) solicita un producto y el dependiente (servidor) se lo entrega. Esta relación Cliente-Servidor es muy común en la vida, donde alguien pide algo y otro lo provee.

3. Pausa activa: Analizar una URL de mi sitio favorito y qué pasa si solo escribo el dominio
Por ejemplo, en la URL: [https://www.youtube.com/watch?v=dQw4w9WgXcQ
](https://www.youtube.com/watch?v=o5KyLuuqFms&list=RDo5KyLuuqFms&start_radio=1)



Nombre de dominio: /watch?v=o5KyLuuqFms&list=RDo5KyLuuqFms&start_radio=1)
/watch?v=dQw4w9WgXcQ

Si solo escribo www.youtube.com, sin ruta, el servidor envía la página principal o “página por defecto” (index.html o similar). Esto es como llegar al edificio principal sin pedir una sección específica, y te muestran la entrada general. Si no hay ruta, se asume que se quiere la página principal.

4. Pausa activa: Comparar HTTP con protocolos seriales
Similitudes:

Ambos son protocolos que establecen reglas para la comunicación correcta entre dos dispositivos.

Definen formatos, órdenes, y respuestas para que la información sea entendible.

Aseguran que el mensaje enviado sea recibido y procesado adecuadamente.

Diferencias:

HTTP está diseñado para la comunicación en red global entre clientes y servidores, con muchas reglas para manejar peticiones, respuestas, códigos de estado, tipos de contenido, etc.

Los protocolos seriales usados con micro:bit son más simples, para conexiones directas y punto a punto, y generalmente envían datos de forma cruda sin capas complejas.

HTTP es más complejo porque debe garantizar interoperabilidad universal, manejo de errores, estados múltiples, diferentes tipos de datos, seguridad y escalabilidad.

5. Pausa activa: HTML, CSS y JavaScript en una página de login
HTML: los campos de texto para usuario y contraseña, el botón de “Entrar”, las etiquetas y la estructura general del formulario.

CSS: el color del botón, el tipo de letra, el tamaño de los campos, márgenes, colores de fondo, estilos visuales que hacen que el formulario sea atractivo y legible.

JavaScript: la validación del formulario antes de enviarlo, por ejemplo, verificar que los campos no estén vacíos, mostrar mensajes de error “contraseña incorrecta” sin recargar la página, animaciones o efectos cuando el usuario escribe.

6. Pausa activa: ¿Cómo y cuándo se ejecuta JavaScript?
El navegador lee el HTML y construye el DOM. Luego aplica el CSS para dar estilo. Cuando encuentra una etiqueta <script>, puede:

Pausar el proceso para ejecutar el JS si el script está en medio del HTML, o

Ejecutar el JS después de cargar la estructura si se usa defer o async o está al final del body.

JavaScript no solo corre una vez de arriba abajo; suele esperar eventos (clics, cambios, datos recibidos) para actuar. Esto permite que la página sea interactiva y dinámica sin recargar.

7. Pausa activa: Comparar modelo draw() de p5.js vs modelo basado en eventos
El bucle draw() es imperativo, repite instrucciones constantemente aunque no haya cambios, lo que puede ser costoso en recursos.

El modelo basado en eventos es reactivo: el código solo se ejecuta cuando ocurre algo (clic, dato recibido, etc.), haciendo la aplicación más eficiente y responsiva.

Ventajas del modelo basado en eventos para UI web:

Reduce uso de CPU y batería al no redibujar o ejecutar código innecesariamente.

Permite interacción inmediata y específica según la acción del usuario o el sistema.

Mejora la escalabilidad y mantenimiento del código.

8. Pausa activa: Ventajas de usar JavaScript en cliente y servidor
Unifica el lenguaje para todo el stack de desarrollo, lo que facilita el aprendizaje y uso para los desarrolladores.

Permite compartir código (validaciones, funciones) entre cliente y servidor, evitando duplicaciones.

Facilita el desarrollo full-stack con tecnologías modernas como Node.js y frameworks JavaScript.

Agiliza la comunicación y colaboración entre equipos frontend y backend.

9. Pausa activa final: Diferencias entre HTTP tradicional y WebSockets/Socket.IO
HTTP tradicional es comunicación tipo “carta”: se hace una petición y se espera una respuesta, ideal para cargas estáticas o consultas ocasionales.

WebSockets/Socket.IO establecen una conexión permanente “línea telefónica” que permite mensajes instantáneos en ambas direcciones sin necesidad de abrir nuevas conexiones.

Aplicaciones que usan comunicación en tiempo real:

Chats en línea.

Juegos multijugador.

Colaboración en documentos en vivo.

Actualizaciones de datos en tiempo real (ej. dashboards, cotizaciones, sensores).

Videoconferencias y streaming interactivo.

