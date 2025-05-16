Variables utilizadas:

xValue: representa la inclinación detectada en el eje X por el acelerómetro.

yValue: representa la inclinación detectada en el eje Y por el acelerómetro.

aState: indica si el botón A está presionado (True) o no (False).

bState: indica si el botón B está presionado (True) o no (False).

Formato de envío:

"{},{},{},{}\n".format(xValue, yValue, aState, bState)


con el formato CSV:

True,False
Ahora los valores están claramente separados y es más fácil entenderlos.

Frecuencia de transmisión:
sleep(100)

Este comando pausa el envío de datos durante 100 milisegundos. Esto significa que el micro:bit está enviando datos a una frecuencia de 10 Hz (10 veces por segundo).
Si no se incluye esta pausa, el puerto serial podría saturarse debido al exceso de información, causando fallos en la comunicación.

Valores del acelerómetro:
Los valores en los ejes X y Y cambian dependiendo de cómo inclines o muevas el micro:bit.

El rango de valores puede alcanzar hasta aproximadamente ±1024.

Estados de los botones:

Si un botón está presionado, su estado será True; de lo contrario, será False.

La función is_pressed() detecta si el botón ha sido presionado y devuelve ese estado.

Datos enviados en ASCII:

Los datos se envían por el puerto serial utilizando codificación ASCII, lo cual convierte cada carácter (número, coma, letra) en un valor hexadecimal.

Ejemplo de mensaje: 

39 36 39 2C 36 35 32 2C 54 72 75 65 2C 46 61 6C 73 65 0A

Esto representa:


Desglose:
39 36 39 → “969”
2C → coma ,
0A → salto de línea (fin del mensaje)
Así, cada carácter es traducido a su código ASCII antes de ser enviado por el micro:bit.

