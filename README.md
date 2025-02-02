# accident-prevention
mitgating accident prevention at hair pin bends
const int trigPinA = 9;
const int echoPinA = 8;
const int trigPinB = 11;
const int echoPinB = 10;
const int ledA =4;
const int ledB =3;
const int buzzerA = 7;
const int buzzerB = 6;

long durationA, durationB;
int distanceA, distanceB;

void setup() {
  Serial.begin(9600);
  
  pinMode(trigPinA, OUTPUT);
  pinMode(echoPinA, INPUT);
  pinMode(trigPinB, OUTPUT);
  pinMode(echoPinB, INPUT);
  
  pinMode(ledA, OUTPUT);
  pinMode(ledB, OUTPUT);
  pinMode(buzzerA, OUTPUT);
  pinMode(buzzerB, OUTPUT);
}

void loop() {
  // Measure distance from SensorA
  digitalWrite(trigPinA, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPinA, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPinA, LOW);
  durationA = pulseIn(echoPinA, HIGH);
  distanceA = durationA * 0.034 / 2;

  // Measure distance from SensorB
  digitalWrite(trigPinB, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPinB, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPinB, LOW);
  durationB = pulseIn(echoPinB, HIGH);
  distanceB = durationB * 0.034 / 2;
Serial.println(distanceA);
Serial.println(distanceB);

  // If SensorA detects a vehicle less than 100 cm, activate LED2
  if (distanceA < 100) {
    digitalWrite(ledB, HIGH);
    // If less than 50 cm, also activate Buzzer2
    if (distanceA < 50) {
      digitalWrite(buzzerB, HIGH);
    } else {
      digitalWrite(buzzerB, LOW);
    }
  } else {
    digitalWrite(ledB, LOW);
    digitalWrite(buzzerB, LOW);
  }

  // If SensorB detects a vehicle less than 100 cm, activate LED1
  if (distanceB < 100) {
    digitalWrite(ledA, HIGH);
    // If less than 50 cm, also activate Buzzer1
    if (distanceB < 50) {
      digitalWrite(buzzerA, HIGH);
    } else {
      digitalWrite(buzzerA, LOW);
    }
  } else {
    digitalWrite(ledA, LOW);
    digitalWrite(buzzerA, LOW);
  }

  delay(100);
}
