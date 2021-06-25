//Created by Guninder M on 6/25/21. Revision 1//

#include "DHT.h"    //install this library from Library Manager and 
                    //install the additional library it requests while doing so

#define DHTPIN 2    //the digital pin # on which sensor OUT is connected to
#define DHTTYPE DHT11   //sensor type (there is a DHT22 available as well)
DHT dht(DHTPIN, DHTTYPE);  //DHT library function

//pin assignment
int relay_1 = 7;  //relay 1 pin to activate coil
int relay_2 = 8;  //relay 2 pin to activate coil

//Actuator door open and close temperature values in celsius - can be changed to suit application needs
int open_door_temp = 27;
int close_door_temp = 24;


void setup() {
  Serial.begin(9600);
  Serial.println(F("DHTxx test!"));

  dht.begin();
  
  pinMode(relay_1, OUTPUT); //defining relay 1 pin as output
  pinMode(relay_2, OUTPUT); //defining relay 2 pin as output
  
  digitalWrite(relay_1, LOW); //deactivating relay 1
  digitalWrite(relay_2, LOW); //deactivating relay 2
  
}

void loop() {

  float h = dht.readHumidity();  //reads humidity
  float t = dht.readTemperature(); //reads temperature
  float f = dht.readTemperature(true); //reads temperature 

  if (isnan(h) || isnan(t) || isnan(f)) {
    Serial.println(F("Failed to read from DHT sensor!"));
    return;
  }

  float hif = dht.computeHeatIndex(f, h); //converts the readings to celcius 
  float hic = dht.computeHeatIndex(t, h, false); //converts the readings to fahrenheit

//  //Serial.print is useful if you are using serial monitor on PC and is not required for this code to work 
//  Serial.print(F(" Humidity: "));
//  Serial.print(h);
//  Serial.print(F("%  Temperature: "));
//  Serial.print(t);
//  Serial.print(F("°C "));
//  Serial.print(f);
//  Serial.print(F("°F  Heat index: "));
//  Serial.print(hic);
//  Serial.print(F("°C "));
//  Serial.print(hif);
//  Serial.println(F("°F"));
  
  
  if (hic > open_door_temp) {         //if the temperature value is higher than 27C, extend actuator
  
    digitalWrite(relay_1, HIGH);
    digitalWrite(relay_2, LOW);
  
  }

  else if (hic < close_door_temp) {     //if the temperature value is lower than 24C, retract actuator
    digitalWrite(relay_1, LOW);
    digitalWrite(relay_2, HIGH);
  }

  else {
    
  }

  delay(500);  //can be changed based on needs

}
