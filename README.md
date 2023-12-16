# Practica-No.4-ESP32-con-ULTRASONICO-y-LCD
Dentro de este repositorio se muestra la manera de programar una ESP32 con el sensor **ULTRASÓNICO** y además, que los datos obtenidos se muestren en una pantalla LCD, así como información personal.
## Introducción
### Descripción
La **ESP32** se utiliza en un entorno de adquisición de datos, por lo cual en esta práctica utilizaremos un sensor **ULTRASÓNICO** para obtener el registro de distancia hacia un objeto o superficie. Dichos registro será mostrado de manera visual en una pantalla LCD. Posterior a ser mostrado el dato de la distancia, se conseguirá observar en la misma pantalla, mi nombre y mi carrera. Para esta practica se hace uso de un simulador llamado [WOKWI](https://wokwi.com/projects/new/esp32).
## Material necesario
Para realizar esta práctica necesitas lo siguiente

- [WOKWI](https://wokwi.com/projects/new/esp32)
- Tarjeta ESP32
- Sensor ULTRASONICO
- LCD 16x2 (I2C)
## Instrucciones
### Requisitos previos
Para poder hacer uso de este repositorio se requiere entrar a la plataforma de [WOKWI](https://wokwi.com/projects/new/esp32).
### Instrucciones de preparación del entorno
1. Abrir la terminal de programación y colocar el siguiente código:

```
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4

LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

const int Trigger = 4;   //Pin digital 2 para el Trigger del sensor
const int Echo = 15;   //Pin digital 3 para el Echo del sensor

void setup() {
  Serial.begin(9600);//iniciailzamos la comunicación
  pinMode(Trigger, OUTPUT); //pin como salida
  pinMode(Echo, INPUT);  //pin como entrada
  digitalWrite(Trigger, LOW);//Inicializamos el pin con 0
  lcd.init();
  lcd.backlight();
}

void loop()
{

  long t; //timepo que demora en llegar el eco
  long d; //distancia en centimetros

  digitalWrite(Trigger, HIGH);
  delayMicroseconds(10);          //Enviamos un pulso de 10us
  digitalWrite(Trigger, LOW);
  
  t = pulseIn(Echo, HIGH); //obtenemos el ancho del pulso
  d = t/59;             //escalamos el tiempo a una distancia en cm
  
  Serial.print("Distancia: ");
  Serial.print(d);      //Enviamos serialmente el valor de la distancia
  Serial.print("cm");
  Serial.println();

  lcd.clear();
  lcd.setCursor(0,0);
  lcd.print("Distancia: " + String(d) + "cm");
  delay(2000);
  lcd.clear();
  lcd.setCursor(0,0);
  lcd.print("Ing. Abraham");
  lcd.setCursor(0,1);
  lcd.print("Ing. Mecanica");
  delay(2000);          //Hacemos una pausa de 100ms
}
```
2. Instalar la libreria de **LiquidCrystal I2C** como se muestra en la siguiente imagen
![](https://github.com/AbrahamCH1/Practica-No.3-DHT-con-LCD/blob/main/Captura%20de%20pantalla%20(296).png?raw=true)

3. Hacer la conexion de **ULTRASONICO** y **LCD 16x2 (I2C)** con la **ESP32** como se muestra en la siguente imagen.
![](https://github.com/AbrahamCH1/Practica-No.4-ESP32-con-ULTRASONICO/blob/main/Captura%20de%20pantalla%20(299).png?raw=true)

### Instrucciones de operación
1. Iniciar simulador.
2. Visualizar el dato de la distancia en el monitor serial.
3. Visualizar el dato de la distancia en la pantalla LCD.
4. Visualizar el dato Ing. Abraham e Ing. Mecanica en la pantalla LCD.
5. Colocar la distancia dando *doble click* al sensor **ULTRASONICO** 
## Resultados
Cuando haya funcionado, se podrán observar los valores dentro de la pantalla LCD.
![](https://github.com/AbrahamCH1/Practica-No.4-ESP32-con-ULTRASONICO/blob/main/Captura%20de%20pantalla%20(300).png?raw=true)
![]()

# Créditos
Desarrollado por Ing. Abraham Contreras Herrera
[GITHUB](https://github.com/AbrahamCH1)
