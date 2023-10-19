# Parcial SPD 
![Tinkercad](./img/ArduinoTinkercad.jpg)


## Alumno 
- Leandro Gómez Antúnez 


## Parte 1: Contador de 0 a 99 con Display 7 Segmentos y Multiplexación 
![Tinkercad](./img/ContadorBinario.png)


## Descripción
En esta parte del proyecto se diseño un contador de 0 a 99 utilizando 2 displays de 7 segmentos. El contador utiliza 3 botones para controlar su funcionamiento: 1 para contar de forma creciente, 1 para contar de forma decreciente y 1 para reiniciar la cuenta a 0.  Para optimizar la cantidad de pines de la placa arduino se utilizó la tecnica de multiplexacion con cátodo común.

## Función principal
Esta parte del codigo se encarga de sumar, restar o resetear el contador dependiendo del pulsador que accionemos. Se aplicó un pequeño delay utilizando la función millis() para evitar el efecto rebote del pulsador. Tambien hace uso de Serial.print() para controlar que los valores sean los esperados. Una vez determinado el numero a mostrar el valor del contador se pasa a la funcion llamada "alternarLeds()" que se encarga de mostrar en los displays el valor, ademas de alternar el encendido de cada uno debido al uso de la multiplexacion.

```cpp
//Pulsadores--------------------
  	puls_suma = digitalRead(pulsador_suma);  //lectura digital de pin
	puls_resta = digitalRead(pulsador_resta);
  	puls_reset = digitalRead(pulsador_reset);
  
  
  if (puls_suma && (millis()-tiempo > antirrebote)) {
    contador++;
    tiempo = millis();
  	Serial.println(contador);
  }else if (puls_resta && (millis()-tiempo > antirrebote)) {
    contador--;
    tiempo = millis();
  	Serial.println(contador);	
  }else if (puls_reset && (millis()-tiempo > antirrebote)) {
    	contador = 0;
    tiempo = millis();
    Serial.println(contador);
  }
  
  if(contador > 99){
    contador = 0;
  }else if(contador < 0){
    contador = 99;
  }
  
  
  alternarLeds(contador);
```

## :robot: Link al proyecto
- [proyecto](https://www.tinkercad.com/things/8Xpm7Flfr3n-parcial-domiciliario-spd-parte-1/editel?sharecode=JVViB7MPuhPJMNZZktFDwT3zRe2Ar468ZiNAzWNvGbU)
