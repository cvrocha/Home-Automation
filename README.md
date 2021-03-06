<h1 align="center"><img width="100px" src="https://user-images.githubusercontent.com/62439381/159342255-1f96b7cb-5f67-4090-b00d-b89f4d7a1dc4.png">&nbsp;Automação residencial <img width="100px" src="https://user-images.githubusercontent.com/62439381/159342255-1f96b7cb-5f67-4090-b00d-b89f4d7a1dc4.png">&nbsp;</h1>

O objetivo principal deste projeto é desenvolver um sistema de automação residencial utilizando uma placa Arduino com Bluetooth sendo controlado remotamente por qualquer smartphone com sistema operacional Android.

<br>

Para isso, um módulo Bluetooth é interfaceado com a placa Arduino na extremidade do receptor enquanto na extremidade do transmissor, uma aplicação GUI no telefone celular envia comandos ON/OFF para o receptor onde as cargas estão conectadas. Ao tocar no local especificado na GUI, as cargas podem ser LIGADAS/DESLIGADAS remotamente através desta tecnologia.

# 

A demonstração do projeto está no vídeo e imagens **_abaixo_:**

<div align="center">
 <a href="https://www.youtube.com/embed/eDQ6t2ftBEQ"><img width="96%" src="https://user-images.githubusercontent.com/62439381/159349548-c4c37f3f-2028-4c67-a2db-5a47f2f92176.png"></a>
<a href="https://www.youtube.com/embed/eDQ6t2ftBEQ"><img src="https://user-images.githubusercontent.com/62439381/159343227-2a1df231-4b02-460c-a880-551482443406.jpeg" width="96%"/></a>
<a href="https://www.youtube.com/embed/eDQ6t2ftBEQ"><img src="https://user-images.githubusercontent.com/62439381/159343162-4388a896-3463-4bd5-9d41-b9bf375025dc.jpeg" width="96%"/></a>
 </div>
</div> 

<div align="center">
  <div style="display: flex; align-items: flex-start;">
<a href="https://www.youtube.com/embed/eDQ6t2ftBEQ"><img src="https://user-images.githubusercontent.com/62439381/159343290-384b11ba-4297-4a48-b190-1ee8dd70d0a4.jpg" width="48%"/></a>
<a href="https://www.youtube.com/embed/eDQ6t2ftBEQ"><img src="https://user-images.githubusercontent.com/62439381/159343358-0a99ee42-5f1a-4ba9-b653-3cdcb3b24b97.jpg" width="48%"/></a>
  </div>
</div>

# Conteúdo

