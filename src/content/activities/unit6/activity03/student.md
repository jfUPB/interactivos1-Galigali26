### Dependecias
```
const express = require('express');
const http = require('http');
const socketIO = require('socket.io');
const path = require('path');
```

### ¿Qué hacen?

express: framework para manejar rutas y respuestas HTTP fácilmente.

http: base para crear el servidor.
socket.io: habilita la comunicación en tiempo real (cliente-servidor-cliente).
path: asegura compatibilidad de rutas en diferentes sistemas operativos.
Ventaja de usar módulos: reutilización de código probado, ahorro de tiempo, mayor seguridad y mantenibilidad.

### 2. Creación del servidor y conexión de Socket.IO

```
const app = express();
const server = http.createServer(app);
const io = socketIO(server);
const port = 3000;
```
app es tu servidor Express.

server es el servidor HTTP que sirve tu aplicación.

io habilita Socket.IO sobre ese servidor.
port define en qué puerto escuchar.

### 3.  Variables de estado

```
let page1 = { x: 0, y: 0, width: 100, height: 100 };
let page2 = { x: 0, y: 0, width: 100, height: 100 };
```
Estas guardan la última posición/tamaño recibida desde cada ventana.

### 4.  Archivos estáticos del cliente

```
app.use(express.static(path.join(__dirname, 'views')));
```
Esto le dice a Express que sirva los archivos HTML, CSS y JS que estén en la carpeta views.
Experimento clave:
Si cambias a una carpeta inexistente ('archivos_cliente'), el servidor no podrá encontrar ni servir los archivos, y verás un error 404 en el navegador.

### 5. Rutas personalizadas
```
app.get('/page1', (req, res) => {
  res.sendFile(path.join(__dirname, 'views', 'page1.html'));
});
```
Y lo mismo para /page2.

Prueba clave:
Si cambias la ruta a /pagina_uno, debes cambiar también la URL del navegador. Las rutas son exactas: si el navegador pide /page1, Express no responde a menos que lo hayas definido explícitamente.

###  6. Conexión de clientes vía Socket.IO
```
io.on('connection', (socket) => {
  console.log('A user connected - ID:', socket.id);

  socket.on('disconnect', () => {
    console.log('User disconnected - ID:', socket.id);
  });
});
```

Cada cliente conectado es único y tiene su propio socket.id.

Prueba clave:
Conecta dos clientes (page1 y page2), observa sus IDs, luego cierra una pestaña. El servidor te lo informará.

### 7. Recepción y retransmisión de datos
```
socket.on('win1update', (window1, sendid) => {
  page1 = window1;
  socket.broadcast.emit('getdata', page1);
});
```
 Recibe window1 de un cliente (page1).

Actualiza page1 global.
Retransmite getdata a todos los demás clientes excepto al que envió.

Test clave:
Si usas socket.emit() en lugar de broadcast.emit(), solo el cliente que envía el mensaje lo recibe (no se comparte con los demás).

### 8. Iniciar el servidor

```
server.listen(port, () => {
  console.log(`Server is listening on http://localhost:${port}`);
});
```
Inicia el servidor y lo deja escuchando en el puerto asignado.

Test clave:
Cambia port = 3001. Solo podrás acceder al servidor en http://localhost:3001, no en el 3000.

FLUJO COMPLETO:
Cliente abre page1 o page2.

Se conecta al servidor mediante Socket.IO.

El servidor asigna un ID y escucha eventos como win1update.
El cliente envía datos de posición.
El servidor actualiza su estado y retransmite la info a los demás.
Al cerrar el navegador, se informa al servidor de la desconexión.








