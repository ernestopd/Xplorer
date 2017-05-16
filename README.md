#include <Servo.h> //libreria para el servo
Servo myservo; 
int Echo = A4; 
int Trig = A5;
int in1 = 6;
int in2 = 7;
int in3 = 8;
int in4 = 9;
int ENA = 5;
int ENB = 11;
int ABS = 140;
int rightDistance = 0,leftDistance = 0,middleDistance = 0 ;


int Distance_test()   //test de distancia 
{
  digitalWrite(Trig, LOW); 
  delayMicroseconds(2);
  digitalWrite(Trig, HIGH);  //trigger manda una onda  
  delayMicroseconds(20);
  digitalWrite(Trig, LOW);   
  float Fdistance = pulseIn(Echo, HIGH);  //Echo la recibe 
  Fdistance= Fdistance/58;   //calculamos la distancia con formula    
  return (int)Fdistance;
}  

void setup() 
{ 
  myservo.attach(3);// attach servo on pin 3 to servo object
  Serial.begin(9600);     
  pinMode(Echo, INPUT);    
  pinMode(Trig, OUTPUT);  
  pinMode(in1,OUTPUT);
  pinMode(in2,OUTPUT);
  pinMode(in3,OUTPUT);
  pinMode(in4,OUTPUT);
  pinMode(ENA,OUTPUT);
  pinMode(ENB,OUTPUT);
  _mStop();
} 

void loop() 
{ 
    myservo.write(85);//posicion del servo
    delay(500); 
    middleDistance = Distance_test(); 
 

    if(middleDistance<=35) // verifica el resultado de middleDistance, resultado de Distance_test, si es menor de 35
    {     
      
       _mright();  
        delay(150);
       }
     

    else
        _mForward();                     
}

void _mForward()
{
 analogWrite(ENA,ABS);
 analogWrite(ENB,ABS);
  digitalWrite(in1,HIGH);//digital output
  digitalWrite(in2,LOW);
  digitalWrite(in3,LOW);
  digitalWrite(in4,HIGH);

}

void _mBack()
{
 analogWrite(ENA,ABS);
 analogWrite(ENB,ABS);
  digitalWrite(in1,LOW);
  digitalWrite(in2,HIGH);
  digitalWrite(in3,HIGH);
  digitalWrite(in4,LOW);

}

void _mleft()
{
 analogWrite(ENA,ABS);
 analogWrite(ENB,ABS);
  digitalWrite(in1,HIGH);
  digitalWrite(in2,LOW);
  digitalWrite(in3,HIGH);
  digitalWrite(in4,LOW); 

}

void _mright()
{
 analogWrite(ENA,ABS);
 analogWrite(ENB,ABS);
  digitalWrite(in1,LOW);
  digitalWrite(in2,HIGH);
  digitalWrite(in3,LOW);
  digitalWrite(in4,HIGH);

} 
void _mStop()
{
  digitalWrite(ENA,LOW);
  digitalWrite(ENB,LOW);

} 
