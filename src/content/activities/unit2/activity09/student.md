´´´´from microbit import *
import utime

class Pixel:
    def __init__(self, pixelX, pixelY, initState):
        self.pixelX = pixelX
        self.pixelY = pixelY
        self.pixelState = initState  # Estado inicial

    def encender(self):
        display.set_pixel(self.pixelX, self.pixelY, 9)  # Enciende con brillo máximo

    def apagar(self):
        display.set_pixel(self.pixelX, self.pixelY, 0)  # Apaga el LED

class Semaforo:
    def __init__(self):
        self.state = "ROJO"
        self.startTime = utime.ticks_ms()

        # Definir los LEDs de cada color en orden de arriba a abajo
        self.luz_roja = [
            Pixel(1, 0, 9), Pixel(2, 0, 9), Pixel(3, 0, 9),
            Pixel(1, 1, 9), Pixel(2, 1, 9), Pixel(3, 1, 9)
        ]
        
        self.luz_amarilla = [
            Pixel(1, 2, 0), Pixel(2, 2, 0), Pixel(3, 2, 0)
        ]
        
        self.luz_verde = [
            Pixel(1, 3, 0), Pixel(2, 3, 0), Pixel(3, 3, 0),
            Pixel(1, 4, 0), Pixel(2, 4, 0), Pixel(3, 4, 0)
        ]

        # Iniciar con la luz roja encendida
        self.encender(self.luz_roja)

    def encender(self, luces):
        for luz in luces:
            luz.encender()

    def apagar(self, luces):
        for luz in luces:
            luz.apagar()

    def update(self):
        current_time = utime.ticks_ms()

        if self.state == "ROJO":
            if utime.ticks_diff(current_time, self.startTime) > 3000:
                self.apagar(self.luz_roja)
                self.encender(self.luz_amarilla)
                self.state = "AMARILLO"
                self.startTime = utime.ticks_ms()

        elif self.state == "AMARILLO":
            if utime.ticks_diff(current_time, self.startTime) > 1500:
                self.apagar(self.luz_amarilla)
                self.encender(self.luz_verde)
                self.state = "VERDE"
                self.startTime = utime.ticks_ms()

        elif self.state == "VERDE":
            if utime.ticks_diff(current_time, self.startTime) > 3000:
                self.apagar(self.luz_verde)
                self.encender(self.luz_roja)
                self.state = "ROJO"
                self.startTime = utime.ticks_ms()

semaforo = Semaforo()

while True:
    semaforo.update()
