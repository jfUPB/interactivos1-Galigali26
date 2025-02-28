Este código funciona como una pequeña máquina de estados que hace parpadear los LEDs del micro:bit de manera controlada. Cada píxel tiene dos momentos clave: cuando se inicializa (Init) y cuando está esperando que pase el tiempo para cambiar de estado (WaitTimeout).

Mientras el programa corre, cada píxel revisa constantemente si ha pasado el tiempo suficiente para encenderse o apagarse. Si es así, cambia su estado y reinicia el temporizador. Todo esto ocurre de forma independiente para cada píxel, lo que permite que tengan distintos tiempos de parpadeo sin interferir entre sí.

Es una forma eficiente de manejar animaciones en la matriz LED del micro:bit sin usar retardos (sleep()), lo que deja la puerta abierta a seguir agregando más comportamientos en el futuro. Si quisieras hacer que varios LEDs parpadeen a diferentes ritmos o agregar nuevos efectos, este código te da una buena base para lograrlo. 
