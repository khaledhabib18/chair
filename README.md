// Define pin assignments
const int switchPin = 7;      // Switch connected to pin 2
const int ledPin = 13;         // LED connected to pin 3
const int buzzerPin = 10;      // Buzzer connected to pin 4

// Variables to store the switch state
int lastSwitchState = HIGH;   // Previous state of the switch (input pull-up, HIGH by default)
int currentSwitchState;

void setup() {
  Serial.begin(9600);
  pinMode(switchPin, INPUT_PULLUP); // Set the switch pin as input with pull-up
  pinMode(ledPin, OUTPUT);          // Set the LED pin as output
  pinMode(buzzerPin, OUTPUT);       // Set the buzzer pin as output

  digitalWrite(ledPin, HIGH);        // Ensure LED is off initially
  digitalWrite(buzzerPin, LOW);     // Ensure buzzer is off initially
  Serial.println("Systm starts ");
}

void loop() {
  // Read the current state of the switch
  currentSwitchState = digitalRead(switchPin);

  if (currentSwitchState != lastSwitchState) {
    // Switch state has changed
    if (currentSwitchState == LOW) {
      // Switch is pressed
      Serial.println("Seat is full ");
      digitalWrite(ledPin, LOW);   // Turn on the LED
      digitalWrite(buzzerPin, HIGH); // Turn on the buzzer
      delay(1000);                  // Keep them on for 1 second
      digitalWrite(ledPin, HIGH);    // Turn off the LED
      digitalWrite(buzzerPin, LOW); // Turn off the buzzer
    } else {
      // Switch is released
	  Serial.println("Seat is empty ");
      for (int i = 0; i < 2; i++) {
        digitalWrite(ledPin, LOW);   // Blink the LED
        digitalWrite(buzzerPin, HIGH); // Activate the buzzer
        delay(500);                   // On for 0.5 seconds
        digitalWrite(ledPin, HIGH);    // Turn off the LED
        digitalWrite(buzzerPin, LOW); // Turn off the buzzer
        delay(500);                   // Off for 0.5 seconds
      }
    }
    // Update the last switch state
    lastSwitchState = currentSwitchState;
  }
}
