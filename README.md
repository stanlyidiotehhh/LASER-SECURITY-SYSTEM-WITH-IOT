# LASER-SECURITY-SYSTEM-WITH-IOT

#include <SoftwareSerial.h>

SoftwareSerial SIM900(7, 8);

String textForSMS;

int data = 0; 

int sensor = A1; 

void setup() {

  randomSeed(analogRead(0));

  Serial.begin(9600);

      SIM900.begin(9600);

Serial.println(" logging time completed!");

pinMode(sensor, INPUT); 

 delay(5000); // wait for 5 seconds

}

void loop() {

data = analogRead(sensor); 

Serial.println(data); 

     if ( data < 400)

  {

       textForSMS =  "\nIntruder detected";  

  sendSMS(textForSMS);

  Serial.println(textForSMS);

  Serial.println("message sent."); 

delay(5000);

  }

}

void sendSMS(String message)

{

  SIM900.print("AT+CMGF=1\r");                   

  delay(1000);

SIM900.println("AT + CMGS = \"+923339218213\""); 

  delay(1000);

  SIM900.println(message);                         

  delay(1000);

  SIM900.println((char)26);                       

  delay(1000); 

  SIM900.println();

  delay(100);                                                          

}
