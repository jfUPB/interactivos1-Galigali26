![image](https://github.com/user-attachments/assets/6f87044f-d785-4510-a3c4-a717ebdd3bc7)

Enviar los datos en ascii hace mucho mas facil la lectura de los datos, si se sabe cuales son los datos que se van a enviar es mejor en binario por la compresion pero si es alguna prueba considero que es mejor el ascii, se estan enviando 6 datos cuando se hace el gesto shake

![image](https://github.com/user-attachments/assets/2a76d8cf-88a6-485d-9207-92b0f8425d30)


Cada uno tiene un numero entero que no veo que haga nada al lado de cada datos, los dos primero son la posicion en X y Y que tiene el microbit cuando se hace el gesto en shake y los otros dos son el true y false de la A y B, cuando esta en true aparece como 1, cuando intento sacar resultados negativos simplemente aparecen 00 no entiendo como se podria ver.

![image](https://github.com/user-attachments/assets/a3981d82-4f6e-4c6a-acd7-a0212be383d5)

Es mucho mas facil de leer los datos en texto pero en hex es mucho mas complejo y lanza muchisimos mas datos de los necesarios, considero que tienen usos distintos dependiendo de la utilizacion que se le vaya a dar, digamos que tanta interaccion tiene con el usario nuestro proyecto, para evitar sobrecargas del puerto serial seria mejor usar formato binario.
