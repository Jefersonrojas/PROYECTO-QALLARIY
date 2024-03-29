 <p align="center" style="margin-top: 50px; margin-bottom: 50px; font-family: Arial, sans-serif;">
  <p align="center">
    <img src="https://i.postimg.cc/pXjm2knB/Grupo-08.jpg)](https://postimg.cc/ZCTbH8H9)" width="1000" alt="logo">
  </p>  
 
   </p>  
  <h1 align="center" style="margin-top: 30px; margin-bottom: 0px;">Taller N° 03:</h1>
</p>
 </p>  
  <h1 align="center" style="margin-top: 30px; margin-bottom: 0px;">"Internet de las Cosas (IoT)"</h1>
</p>
 
## 1. Introducción 
*En este proyecto, se busca familiarizar a los participantes con la MKR IoT Carrier, componente clave del Arduino Oplà IoT Kit. A través de un programa práctico, se pretende que los usuarios comprendan los diferentes elementos de la placa, exploren la librería MKRIoTCarrier y adquieran habilidades para programar actuadores y sensores. Los objetivos incluyen la creación de una aplicación básica que demuestre todas las funciones de la MKR IoT Carrier, sirviendo como una introducción esencial antes de abordar proyectos más avanzados y como referencia para refrescar conocimientos sobre el hardware en futuras aplicaciones. Este proyecto establece una base sólida para la comprensión y aplicación efectiva de la MKR IoT Carrier en proyectos de Internet de las cosas*

### Importancia

*El Internet de las Cosas (IoT) permite recopilar y transmitir información de manera automatizada, para mejorar nuestra calidad de vida, aumentar la eficiencia y la productividad de los procesos industriales y empresariales, y reducir el impacto ambiental de nuestras actividades.*

### Lista de materiales utilizados en el laboratorio


