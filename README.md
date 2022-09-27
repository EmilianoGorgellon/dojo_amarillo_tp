# Proyecto: Sistema que mida temperatura en camara frigorifica.
![Tinkercad](./img/proyecto.png)

## Integrantes 
- Maximiliano Gomez
- Guido Gabriel Pascucci
- Martin Virun
- Ricardo Gonzalez
- Geronimo Camacho
- Emiliano Gorgellon

## Descripción
La funcion de este codigo, es informar al usuario el nivel, un numero exacto y atraves de los leds representamos un indicio de la temperatura dentro
solucionando todas las preguntas sobre la temperatura dentro de la cámara frigorífica.
Se agrego la funcionalidad de una tecla que en caso de estar prendida permite la funcion de los leds y display pero en caso de estar apagada no funcionaria.

## Función principal
Esta funcion se encarga de encender los leds y display segun la temperatura del sensor.
SENSOR_TEMPERATURA es un #define que utilizamos para leer los valores del sensor de temperatura asociado al pin de arduino. La funcion map permite que los valores del sensor pasarlos a grado celcius.


~~~ c (lenguaje en el que esta escrito)
#define A 12
#define B 13
#define C 7
#define D 8
#define E 9
#define F 11
#define G 10
#define AZUL 2
#define ROJO 3
#define VERDE 4
#define SENSOR_TEMPERATURA A0
#define POTENCIOMETRO A1


int lecturaAnalogica=0;
int temperatura = 0;
int valor_potenciometro = 0;
int switchA1 = 0;


void setup()
{
  Serial.begin(9600);
  pinMode(7, OUTPUT);
  pinMode(8, OUTPUT);
  pinMode(9, OUTPUT);
  pinMode(10, OUTPUT);
  pinMode(11, OUTPUT);
  pinMode(12, OUTPUT);
  pinMode(13, OUTPUT);
  pinMode(2, OUTPUT);
  pinMode(3, OUTPUT);
  pinMode(4, OUTPUT);
  pinMode(A1, INPUT);
}

void loop()
{
  valor_potenciometro = analogRead(A0);
  lecturaAnalogica = analogRead(SENSOR_TEMPERATURA);
  temperatura= map(lecturaAnalogica,20,358, -40, 125);
  Serial.print("La temperatura es : ");
  Serial.print(temperatura);
  Serial.println(" grados");
  switchA1 = digitalRead(A1);
  
  if(switchA1 == 0){
  	if(temperatura>24){
      printDigit('c');
      prenderLedRojo();
  	} 
  	else if(temperatura<0){
      printDigit('f');
      prenderLedAzul();
  	}
  	else
  	{
      printDigit('d');
      prenderLedVerde();
  	}
  	} else {
      apagarDisplay();
      apagarLeds();
  	}
}

void printDigit(char valor)
{
  apagarDisplay();
  
  switch (valor)
  {
  	case 'c':
  	{
        digitalWrite(A, HIGH);
 	    digitalWrite(D, HIGH);
        digitalWrite(E, HIGH);
        digitalWrite(F, HIGH);
      	break;
  	}
    case 'f':
  	{
        digitalWrite(A, HIGH);
        digitalWrite(E, HIGH);
        digitalWrite(F, HIGH);
        digitalWrite(G, HIGH);
      	
      	break;
  	}
  
    case 'd':
      digitalWrite(B, HIGH);
   	  digitalWrite(C, HIGH);
      digitalWrite(D, HIGH);
      digitalWrite(E, HIGH);
      digitalWrite(G, HIGH);
      break;
  }

}

void prenderLedRojo(){
  apagarLeds();
  digitalWrite(ROJO, HIGH);
}

void prenderLedAzul(){
  apagarLeds();
  digitalWrite(AZUL, HIGH);
}

void prenderLedVerde(){
  apagarLeds();
  digitalWrite(VERDE, HIGH);
}

void apagarLeds(){
  digitalWrite(AZUL, LOW);
  digitalWrite(ROJO, LOW);
  digitalWrite(VERDE, LOW);
}

void apagarDisplay(){
  digitalWrite(A, LOW);
  digitalWrite(B, LOW);
  digitalWrite(C, LOW);
  digitalWrite(D, LOW);
  digitalWrite(E, LOW);
  digitalWrite(F, LOW);
  digitalWrite(G, LOW);
}

~~~

## :robot: Link al proyecto
- [proyecto](https://www.tinkercad.com/things/0U31T13dKQe-copy-of-empresa-frigorifica/editel?sharecode=Cw90pNXzL8RvYcMZEbBVsAhTxGaJD3d-tG8ycUFVjGc)
## :tv: Link al video del proceso
- [video](https://www.youtube.com/watch?v=CsbndeN2B_U)

---
