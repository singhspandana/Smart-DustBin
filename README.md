# Smart-DustBin
#include <Servo.h>

// Pin Definitions
const int trigPin = 9;
const int echoPin = 10;
const int servoPin = 3;

// Distance Threshold in cm
const int distanceThreshold = 15;

Servo lidServo;

void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  lidServo.attach(servoPin);
  lidServo.write(0); // Start with lid closed
  Serial.begin(9600);
}

void loop() {
  long duration;
  int distance;

  // Trigger the ultrasonic sensor
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  // Read the echo time
  duration = pulseIn(echoPin, HIGH);

  // Calculate the distance in cm
  distance = duration * 0.034 / 2;

  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");

  if (distance <= distanceThreshold) {
    // Open the lid
    lidServo.write(90); // adjust as needed
    delay(3000);         // keep open for 3 seconds
    lidServo.write(0);   // close the lid
  }

  delay(500); // reduce CPU usage
}