| MATERIALES |  IMAGEN | 
| :------------ |:---------------:| 
| SENSOR PIR| [![PIR.jpg](https://i.postimg.cc/VsjYHfPs/descarga.jpg)](https://postimg.cc/QVdGFrMv)|
| Arduino MKR WIFI 1010| [![ARDUINO.jpg](https://i.postimg.cc/dQSZf2tx/descarga-9.jpg)](https://postimg.cc/hhTGz7mL) |
| Arduino MKR IoT Carrier | [![Arduino MKR IoT Carrier.jpg](https://i.postimg.cc/SQ5PB5CZ/descarga-1.jpg)](https://postimg.cc/V5q4MK7M)| 


## 2.- Ejercicios desarrollados en la práctica del laboratorio

###  EJERCICIO 1

#### CÓDIGO DEL EJERCICIO 1:

```cpp

#include <Arduino_MKRIoTCarrier.h>
MKRIoTCarrier carrier;

float temperature = 0;
float humidity = 0;

void setup() {
  Serial.begin(9600);

  //Establece si el gavinete tiene montado
  CARRIER_CASE = true;

  // Inicializa el operador IoTSK y muestra cualquier error en el monitor serie
  carrier.begin();
}
void loop() {

  // Leer los valores del sensor
  temperature = carrier.Env.readTemperature();
  humidity = carrier.Env.readHumidity();

  // Actualiza botones táctiles
  carrier.Buttons.update();

  // Imprime cada uno de los valores del sensor
  Serial.print("Temperature = ");
  Serial.print(temperature);
  Serial.println(" Â°C");
  Serial.print("Humidity = ");
  Serial.print(humidity);
  Serial.println(" %");

  //Función para imprimir valores
  if (carrier.Buttons.onTouchDown(TOUCH0)) {
    printTemperature();
  }
  if (carrier.Buttons.onTouchDown(TOUCH1)) {
    printHumidity();
  }

// IMPRIMIR TEMPERATURA
}
void printTemperature() {
  // Configurar la pantalla, configurar el color del fondo, el tamaño del texto y el color del texto
  carrier.display.fillScreen(ST77XX_RED);     // Fondo rojo
  carrier.display.setTextColor(ST77XX_WHITE); // Texto blanco 
  carrier.display.setTextSize(6);             // Tamaño del texto
  carrier.display.setCursor(30, 50);          // Establecer la posición para imprimir (x e y)
  carrier.display.print("Temp: ");
  carrier.display.setTextSize(4);             // Disminuyendo el tamaño del texto  
  carrier.display.setCursor(40, 120);         // Establece una nueva posición para imprimir (x e y)
  carrier.display.print(temperature);
  carrier.display.print(" C");
}

// IMPRIMIR HUMEDAD
void printHumidity() {
  // Configurar la pantalla, configurar el color del fondo, el tamaño del texto y el color del texto
  carrier.display.fillScreen(ST77XX_BLUE);     //  Fondo rojo
  carrier.display.setTextColor(ST77XX_WHITE);  //  Texto blanco 
  carrier.display.setTextSize(4);              // Texto de tamaño mediano
  carrier.display.setCursor(20, 110);         // Establecer la posición para imprimir (x e y)
  carrier.display.print("Humi: ");
  carrier.display.print(humidity);
  carrier.display.println(" %");
}
```

## Imagenes como prueba de los resultados del ejercicio

| Temperatura |  Humedad | 
| :------------ |:---------------:| 
| Medición de la temperatura en grados Celsius equivalente a 30.10 °C|[![temperaturaaa.jpg](https://i.postimg.cc/kX5QQfLZ/temperaturaaa.jpg)](https://postimg.cc/NLW2Y7s7) |
| Medición de la humedad en porcentaje equivalente a 61.39 %| [![humedad.jpg](https://i.postimg.cc/6QYgm7bp/humedad.jpg)](https://postimg.cc/Y4Ld4Sw5) |

## Explicación del código
•	Primero configura y establece la comunicación serial a 9600 baudios.

•	Luego inicializa la placa MKRIoTCarrier y verifica si el gabinete está montado en el bucle principal (loop)

•	Despúes lee los valores de temperatura y humedad de los sensores integrados y actualiza los botones táctiles.


• A continuación imprime los valores de temperatura y humedad en el monitor serie.

•	Si se toca el botón táctil TOUCH0, llama a la función printTemperature().

•	Si se toca el botón táctil TOUCH1, llama a la función printHumidity().

•	La función printTemperature() configura la pantalla con un fondo rojo y muestra el valor de temperatura en la pantalla con un formato específico.

•	La función printHumidity() configura la pantalla con un fondo azul y muestra el valor de humedad en la pantalla con un formato específico.




##   EJERCICIO 2


### CÓDIGO DEL EJERCICIO 2:


```cpp

#include <Arduino_MKRIoTCarrier.h>
MKRIoTCarrier carrier;
double temperature = 0;
float humidity = 0;

void setup() {
  Serial.begin(9600);
  CARRIER_CASE = true;
  carrier.begin();
}

void loop() {
  temperature = carrier.Env.readTemperature();
  humidity = carrier.Env.readHumidity();
  carrier.Buttons.update();

  Serial.print("Temperature = ");
  Serial.print(temperature);
  Serial.println(" °C");

  // Convertir a Fahrenheit y Kelvin
  double fahrenheit = (temperature * 9.0 / 5.0) + 32.0;
  double kelvin = temperature + 273.15;

  if (carrier.Buttons.onTouchDown(TOUCH0)) {
    printTemperature(temperature, "C");
  }
  if (carrier.Buttons.onTouchDown(TOUCH1)) {
    printTemperature(fahrenheit, "F");
  }
  if (carrier.Buttons.onTouchDown(TOUCH2)) {
    printTemperature(kelvin, "K");
  }
}

void printTemperature(double temp, const char *unit) {
  carrier.display.fillScreen(ST77XX_RED);
  carrier.display.setTextColor(ST77XX_WHITE);
  carrier.display.setTextSize(6);
  carrier.display.setCursor(30, 50);
  carrier.display.print("Temp: ");
  carrier.display.setTextSize(4);
  carrier.display.setCursor(40, 120);
  carrier.display.print(temp);
  carrier.display.print(" ");
  carrier.display.print(unit);
}
```

| ESCALA |  MEDIDA | 
| :------------ |:---------------:| 
| Medición en grados Celsius| [![celsius.jpg](https://i.postimg.cc/MGcYbvBB/celsius.jpg)](https://postimg.cc/qtTnpBjB) |
| Medición en grados Fahrenheit| [![Farenheit13.jpg](https://i.postimg.cc/15jBgGnS/Farenheit13.jpg)](https://postimg.cc/7fS0dTnt) |
| Medición en grados Kelvin | [![kelvin12.jpg](https://i.postimg.cc/dt2dFG2n/kelvin12.jpg)](https://postimg.cc/zVf3SbPR)| 


## CAMBIO DE TEMPERATURAS

https://github.com/Jefersonrojas/PROYECTO-QALLARIY/assets/150811988/378dc1f8-8c82-429d-9cbb-c114d803611e



## EXPLICACIÓN DEL CÓDIGO
### 1.INCLUSIÓN DE LA BIBLIOTECA (MKRIoTCarrier)


```cpp
#include <Arduino_MKRIoTCarrier.h>
````

### 2 DECLARACIÓN DE VARIABLES



```cpp
MKRIoTCarrier carrier;
double temperature = 0;
float humidity = 0;

````

### 3.CONFIGURACIÓN (setup)


```cpp
void setup() {
  Serial.begin(9600);
  CARRIER_CASE = true;
  carrier.begin();
}


````

### 4.FUNCIÓN DEL BUCLE (Loop)


```cpp
void loop() {
  temperature = carrier.Env.readTemperature();
  humidity = carrier.Env.readHumidity();
  carrier.Buttons.update();

  // Lecturas de temperatura y humedad
  Serial.print("Temperature = ");
  Serial.print(temperature);
  Serial.println(" °C");

  // Convertir a Fahrenheit y Kelvin
  double fahrenheit = (temperature * 9.0 / 5.0) + 32.0;
  double kelvin = temperature + 273.15;

  // Verificación de eventos de botones táctiles
  if (carrier.Buttons.onTouchDown(TOUCH0)) {
    printTemperature(temperature, "C");
  }
  if (carrier.Buttons.onTouchDown(TOUCH1)) {
    printTemperature(fahrenheit, "F");
  }
  if (carrier.Buttons.onTouchDown(TOUCH2)) {
    printTemperature(kelvin, "K");
  }
}


````

* temperature = carrier.Env.readTemperature(); y humidity = carrier.Env.readHumidity().Lee la temperatura y la humedad del entorno utilizando los sensores del portador.
* carrier.Buttons.update();.Actualiza el estado de los botones táctiles.
* Imprime la temperatura actual en grados Celsius a través de la comunicación serie y convierte la temperatura a Fahrenheit y Kelvin.
* Verifica si se ha tocado alguno de los tres botones táctiles (TOUCH0, TOUCH1, TOUCH2) y, en caso afirmativo, llama a la función printTemperature con la temperatura convertida y la unidad correspondiente

### FUNCIÓN PARA IMPRIMIR LA TEMPERATURA EN LA PANTALLA (printTemperature)


```cpp
void printTemperature(double temp, const char *unit) {
  carrier.display.fillScreen(ST77XX_RED);
  carrier.display.setTextColor(ST77XX_WHITE);
  carrier.display.setTextSize(6);
  carrier.display.setCursor(30, 50);
  carrier.display.print("Temp: ");
  carrier.display.setTextSize(4);
  carrier.display.setCursor(40, 120);
  carrier.display.print(temp);
  carrier.display.print(" ");
  carrier.display.print(unit);
}

````

* Configura la pantalla TFT para mostrar la temperatura en un formato específico. En este caso se utiliza un fondo rojo y texto blanco.

### Imagenes como prueba de los resultados del ejercicio

<p align="center">
  <img src="" alt="" width="400px" />
</p>


## EJERCICIO 3 y 4

| Explicación  |  Error  | 
| :------------ |:---------------:| 
| En este ejercicio el objetivo principal era hacer que tenga una funcion similar a la de una alarma de sensor, es decir, cada ves que sentia la percepción de un objeto o persona, este tenia que sonar automaticamente. | [![ERROR1.jpg](https://i.postimg.cc/15XLhL2H/ERROR1.jpg)](https://postimg.cc/KRX9tsZk)| [![Whats-App-Image-2024-01-23-at-2-20-01-AM.jpg](https://i.postimg.cc/Lss7b8kS/Whats-App-Image-2024-01-23-at-2-20-01-AM.jpg)](https://postimg.cc/DStBWFYp)|
|En el presente ejercicio a realizar, tenia como proposito que nuestro sensor mida la percepcion del ambiente, es decir, cuando el ambiente esta frio se encienda y dé el color rojo como indicador de un entorno frio y dé azul si el ambiente era lo contrario. Debido a imprevistos de la maquina que estaban fuera de nuestro alcanze no se pudo lograr los objetivos, puesto que la maquina con la que se trabajo necesitaba permisos y condiciones para ciertas instalaciones, se pidio ayuda a los docentes quienes nos explicaron el imprevisto de nuestra maquina, consideramos que hubiese sido una experiencia satisfactoria si se hubiese podido lograr el experimento | [![Error-2.jpg](https://i.postimg.cc/5NQnm1DZ/Error-2.jpg)](https://postimg.cc/nCZ4F8Fk)| [![Whats-App-Image-2024-01-23-at-2-20-01-AM.jpg](https://i.postimg.cc/Lss7b8kS/Whats-App-Image-2024-01-23-at-2-20-01-AM.jpg)](https://postimg.cc/DStBWFYp)|

<p align="center">
  <img src="" alt="" width="400px" />
</p>

## 3.- Conclusión
En conclusion, todo lo experimentando y aprendido, tiene como objetivo principal familiarizar a los participantes con la MKR IoT Carrier del Arduino Oplà IoT Kit. que  permite aprender y comprender el uso de los actuadores y sensores. En el presente informe se realizo para cuatro ejercicios (por problemas tecnicos solo se logro para dos ejercicios). Tales ejercicios servira como base para proyectos futuros estableciendo una base sólida para la comprensión y aplicación práctica de este componente en el ámbito del Internet de las cosas.


