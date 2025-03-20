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
```
###_Buzzer_Beep_Circuit
```
void setup() {
  pinMode(8, OUTPUT);  // Corrected "pinmode" to "pinMode" and "output" to "OUTPUT"
}

void loop() {
  digitalWrite(8, HIGH); // Corrected "digital write" to "digitalWrite"
  delay(500);
  digitalWrite(8, LOW);
  delay(500);
}
```
###LED_chasing_(Sequential_LEDs)
```
#define LED1 2
#define LED2 3
#define LED3 4
#define LED4 5

void setup() {
  pinMode(LED1, OUTPUT);
  pinMode(LED2, OUTPUT);
  pinMode(LED3, OUTPUT);
  pinMode(LED4, OUTPUT);
}

void loop() {
  digitalWrite(LED1, HIGH);
  delay(200);
  digitalWrite(LED1, LOW);

  digitalWrite(LED2, HIGH);
  delay(200);
  digitalWrite(LED2, LOW);

  digitalWrite(LED3, HIGH);
  delay(200);
  digitalWrite(LED3, LOW);

  digitalWrite(LED4, HIGH);
  delay(200);
  digitalWrite(LED4, LOW);
}
```
###_Potentiometer_Controlled_LED_Brightness
```
int potPin = A0;
int ledPin = 9;
int potValue = 0;

void setup() {
    pinMode(ledPin, OUTPUT);
}

void loop() {
    potValue = analogRead(potPin); 
    int brightness = map(potValue, 0, 1023, 0, 255);
    analogWrite(ledPin, brightness); // Adjust brightness
}


