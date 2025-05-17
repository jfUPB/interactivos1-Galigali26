Vector de prueba-	Descripción	-Resultado esperado
['A', 'B', 'A', 'Shake']	-Secuencia correcta completa (ideal)-	Regresa a CONFIGURACION, contador reseteado, display "Config"
['A', 'B', 'A']-	Secuencia incompleta-	Sigue en ARMADO, espera inputs
['A', 'B', 'Shake', 'A']	- Secuencia incorrecta (orden equivocado)-	Reinicia secuenciaActual (vacía)
['B', 'A', 'A', 'Shake']-	Secuencia incorrecta -	Reinicia secuenciaActual (vacía)
['Shake']	- Solo un shake	- Añade 'Shake' a secuenciaActual
Secuencia vacía -	Sin inputs recibidos -	Estado CONFIGURACION, contador intacto
Secuencia larga con extras	- ['A', 'B', 'A', 'Shake', 'A'] (más elementos) -	Reinicia secuenciaActual (vacía)
