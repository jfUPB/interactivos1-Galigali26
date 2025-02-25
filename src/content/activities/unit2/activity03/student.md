### Entradas
Botón A , Botón B, Acelerómetro, Micrófono, Sensor Táctil en el logo

Detecta si el botón A está siendo presionado =button_a.is_pressed()
Devuelve el nivel de sonido ambiente en una escala de 0 a 255 = microphone.sound_level()
Detecta si el logo capacitivo del Micro:bit ha sido tocado = touch_logo.is_touched()

### Salidas
Matriz LED 5x5 ,Buzzer interno, Botón de reinicio , UART 
Muestra una imagen en la matriz LED = display.show(Image.HAPPY)
Reproduce un sonido predefinido en el buzzer interno = audio.play(Sound.HAPPY)
Envía datos por comunicación serie = uart.write("Hola")
