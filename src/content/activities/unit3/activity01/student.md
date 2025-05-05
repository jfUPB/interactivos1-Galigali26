```js

from microbit import *

imagenes1 = {
    'rojo': Image('99999:00000:00000:00000:00000'),
    'amarillo': Image('00000:00000:99999:00000:00000'),
    'verde': Image('00000:00000:00000:00000:99999')
}

imagenes2 = {
    'rojo': Image('66666:00000:00000:00000:00000'),
    'amarillo': Image('00000:00000:66666:00000:00000'),
    'verde': Image('00000:00000:00000:00000:66666')
}

imagenes3 = {
    'rojo': Image('33333:00000:00000:00000:00000'),
    'amarillo': Image('00000:00000:33333:00000:00000'),
    'verde': Image('00000:00000:00000:00000:33333')
}

def mostrar_semaforo(nombre, tiempos, imagenes):
    for color in ['rojo', 'amarillo', 'verde']:
        display.scroll(nombre, wait=False, loop=False)
        for i in range(tiempos[color]):
            display.show(imagenes[color])
            sleep(1000)

tiempos1 = {'rojo': 5, 'amarillo': 2, 'verde': 3}
tiempos2 = {'rojo': 3, 'amarillo': 1, 'verde': 2}
tiempos3 = {'rojo': 4, 'amarillo': 3, 'verde': 2}

# Bucle principal: muestra los semáforos uno tras otro
while True:
    mostrar_semaforo("S1", tiempos1, imagenes1)
    mostrar_semaforo("S2", tiempos2, imagenes2)
    mostrar_semaforo("S3", tiempos3, imagenes3)

```
