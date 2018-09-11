# SemaforoInteligente
***
## indice 
+ [descripcion del programa](#descripcion)
+ [circuito en digital](#circuito)    
+ [codigo en arduino](#codigo)
+ [Evidencia](#Evidencia)
+ [conclusión](#conclusión)
***
## Descripcion   
Sistema alertizador salvaguarda humano-coche;

Realizar un sistema que simule un semáforo interactivo usando Arduino. Este debe mostrar un conjunto de semáforos que cambiarán de verde a ámbar, rojo, y viceversa, luego de un periodo de tiempo establecido, utilizando el sistema de cuatro estados de los semáforos en México. Este se extiende para incluir un conjunto de luces y un botón peatonal para solicitar cruzar la calle. Cuando llega el peatón y se dispone a cruzar pulsa el botón que encuentra en la parte baja del semáforo, este reconoce la orden y cierra el paso de los vehículos para que el viandante pueda cruzar con seguridad hasta el otro lado de la calle. Una vez que se acaba el tiempo estipulado para que el peatón cruce, ese semáforo permanecerá abierto para mejorar la movilidad de los vehículos. El sistema deberá contener una perilla para controlar el tiempo mínimo en que el semáforo vehicular va a durar en verde.

Material utilizado:

•	5 LEDS (2 verdes, 1 amarillo, 2 rojos);
•	1 Potenciómetro - (10K);
•	6 resistores delimitadores de 220 Ω;
•	1 push boton;
•	1 protoboard;
•	Arduino.

***
## circuito 
![circuito](/Diagrama.png)
***
## codigo 
~~~
/*  En esta práctica se desarrollará un semaforo el cuál consta de 5 leds los cuáles, 3 representan al semaforo de los carros
y 2 al semaforo de peatones. Cuando el semaforo de los carros esté en verde, el de peatones estará en rojo y viceversa. También
cuénta con un botón para que los peatones puedan pedir el paso. Y también se incluye un potenciometro para medir los tiempos de 
el semaforo.
 
Autor: Oscar Iván Pacheco Vargas */
 
// Leds del semaforo para los autos
const int verde = 13;       
const int amarillo = 12;       
const int rojo = 11;        

//Leds para el semaforo de los peatones
const int p_Verde = 9;       
const int p_Rojo = 8;        

//boton para los peatones
const int boton = 7; 
       
const int pot=A0;           //Potenciometro con el que se medirá los tiempos del semaforo
int espera=0;               //Variable para checar el tiempo 

void setup() {                      
  pinMode(boton, INPUT);            //De este pin se recibirá la señal emitida por el boton
  pinMode(p_Verde, OUTPUT);         //Este pin mandará la señal para prender el led verde de peatones
  pinMode(p_Rojo, OUTPUT);          //Este pin mandará la señal para prender el led rojo de peatones
  pinMode(rojo, OUTPUT);            //Este pin mandará la señal para prender el led rojo de los autos
  pinMode(amarillo, OUTPUT);        //Este pin mandará la señal para prender el led amarillo de los autos
  pinMode(verde, OUTPUT);           //Este pin mandará la señal para prender el led verde de los autos
  
  digitalWrite(verde, HIGH);        //Inicia el proceso del semaforo de autos prendiedo el led verde indicando que los autos estan pasando
  digitalWrite(p_Rojo, HIGH);        //Enciende el led rojo de los peatones que indica que no deben pasar 
  Serial.begin(9600);               //Abre el puerto serial a una velocidad de comunicacion de 9600 baudios

}

void loop() {
  int val=0;                              //Inicializa el botón en 0 cuando se presiona 
  int valor=0;                            //Inicializa el valor del potenciometro
 val=digitalRead(boton);                  //Indica que el boton emitirá un pulso digital
 valor=(analogRead(pot)*10);              //Indica la cantidad que va mandar el potenciometro de manera analogica

 
  if (val == HIGH && espera==0) {           // Si el botón es presionado y está con valor de cero, inicia el proceso
      espera==1;                            // del semáforo que se explica a continuación:
      digitalWrite(verde, LOW);             // El led del semaforo verde se apaga
      digitalWrite(amarillo, HIGH);         // El led del samáforo amarillo se enciende
     delay(valor);                          // Indica el tiempo de espera dado por el potenciometro

      digitalWrite(amarillo, LOW);          // El led del semaforo amarillo se apaga para dar paso a los peatones
      digitalWrite(rojo, HIGH);             // El led del semaforo rojo se enciende indicando que los autos deben detenerse
      digitalWrite(p_Rojo, LOW);            // El led rojo de los peatones se apaga
      digitalWrite(p_Verde, HIGH);          // El led verde de los peatones se enciende indicando que pueden pasar
      delay(valor);                         // Indica el tiempo en que estaran pasando los peatones 
      }

      //realiza lo mismo explicado anteriormente 
      digitalWrite(p_Verde, LOW);        
      digitalWrite(p_Rojo, HIGH);         
      digitalWrite(rojo, LOW);          
      digitalWrite(verde, HIGH);        
      delay(valor);                
          
      espera=0;                           //Variable para reiniciar el proceso de ambos semaforos
  }

~~~

## Evidencia

![Evidencia](/Img1.jpg)
![Evidencia](/Img2.jpg)
![Evidencia](/Img3.jpg)



## conclusión
~~~

Con la ayuda de arduino pudimos desarrollar un prototipo de semáforo vehicular 
y peatonal el cual se basa en un lenguaje de alto nivel muy sencillo de utilizar 
para los que tenemos conocimiento en programación, y que nos permiten implementar 
la funcionalidad en base a las necesidades que ocupemos. Al tener nuestro código 
que ocupamos para nuestro semáforo, únicamente conectamos los componentes necesarios 
al protoboard y observamos que funciona correctamente.  

~~~