Este Readme está dividido em várias partes
1. [Descrição](#descrição)
2. [Componentes](#components)
3. [Implementação](#implementação)


<a name="descrição">Descrição</a>
---------
Este projeto é um dos mais importantes <a href = "https://www.projectsof8051.com/arduino-projects/">Arduino Projects</a>. A automação residencial baseada em arduino usando o projeto Bluetooth ajuda o usuário a controlar qualquer dispositivo eletrônico usando o aplicativo Device Control em seu Smartphone Android. O aplicativo android envia comandos para o controlador – Arduino, por meio de comunicação sem fio, ou seja, Bluetooth. O Arduino está conectado à placa principal que possui cinco relés, conforme mostrado no diagrama de blocos. Esses relés podem ser conectados a diferentes dispositivos eletrônicos como luzes, televisão, ventilador, etc.
Quando o usuário pressiona o botão 'On' exibido no aplicativo para o dispositivo 1, a campainha é ligada. Este Buzzer pode ser desligado, pressionando o mesmo botão novamente.
Da mesma forma, quando o usuário pressiona o botão ‘On’ exibido no aplicativo para o dispositivo 2, o ventilador é ligado. O ventilador pode ser desligado, pressionando novamente o mesmo botão.
Este projeto de automação residencial usando Bluetooth e Arduino pode ser usado para controlar qualquer dispositivo AC ou DC.
Dado abaixo é o diagrama de fluxo que explica o fluxo do projeto.

<div align="center">
 <div>
 <a href="https://www.youtube.com/embed/eDQ6t2ftBEQ"> <img src = "https://github.com/aagarwal1012/Home-Automation/blob/master/Images/diagram.jpg" width = "96%"/> </a>
 </div>
</div> 


<a name="components">Componentes</a>
---------
Esta seção lista vários componentes de hardware e software usados no projeto.

#### Hardware
A lista de componentes mencionados aqui são especificamente para controlar 4 cargas diferentes.

- Arduino UNO
- HC – 05 Bluetooth Modulo
- 5 V Relay X 4
- Proto board
- Fios de conexão (Jump, Jumper)
- Smartphone ou tablet (Bluetooth ativado)
- 9V Fonte de energia

#### Software

- Arduino 1.8.5 compiler
- [Android application](#app)



<a name="implementação">Implementação</a>
---------
### Diagrama de circuito

<div align="center">
 <div>
 <a href="https://www.youtube.com/embed/eDQ6t2ftBEQ"> <img src = "https://github.com/aagarwal1012/Home-Automation/blob/master/Images/ciruit_diagram.png" width = "96%"/> </a>
 </div>
</div> 


### Código Arduino

```
//Arduino uno
//by: Caio Rocha and Lucas Feitosa
 
#include <SPI.h>
#include <Ethernet.h>
#include <SoftwareSerial.h>

SoftwareSerial bluetooth(10, 11);
String readString;
 
int pino_rele1 = 3;
int pino_rele2 = 4;
int pino_rele3 = 5;
int pino_rele4 = 6;
boolean ligado = true;
boolean ligado_2 = true;
int incomingByte; 

void setup()
{
  Serial.begin(9600);
  bluetooth.begin(9600);
  pinMode(pino_rele1, OUTPUT);
  pinMode(pino_rele2, OUTPUT);
  pinMode(pino_rele3, OUTPUT);
  pinMode(pino_rele4, OUTPUT);
}
 
void loop()
{
  //Serial.println("LOOP");
  if (bluetooth.available() > 0) 
  {
    // read the oldest byte in the serial buffer:
    incomingByte = bluetooth.read();
    Serial.println(incomingByte);
    Serial.println("");
    // if it's a capital H (ASCII 72), turn on the LED:
    if (incomingByte == 49) 
    {
      digitalWrite(pino_rele1, LOW);
      bluetooth.println("LAMPADA 1: ON");
       
    }
    // if it's an L (ASCII 76) turn off the LED:
    if (incomingByte == 65) 
    {

     digitalWrite(pino_rele1, HIGH);
      bluetooth.println("LAMPADA 1: OFF");
      
    }
    if (incomingByte == 50) 
    {
      digitalWrite(pino_rele2, LOW);
      bluetooth.println("LAMPADA 2: ON");
       
    }
    // if it's an L (ASCII 76) turn off the LED:
    if (incomingByte == 66) 
    {

     digitalWrite(pino_rele2, HIGH);
      bluetooth.println("LAMPADA 2: OFF");
      
    }
    if (incomingByte == 51) 
    {
      digitalWrite(pino_rele3, LOW);
      bluetooth.println("LAMPADA 3: ON");
      
    }
    // if it's an L (ASCII 76) turn off the LED:
    if (incomingByte == 67) 
    {

     digitalWrite(pino_rele3, HIGH);
      bluetooth.println("LAMPADA 3: OFF");
      
    }
    if (incomingByte == 52) 
    {
      digitalWrite(pino_rele4, LOW);
      bluetooth.println("LAMPADA 4: ON");
       
    }
    // if it's an L (ASCII 76) turn off the LED:
    if (incomingByte == 68) 
    {

     digitalWrite(pino_rele4, HIGH);
      bluetooth.println("LAMPADA 4: OFF");
     
    }
    if (incomingByte == 57) 
    {

     digitalWrite(pino_rele1, LOW);
     digitalWrite(pino_rele2, LOW);
     digitalWrite(pino_rele3, LOW);
     digitalWrite(pino_rele4, LOW);
      bluetooth.println("TODAS AS LAMPADAS: ON");
     
    }

    if (incomingByte == 73) 
    {
      digitalWrite(pino_rele1, HIGH);
      digitalWrite(pino_rele2, HIGH);
      digitalWrite(pino_rele3, HIGH);
     digitalWrite(pino_rele4, HIGH);
      bluetooth.println("TODAS AS LAMPADAS: OFF");
     
    }
  
  } 
}
```


### Android App  

<div align="center">
 <div>
 <a href="https://www.youtube.com/embed/eDQ6t2ftBEQ"> <img src = "https://github.com/aagarwal1012/Home-Automation/blob/master/Images/app_screenshot.png" width = "35%"/>  </a>
 </div>
</div> 


Qualquer sugestão é bem-vinda e sinta-se à vontade para abrir um problema.
