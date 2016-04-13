# Schrodinger-s-Chicken-Coop
It lets you know whether the chicken in the box is alive or dead. If it's alive, the RGB light stays blue. If it's dead, it turns read. 
This project uses a breadboard, a 10 mm RGB LED, a PIR sensor, two 220h reducers, and an Arduino Uno. The code is as follows. 






//constants 
const int sensorPin = 2;
const int redPin = 9;
const int bluePin = 10; 
long duration = 60000; 
// variables
int blueState = 1;
int sensorState = 0; 
long CurrentMillis = 0;
long previousMillis = 0;





void setup() {
 pinMode (sensorPin, INPUT);
 pinMode (redPin, OUTPUT);
 pinMode (bluePin, OUTPUT);
 digitalWrite (bluePin, LOW);
 digitalWrite (redPin, HIGH);
}

void loop() {
  sensorState = digitalRead(sensorPin);
  CurrentMillis = millis(); 
  // compare the sensorState to its previous state
  if (blueState == 1){
    // if the state has been changed, start the timer
    if (sensorState == HIGH) {
      previousMillis = CurrentMillis;
    }
    else { 
      if (CurrentMillis - previousMillis >= duration) { 
        blueState = 0;
        digitalWrite (redPin, LOW);
        digitalWrite (bluePin, HIGH);
      }
      
      }
    }else {
      if (sensorState == HIGH) {
       previousMillis = CurrentMillis;
      blueState = 1;
      digitalWrite (redPin, HIGH);
      digitalWrite (bluePin, LOW);
      }
      
      
  }

}
