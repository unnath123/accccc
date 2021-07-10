arduino code final year project

 
 #include <SoftwareSerial.h>

SoftwareSerial mySerial(9, 10);

void setup()
{
  pinMode(LED_BUILTIN, OUTPUT);
  blinky(5);
  mySerial.begin(9600);   // Setting the baud rate of GSM Module  
  Serial.begin(9600);    // Setting the baud rate of Serial Monitor (Arduino)
  delay(100);
}
void blinky(int rp){
  
  for(int i=0;i<rp;i++){
  digitalWrite(LED_BUILTIN, HIGH);   // turn the LED on (HIGH is the voltage level)
  delay(1000);                       // wait for a second
  digitalWrite(LED_BUILTIN, LOW);    // turn the LED off by making the voltage LOW
  delay(1000);

  }
}

void loop()
{
  if (Serial.available()>0)
   
  {
   
      mySerial.println("AT+CMGF=1");    //Sets the GSM Module in Text Mode
     delay(1000);  // Delay of 1 second
     mySerial.println("AT+CMGS=\"+919741037489\"\r"); // Replace x with mobile number
     delay(1000);
     mySerial.println("Technolab creation");// The SMS text you want to send
     delay(100);
     mySerial.println((char)26);// ASCII code of CTRL+Z for saying the end of sms to  the module 
      delay(1000);
      



      

  }

 if (mySerial.available()>0)
   Serial.write(mySerial.read());
}

