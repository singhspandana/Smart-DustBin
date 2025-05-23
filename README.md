# Smart-DustBin
#include <Servo.h>
const int trigPin = 9;
const int echoPin = 10;
const int servoPin = 3;
const int distanceThreshold = 15;
Servo lidServo;

void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  lidServo.attach(servoPin);
  lidServo.write(0); 
  Serial.begin(9600);
}

void loop() {
  long duration;
  int distance;
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  duration = pulseIn(echoPin, HIGH);
  distance = duration * 0.034 / 2;
  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");
  if (distance <= distanceThreshold) {
    lidServo.write(90); 
    delay(3000);  
    lidServo.write(0);  
  }
  delay(500); 
}
