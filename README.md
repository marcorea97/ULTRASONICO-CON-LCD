# ULTRASONICO-CON-LCD
______________________
**Descripción**

En esta práctica, se realizará una medición de distancia utilizando un sensor ultrasónico. Los resultados se mostrarán en una pantalla LCD. La tarjeta ESP32 se empleará como unidad de adquisición de datos. Además, se usará un sensor DHT11 para medir la temperatura y humedad del entorno, registrando estos datos cada segundo y visualizándolos en una pantalla LCD 16x2. Toda la simulación se llevará a cabo en la plataforma WOKWI.

________________________

**Materiales necesarios**

•	Simulador WOKWI

•	Tarjeta ESP32

•	Sensor ultrasónico HC-SR04

•	Pantalla LCD 16x2 con interfaz I2C
________________________

**Requisitos previos**

1.	Instalar la biblioteca LiquidCrystal I2C según las instrucciones proporcionadas.
2.	Realizar las conexiones del sensor ultrasónico HC-SR04 y la pantalla LCD 16x2 I2C a la ESP32 de acuerdo con el esquema suministrado.
Instrucciones de operación
1.	Inicia el simulador WOKWI.
2.	Observa los datos en el monitor serial.
3.	Ajusta la distancia interactuando con el sensor ultrasónico en el simulador (doble clic sobre el HC-SR04).

_________________________________
**Instrucciones**

1.	Inserta el código proporcionado en el entorno de simulación.
2.	Realiza la misma actividad que en la práctica anterior, pero muestra también información del programador.
3.	Configura las conexiones entre el LCD, el sensor ultrasónico y la ESP32 siguiendo el diagrama proporcionado

______________________________
**Modo de conexion**

![](https://github.com/marcorea97/ULTRASONICO-CON-LCD/blob/main/ULTRASONICO%20CON%20LCD%201.png)
________________________
**Código de referencia**

const int Trigger = 4;   // Pin digital para el Trigger del sensor
const int Echo = 15;     // Pin digital para el Echo del sensor
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4

LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {
  Serial.begin(9600);              // Inicializamos la comunicación
  pinMode(Trigger, OUTPUT);        // Pin como salida
  pinMode(Echo, INPUT);            // Pin como entrada
  digitalWrite(Trigger, LOW);      // Inicializamos el pin con 0
  lcd.init();
  lcd.backlight();
}

void loop() {
  long t; // Tiempo que demora en llegar el eco
  long d; // Distancia en centímetros

  digitalWrite(Trigger, HIGH);
  delayMicroseconds(10);           // Enviamos un pulso de 10 µs
  digitalWrite(Trigger, LOW);

  t = pulseIn(Echo, HIGH);         // Obtenemos el ancho del pulso
  d = t / 59;                      // Convertimos el tiempo en distancia en cm

  Serial.print("Distancia: ");
  Serial.print(d);
  Serial.println(" cm");
  delay(2000);

  lcd.clear();
  lcd.setCursor(2, 0);
  lcd.print("DIPLOMADO V");
  lcd.setCursor(2, 1);
  lcd.print("Mecatrónica");
  delay(2000);

  lcd.clear();
  lcd.setCursor(2, 0);
  lcd.print("Victor Cabañas");
  lcd.setCursor(2, 1);
  lcd.print("Ing. Mecánica");
  delay(2000);

  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Distancia: " + String(d) + " cm");
  delay(2000);
}



______________________________

**Resultados esperados**

![](https://github.com/marcorea97/ULTRASONICO-CON-LCD/blob/main/LCD%20DIP.png)

![](https://github.com/marcorea97/ULTRASONICO-CON-LCD/blob/main/LCD%20MARCO%20REA.png)

![](https://github.com/marcorea97/ULTRASONICO-CON-LCD/blob/main/LCD%20DISTANCIA.png)



 Cuando la configuración sea correcta, podrás visualizar los comentarios añadidos en el codigo de programacion ademas de la distancia en el monitor y en la pantalla LCD.
