Proceso de Prueba y Depuración de la Bomba

1. Introducción

Para asegurarnos de que la bomba funciona de manera confiable en diferentes situaciones, hemos realizado una serie de pruebas detalladas. En este documento, te contamos cómo probamos el sistema, qué problemas encontramos y cómo los solucionamos para mejorar su desempeño.
2. Casos de Prueba

A continuación, presentamos cinco pruebas clave que realizamos, con sus resultados esperados y lo que realmente sucedió.

3. Errores Encontrados y Soluciones Implementadas

Problema 1: La alarma no se activaba con presión alta

¿Qué pasaba? Si la presión superaba los 100 PSI, la alarma no se encendía.

¿Por qué ocurría? El código no tenía bien definida la condición para activar la alarma.

¿Cómo lo arreglamos? Ajustamos la lógica para que la alarma se active correctamente cuando la presión sea mayor a 100 PSI.

Problema 2: No detectaba cuando el sensor estaba desconectado

¿Qué pasaba? Si el sensor fallaba o no enviaba datos, el sistema no reaccionaba.

¿Por qué ocurría? No había una validación para detectar valores nulos o fuera de rango.

¿Cómo lo arreglamos? Agregamos una verificación que detecta si el sensor está desconectado y enciende la alarma.
4. Código Final Corregido

```PYTHON
const int sensorPin = A0;
const int bombaPin = 9;
const int alarmaPin = 10;

void setup() {
    pinMode(bombaPin, OUTPUT);
    pinMode(alarmaPin, OUTPUT);
    Serial.begin(9600);
}

void loop() {
    int lectura = analogRead(sensorPin);
    float presion = map(lectura, 0, 1023, 0, 150);  // Convertir a PSI

    if (lectura == 0) {  // Detección de sensor desconectado
        Serial.println("Error: Sensor desconectado");
        digitalWrite(alarmaPin, HIGH);
    } else if (presion > 100) {
        digitalWrite(alarmaPin, HIGH);
        Serial.println("¡Alarma! Presión alta");
    } else {
        digitalWrite(alarmaPin, LOW);
    }

    if (presion >= 40 && presion <= 100) {
        digitalWrite(bombaPin, HIGH);
        Serial.println("Bomba activada");
    } else {
        digitalWrite(bombaPin, LOW);
    }
    
    delay(1000);
}

```
5. Conclusión

Después de realizar estas pruebas y correcciones, ahora la bomba responde mejor a diferentes condiciones de presión y detecta fallos del sensor. Con estas mejoras, el sistema es más seguro y confiable en su funcionamiento.


