# _**Sistema de Incendio con Arduino.**_

## **Componentes necesarios:**
*Arduino UNO

*Sensor de temperatura

*Control remoto IR (Infrarrojo)

*Display LCD (16x2 caracteres)

*Servo motor

*Cables y resistencias según sea necesario

*Protoboard para realizar las conexiones

*Dos leds.

---

##  **Codigo Arduino.**

### **Incluimos bibliotecas**

`#include <LiquidCrystal.h>`

`#include <Servo.h>`

`#include <IRremote.h>`

---


### **Definimos componentes.**

>(Ejemplos de algunos)

`#define SERVO 3`

`#define LED 13 `

---

### **Inicializamos en el setup( ) los componentes.**



```c++
void setup()
{
  Lcd.begin(16,2);
  Servo1.attach(3, 200, 2500);
  pinMode(12, OUTPUT);
  pinMode(13, OUTPUT);
  IrReceiver.begin(IR, DISABLE_LED_FEEDBACK); 
}
```

---

### **Definimos rangos de temperatura.**

>(Ejemplo de Primavera)

```C++
else if(temperaturaMap > 15 && temperaturaMap < 30)
{
  mostrarInformacion("Estacion:Primavera", temperaturaMap);
  encenderLED(13);
  apagarLED(12);
}
```

---

### **Configuramos control remoto para que active Sistema de Incendio.**

>(Ejemplo en el boton 1 se activa sistema de incendio en verano)

```c++
   if (IrReceiver.decode())
   {
       if (IrReceiver.decodedIRData.decodedRawData == Tecla_1)
       {
         mostrarMensaje("Sist Verano","Activado");
         
         if (temperaturaMap < 60)
         {
            mostrarMensaje("Normal","Funcionamiento");
            encenderLED(13);
            apagarLED(12);
            Servo1.write(0);
         }
         else if(temperaturaMap >= 60)
         {
          mostrarMensaje("ALERTA","INCENDIO");
            encenderLED(12);
            apagarLED(13);
            Servo1.write(160);
         }
        
```

---
### **Funcion para prender y apagar los leds.**

```c++
void encenderLED(int pin)
{
  digitalWrite(pin, HIGH);    
  
}

void apagarLED(int pin)
{
  digitalWrite(pin, LOW);    
  
} 
```

---

### **Funcion para mostrar temperatura en el Display.**

>(Mediante esta funcion mostramos la estacion en la que estamos y la temperatura ambiente)

```c++
void mostrarInformacion(char mensaje[],int temperaturaMap)
{
  Lcd.print(mensaje);
  Lcd.setCursor(0,1);
  Lcd.print(temperaturaMap);
  delay(1000);
  Lcd.clear();
}
```
---


### **Funcion para mostrar cualquier mensaje en el  Display.**

```c++
void mostrarMensaje(char mensaje[],char mensajeDos[])
{
  Lcd.print(mensaje);
  Lcd.setCursor(0,1);
  Lcd.print(mensajeDos);
  delay(1000);
  Lcd.clear();
}
```
---

## **Link al Proyecto en Tinkercad.**

[Proyecto.](https://www.tinkercad.com/things/dNU8B6mRc5Z-tp/editel)








