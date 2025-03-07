Primero encontramos un error en la de indentación y errores de sintaxis en la línea de SMILE

```js
elif current_state == STATE_SMILE:
        if button_a.was_pressed():
            display.show(Image.HAPPY)
            start_time = utime.ticks_ms()
            interval = HAPPY_INTERVAL
            current_state = STATE_HAPPY
        elif utime.ticks_diff(utime.ticks_ms(), start_time) > interval:
            display.show(Image.SAD)
            start_time = utime.ticks_ms()
            interval = SAD_INTERVAL
        current_state = STATE_SAD //<--acá
```

### Vectores de prueba
Para probar que el sistema funciona correctamente, definimos tres vectores de prueba. En cada uno, observamos cómo cambia el estado según las condiciones iniciales y los eventos ocurridos.

Vector de prueba 1: Cambio automático de estados sin intervención del usuario
Condiciones iniciales
El sistema inicia en STATE_HAPPY.
Se deja que el tiempo transcurra sin presionar ningún botón.
Resultados esperados
Se muestra (Image.HAPPY) durante HAPPY_INTERVAL (1.5 segundos).
Se cambia automáticamente a  (Image.SMILE) después del tiempo establecido.
Se cambia automáticamente a  (Image.SAD) después de SMILE_INTERVAL (1 segundo).
Se cambia automáticamente a  (Image.HAPPY) después de SAD_INTERVAL (2 segundos).

Resultados obtenidos
El sistema pasa correctamente por los estados en el tiempo esperado sin intervención del usuario.

Vector de prueba 2: Intervención del usuario con el botón A en estado HAPPY
Condiciones iniciales
El sistema está en STATE_HAPPY.
Se presiona el botón A antes de que cambie automáticamente.
Resultados esperados
Al presionar el botón A, inmediatamente cambia a (Image.SAD).
Se mantiene en STATE_SAD durante SAD_INTERVAL (2 segundos).
Luego, el sistema cambia automáticamente a (Image.HAPPY).

Resultados obtenidos
✅ El botón A interrumpe correctamente el flujo automático y lleva al estado STATE_SAD. Luego, el sistema continúa con la secuencia normal.

Vector de prueba 3: Presionar el botón A en diferentes estados para ver si cambia correctamente
Condiciones iniciales
Se deja que el sistema llegue a STATE_SAD sin intervención.
Luego, se presiona el botón A en STATE_SAD.
Resultados esperados
Se inicia en  (Image.SAD).
Se presiona el botón A → cambia inmediatamente a (Image.SMILE).
Después de SMILE_INTERVAL (1 segundo), cambia automáticamente a (Image.SAD).
Si no se toca nada más, después de SAD_INTERVAL (2 segundos) volverá a (Image.HAPPY).

Resultados obtenidos
✅ El sistema reacciona correctamente al botón A en STATE_SAD, cambiando a STATE_SMILE, y luego sigue la transición automática.
