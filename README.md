###BASIC_TINKERCAD_CIRCUITS
Codes that is used in building circuits

###_LED_Blinking_circuit
```
#define LED_PIN 13

void setup() {
  pinMode(LED_PIN, OUTPUT);
}

void loop() {
  digitalWrite(LED_PIN, HIGH); // Turn LED ON
  delay(1000);                 // Wait 1 second
  digitalWrite(LED_PIN, LOW);  // Turn LED OFF
  delay(1000);                 // Wait 1 second
}
```
###_Button_Controlled_LED
```
void setup() {
  pinMode(9, OUTPUT);
  pinMode(2, INPUT);
}

void loop() {
  if (digitalRead(2) == HIGH) {
    digitalWrite(9, HIGH);
  } else {
    digitalWrite(9, LOW);
  }
}
```
###_Traffic_Light_Controller
```
#define RED_LED 8
#define YELLOW_LED 9
#define GREEN_LED 10

void setup() {
  pinMode(RED_LED, OUTPUT);
  pinMode(YELLOW_LED, OUTPUT);
  pinMode(GREEN_LED, OUTPUT);
}

void loop() {
  digitalWrite(GREEN_LED, HIGH);
  delay(3000);
  digitalWrite(GREEN_LED, LOW);
  
  digitalWrite(YELLOW_LED, HIGH);
  delay(1000);
  digitalWrite(YELLOW_LED, LOW);

  digitalWrite(RED_LED, HIGH);
  delay(3000);
  digitalWrite(RED_LED, LOW);
}
```
###_DC_Motor_Control_with_Transistor
```
#define MOTOR_PIN 9

void setup() {
  pinMode(MOTOR_PIN, OUTPUT);
}

void loop() {
  analogWrite(MOTOR_PIN, 255); // Full speed
  delay(3000);
  
  analogWrite(MOTOR_PIN, 128); // Half speed
  delay(3000);
  
  analogWrite(MOTOR_PIN, 0);   // Stop
  delay(3000);
}


