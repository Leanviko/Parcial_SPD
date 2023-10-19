# Parcial SPD 
![Tinkercad](./imagenes/Parcial domiciliario_SPD_Parte1.png)


## Alumno 
- Leandro Gómez Antúnez 


## Parte 1: Contador de 0 a 99 con Display 7 Segmentos y Multiplexación 
![](imagenes/Parcial_SPD_Parte1.png)


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
- [Parte 1](https://www.tinkercad.com/things/8Xpm7Flfr3n-parcial-domiciliario-spd-parte-1/editel?sharecode=JVViB7MPuhPJMNZZktFDwT3zRe2Ar468ZiNAzWNvGbU)

---

## Parte 2: Modificación con Interruptor Deslizante y Números Primos 
![](imagenes/Parcial_domiciliario_SPD_Parte_2.png)


## Descripción
Luego del contador se añadió un interruptor deslizante que permite seleccionar entre dos modos del contador. Hacia la derecha el contador funicionara de la misma manera que en funionaba en la primera parte, deslizando hacia la izquierda el contador solo mostrará los numeros que sean primos. Los 3 botones siguen con la función asignada en un principio.

Luego fué agregado un sensor de temperatura que mostrará através del monitor la temperatura. La razón de no utilizar los displays es que el sensor mide hasta los 125 ºC por lo que era necesario un tercer display. 

## Función primo()
Esta funcion se encarga de determinar si el numero de contador es un numero primo. La funcion recibe el valor del contador como parametro. El valor entra en un bucle for que evaluea si existe otro valor por el que sea divisible aparte de si mismo, en ese caso retornará False. Como caso especial el valor 1 lo descarta como primo aunque cumpla las condiciones. Si se completa el bucle la función devuelve True confirmando que es un valor primo.


```cpp
bool primo( int n){
  if (n==1){
  	return(false);
  }else{
  	for ( int i = 2 ; i <n ; i++){
      if (n % i == 0){ 
        return(false);
      }
    }
  }
  return (true);
}
```

## :robot: Link al proyecto
- [Parte 2](https://www.tinkercad.com/things/bMhXdcsKlZr-parcial-domiciliario-spd-parte-2/editel?sharecode=QUtv5LL5CogbioIICBzB4xI_E0JsPRDQnt_gh3dl7Ds)
