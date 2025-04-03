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
###_LED_Chasing(Sequential_LEDs)
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
```
###_Temperature_and_Humidity_Monitor
```
#include <LiquidCrystal.h>  // Include LCD library

// Initialize LCD with the corresponding pins
LiquidCrystal lcd(7, 8, 9, 10, 11, 12);

#define TEMP_SENSOR_PIN A0  // Potentiometer connected to A0

void setup() {
    Serial.begin(9600);  // Start serial communication
    lcd.begin(16, 2);    // Initialize the LCD
    lcd.print("Temp Monitor");  // Welcome message
    delay(2000);
    lcd.clear();
}

void loop() {
    int sensorValue = analogRead(TEMP_SENSOR_PIN); // Read potentiometer value (0-1023)
    
    // Convert to temperature (simulated range: 0°C - 50°C)
    float temperature = map(sensorValue, 0, 1023, 0, 50);

    // Display on Serial Monitor
    Serial.print("Temperature: ");
    Serial.print(temperature);
    Serial.println("°C");

    // Display on LCD
    lcd.setCursor(0, 0);
    lcd.print("Temp: ");
    lcd.print(temperature);
    lcd.print(" C   ");  // Extra spaces to clear old values

    delay(1000); // Update every second
}
```
###_Temperature_controlled_Fan(using LM35 Sensor)
```
// Define the pin numbers
const int tempPin = A0;     // Pin for the TMP36 sensor (analog input)
const int fanPin = 3;       // Pin for controlling the fan (digital output)

int tempReading = 0;        // Variable to store the sensor reading
float voltage = 0.0;        // Voltage output from TMP36
float temperature = 0.0;    // Temperature in Celsius
const float thresholdTemp = 25.0;  // Threshold temperature (25°C)

// TMP36 characteristics
const float VREF = 5.0; // Reference voltage for Arduino (5V)

// Setup function runs once when the program starts
void setup() {
  // Initialize the fan control pin as output
  pinMode(fanPin, OUTPUT);
  // Start serial communication for debugging
  Serial.begin(9600);
}

// Main loop runs repeatedly
void loop() {
  // Read the analog value from the TMP36 sensor (0 to 1023)
  tempReading = analogRead(tempPin);

  // Convert the analog reading to voltage (based on VREF)
  voltage = tempReading * (VREF / 1023.0);

  // TMP36: 500mV = 0°C and 500mV per degree Celsius
  // Calculate temperature in Celsius
  temperature = (voltage - 0.5) * 100.0;

  // Print temperature to the Serial Monitor for debugging
  Serial.print("Temperature: ");
  Serial.print(temperature);
  Serial.println(" C");

  // Control the fan based on the temperature threshold
  if (temperature >= thresholdTemp) {
    digitalWrite(fanPin, HIGH);  // Turn on the fan
    Serial.println("Fan ON");
  } else {
    digitalWrite(fanPin, LOW);   // Turn off the fan
    Serial.println("Fan OFF");
  }
  // Wait for a short period before reading again
  delay(1000);
}
```
###Digital_thermometer_with_LCD_Display
```
#include <LiquidCrystal.h>
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);

int buttonPin = 7;
int count = 0;
bool lastButtonState = LOW;

void setup() {
  pinMode(buttonPin, INPUT);
  lcd.begin(16, 2);
  lcd.print("Press to count:");
}

void loop() {
  bool currentState = digitalRead(buttonPin);
  
  if (currentState == HIGH && lastButtonState == LOW) {
    count++;
    lcd.setCursor(0, 1);
    lcd.print("Count: ");
    lcd.print(count);
    lcd.print("   ");
    delay(200); // Debounce
  }
  
  lastButtonState = currentState;
}
```
###_Temperature_and_Humidity_Display_using_DHT11
```
#include <Keypad.h>
#include <Servo.h>

Servo myServo;
const String password = "987456";
String input = "";

const byte ROWS = 4;
const byte COLS = 4;
char keys[ROWS][COLS] = {
    {'1', '2', '3', 'A'},
    {'4', '5', '6', 'B'},
    {'7', '8', '9', 'C'},
    {'*', '0', '#', 'D'}
};

byte rowPins[ROWS] = {9, 8, 7, 6};
byte colPins[COLS] = {5, 4, 3, 2};

Keypad keypad = Keypad(makeKeymap(keys), rowPins, colPins, ROWS, COLS);

void setup() {
    Serial.begin(9600);
    myServo.attach(10);
    myServo.write(0); // Locked position
}

void loop() {
    char key = keypad.getKey();
    if (key) {
        Serial.print(key);
        if (key == '#') {
            if (input == password) {
                Serial.println(" Access Granted!");
                myServo.write(90); // Unlock
                delay(5000);
                myServo.write(0); // Lock again
            } else {
                Serial.println(" Access Denied!");
            }
            input = "";
        } else {
            input += key;
        }
    }
}
```
###TMP36_Temperature_Sensor_&_LCD_Wiring
```
#include <LiquidCrystal.h>

#define TMP36_PIN A0  // TMP36 sensor connected to A0
LiquidCrystal lcd(7, 6, 5, 4, 3, 2);  // LCD connected to Arduino pins

void setup() {
    lcd.begin(16, 2);      // Initialize LCD
    lcd.print("Temperature Sensor");
    delay(2000);
    lcd.clear();
}

void loop() {
    int sensorValue = analogRead(TMP36_PIN); // Read analog value
    float voltage = sensorValue * (5.0 / 1023.0); // Convert to voltage
    float temperature = (voltage - 0.5) * 100.0;  // Convert to Celsius

    lcd.setCursor(0, 0);
    lcd.print("Temp: ");
    lcd.print(temperature);
    lcd.print(" C");

    delay(2000);
}

