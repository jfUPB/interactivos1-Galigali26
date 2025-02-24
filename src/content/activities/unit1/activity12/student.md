### Micro:bit 
``` js
from microbit import *

uart.init(baudrate=115200)

display.show(Image('00000:'
                   '33333:'
                   '55555:'
                   '77777:'
                   '99999'))

while True:
    if button_a.is_pressed():
        display.show(Image.GHOST)
        sleep(500)

    if button_b.is_pressed():
        display.show(Image.SKULL)  
        uart.write('B')
        sleep(500)

    if pin_logo.is_touched():  
        display.show(Image.SAD)  
        uart.write('T')  
        sleep(500)

    if accelerometer.was_gesture('shake'):
        display.show(Image.HAPPY)
        sleep(500)
```
