# Task2i
// Motor pins
const int motorLeftForward = 2;
const int motorLeftBackward = 3;
const int motorRightForward = 4;
const int motorRightBackward = 5;

// IR sensor pins
const int sensorLeft = A0;
const int sensorRight = A1;

// Sensor threshold (adjust after testing)
const int threshold = 500;

// Motor speed
const int speed = 150;

void setup() {
  pinMode(motorLeftForward, OUTPUT);
  pinMode(motorLeftBackward, OUTPUT);
  pinMode(motorRightForward, OUTPUT);
  pinMode(motorRightBackward, OUTPUT);
  pinMode(sensorLeft, INPUT);
  pinMode(sensorRight, INPUT);
}

void loop() {
  int leftSensorValue = analogRead(sensorLeft);
  int rightSensorValue = analogRead(sensorRight);

  bool leftOnLine = leftSensorValue < threshold;
  bool rightOnLine = rightSensorValue < threshold;

  if (leftOnLine && rightOnLine) {
    // Both sensors see black -> move forward
    forward();
  } else if (!leftOnLine && rightOnLine) {
    // Left is off (white), right is on (black) -> turn left
    turnLeft();
  } else if (leftOnLine && !rightOnLine) {
    // Right is off, left is on -> turn right
    turnRight();
  } else {
    // Both off line -> stop briefly, then turn around to search
    stopCar();
    delay(200);
    reverseTurn();
  }
}

// Move forward
void forward() {
  analogWrite(motorLeftForward, speed);
  analogWrite(motorRightForward, speed);
  digitalWrite(motorLeftBackward, LOW);
  digitalWrite(motorRightBackward, LOW);
}

// Turn left (pivot)
void turnLeft() {
  analogWrite(motorRightForward, speed);
  digitalWrite(motorLeftForward, LOW);
  digitalWrite(motorLeftBackward, LOW);
  digitalWrite(motorRightBackward, LOW);
}

// Turn right (pivot)
void turnRight() {
  analogWrite(motorLeftForward, speed);
  digitalWrite(motorRightForward, LOW);
  digitalWrite(motorLeftBackward, LOW);
  digitalWrite(motorRightBackward, LOW);
}

// Stop all motors
void stopCar() {
  digitalWrite(motorLeftForward, LOW);
  digitalWrite(motorLeftBackward, LOW);
  digitalWrite(motorRightForward, LOW);
  digitalWrite(motorRightBackward, LOW);
}

// Reverse turn to search for line
void reverseTurn() {
  // Reverse a bit
  analogWrite(motorLeftBackward, speed);
  analogWrite(motorRightBackward, speed);
  digitalWrite(motorLeftForward, LOW);
  digitalWrite(motorRightForward, LOW);
  delay(300);

  // Pivot to find the line again
  analogWrite(motorLeftBackward, speed);
  digitalWrite(motorRightBackward, LOW);
  digitalWrite(motorLeftForward, LOW);
  digitalWrite(motorRightForward, LOW);
  delay(300);
}Sengizoqobela lento
