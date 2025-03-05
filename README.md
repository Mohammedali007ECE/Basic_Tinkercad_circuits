###Basic_Tinkercad_circuits
Codes that is used in building circuits

```#_LED_Blinking_circuit

#include <avr/io.h>
#include <util/delay.h>

int main(void) {
    DDRB |= (1 << PB5);  // Set PB5 (Pin 13) as output
  while (1) {
        PORTB |= (1 << PB5);  // Turn LED ON
        _delay_ms(1000);
        PORTB &= ~(1 << PB5); // Turn LED OFF
        _delay_ms(1000);
    }
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
