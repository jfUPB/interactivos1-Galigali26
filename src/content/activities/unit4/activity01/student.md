```
http://www.generative-gestaltung.de/2/sketches/?01_P/P_2_2_6_03
```

Encontré este diseño que me gustó mucho porque puedo hacer interacción con el.
Este código en p5.js crea una herramienta de dibujo generativo basada en un sistema de péndulo jerárquico (tipo móvil articulado). Cada vez que haces clic y arrastras con el mouse, se traza una ruta, y sobre esa ruta se anima un péndulo (con varios segmentos), que va dejando un trazo visual con su último segmento.
```
https://editor.p5js.org/Galigali26/sketches/mH-Dqj7dU
```


Cambié el color de las líneas del péndulo a rojo
Ubicado en la función Pendulum.prototype.draw:

stroke(0, 10); // color tenue (gris oscuro)

stroke(0, 100, 100)

Este valor HSB representa:
Hue = 0 (rojo)
Saturation = 100 (saturación completa)
Brightness = 100 (máxima luminosidad)

Cambié el color de los nodos (elipses) a verde
También en Pendulum.prototype.draw, modifiqué el relleno del nodo:


fill(0); // probablemente negro

fill(120, 100, 100); // verde brillante en modo HSB
Hue = 120 (verde puro)

Saturation = 100, Brightness = 100

También aumenté el tamaño de la elipse de 4x4 a 6x6 para que los nodos se noten más:
ellipse(this.end.x, this.end.y, 6, 6);

