# Fourth-Arduino-Project-3-LEDs-and-Physical-button
Using a physical button to turn on a red,yellow,and green LED, and the LED depends on amount of button presses

## UPDATE

## CODE
```cpp

const int buttonPin = 2;
const int redLedPin = 9;
const int yellowLedPin = 10;
const int greenLedPin = 4;

int pressCount = 0;

int buttonState = HIGH;
int lastReading = HIGH;

unsigned long lastDebounceTime = 0;
const unsigned long debounceDelay = 50;

void setup() {
  pinMode(buttonPin, INPUT_PULLUP);

  pinMode(redLedPin, OUTPUT);
  pinMode(yellowLedPin, OUTPUT);
  pinMode(greenLedPin, OUTPUT);

  digitalWrite(redLedPin, LOW);
  digitalWrite(yellowLedPin, LOW);
  digitalWrite(greenLedPin, LOW);
}

void loop() {
  int reading = digitalRead(buttonPin);

  if (reading != lastReading) {
    lastDebounceTime = millis();
  }

  if (millis() - lastDebounceTime >= debounceDelay) {
    if (reading != buttonState) {
      buttonState = reading;

      if (buttonState == LOW) {
        pressCount++;

        if (pressCount == 1) {
          digitalWrite(redLedPin, HIGH);
          digitalWrite(yellowLedPin, LOW);
          digitalWrite(greenLedPin, LOW);
        }
        else if (pressCount == 3) {
          digitalWrite(redLedPin, LOW);
          digitalWrite(yellowLedPin, HIGH);
          digitalWrite(greenLedPin, LOW);
        }
        else if (pressCount == 6) {
          digitalWrite(redLedPin, LOW);
          digitalWrite(yellowLedPin, LOW);
          digitalWrite(greenLedPin, HIGH);
        }
        else if (pressCount == 7) {
          digitalWrite(redLedPin, LOW);
          digitalWrite(yellowLedPin, LOW);
          digitalWrite(greenLedPin, LOW);
        }
        else if (pressCount == 8) {
          pressCount = 0;
        }
      }
    }
  }

  lastReading = reading;
}
