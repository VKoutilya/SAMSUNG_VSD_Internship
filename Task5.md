![WIN_20250216_15_02_33_Pro](https://github.com/user-attachments/assets/aed17ad4-b36c-4a9f-8a64-2d1f356bc9fa)

Overview: Buzzer Music Player Using VSD Mini Squadron Microcontroller 🎵🔊

Project Description:
This project demonstrates how to use a buzzer with the VSD Mini Squadron microcontroller with the CH32V003 RISC-V processor to play simple melodies. By generating different frequencies with the buzzer without using the tone() function, we can program the microcontroller to play predefined songs or even allow dynamic note input.


Key Features
✅ Play predefined melodies (e.g., "Twinkle Twinkle Little Star","Star Wars Theme")
✅ Use an array to store musical notes and durations
✅ Control the buzzer without the tone() function
✅ Expandable to support multiple songs

Hardware Requirements
-->VSD Mini Squadron Microcontroller
-->Piezo Buzzer (Passive or Active)
-->Wires & Breadboard (if necessary)
-->Type-C USB Cable (to upload code)

Software Requirements
-->Arduino IDE (to write and upload code)

HOW IT WORKS:
  1. The buzzer is connected to a specified pin [PD0] on the VSD Mini Squadron microcontroller.
  2. The melody array stores a sequence of musical notes (frequencies).
  3. The noteDurations array defines how long each note should play.
  4. The setup() function initializes the buzzer pin and calls playMelody().
  5. In playMelody():
     - The loop iterates through each note in the melody array.
     - The loop instead of the tone() function generates a sound of the specified frequency and duration.
     - A delay is added to separate notes properly.
     - The Loop breaks and the noTone() function stops the sound before moving to the next note.
  6. The loop() function remains empty since the melody is played once at startup.

CODE:
# For StarWars Theme
#include "pitches.h"

#define BUZZER_PIN PD0  // Buzzer connected to PD0

int melody[] = {
  NOTE_AS4, NOTE_AS4, NOTE_AS4,
  NOTE_F5, NOTE_C6,
  NOTE_AS5, NOTE_A5, NOTE_G5, NOTE_F6, NOTE_C6,
  NOTE_AS5, NOTE_A5, NOTE_G5, NOTE_F6, NOTE_C6,
  NOTE_AS5, NOTE_A5, NOTE_AS5, NOTE_G5, NOTE_C5, NOTE_C5, NOTE_C5,
  NOTE_F5, NOTE_C6,
  NOTE_AS5, NOTE_A5, NOTE_G5, NOTE_F6, NOTE_C6,

  NOTE_AS5, NOTE_A5, NOTE_G5, NOTE_F6, NOTE_C6,
  NOTE_AS5, NOTE_A5, NOTE_AS5, NOTE_G5, NOTE_C5, NOTE_C5,
  NOTE_D5, NOTE_D5, NOTE_AS5, NOTE_A5, NOTE_G5, NOTE_F5,
  NOTE_F5, NOTE_G5, NOTE_A5, NOTE_G5, NOTE_D5, NOTE_E5, NOTE_C5, NOTE_C5,
  NOTE_D5, NOTE_D5, NOTE_AS5, NOTE_A5, NOTE_G5, NOTE_F5,

  NOTE_C6, NOTE_G5, NOTE_G5, REST, NOTE_C5,
  NOTE_D5, NOTE_D5, NOTE_AS5, NOTE_A5, NOTE_G5, NOTE_F5,
  NOTE_F5, NOTE_G5, NOTE_A5, NOTE_G5, NOTE_D5, NOTE_E5, NOTE_C6, NOTE_C6,
  NOTE_F6, NOTE_DS6, NOTE_CS6, NOTE_C6, NOTE_AS5, NOTE_GS5, NOTE_G5, NOTE_F5,
  NOTE_C6
};

int durations[] = {
  8, 8, 8,
  2, 2,
  8, 8, 8, 2, 4,
  8, 8, 8, 2, 4,
  8, 8, 8, 2, 8, 8, 8,
  2, 2,
  8, 8, 8, 2, 4,

  8, 8, 8, 2, 4,
  8, 8, 8, 2, 8, 16,
  4, 8, 8, 8, 8, 8,
  8, 8, 8, 4, 8, 4, 8, 16,
  4, 8, 8, 8, 8, 8,

  8, 16, 2, 8, 8,
  4, 8, 8, 8, 8, 8,
  8, 8, 8, 4, 8, 4, 8, 16,
  4, 8, 4, 8, 4, 8, 4, 8,
  1
};

void setup() {
  pinMode(BUZZER_PIN, OUTPUT);  // Set buzzer pin as output
}

void playTone(int frequency, int duration) {
  long period = 1000000 / frequency;  // Calculate the period of the note in microseconds
  long pulseWidth = period / 2;      // Half period for high and low times

  long elapsedTime = 0;
  while (elapsedTime < duration * 1000) {  // Multiply by 1000 to convert milliseconds to microseconds
    digitalWrite(BUZZER_PIN, HIGH);  // Turn the buzzer on
    delayMicroseconds(pulseWidth);    // Wait for half the period
    digitalWrite(BUZZER_PIN, LOW);   // Turn the buzzer off
    delayMicroseconds(pulseWidth);    // Wait for the other half of the period

    elapsedTime += period;  // Increment the elapsed time by the period (in microseconds)
  }
}

void loop() {
  int size = sizeof(durations) / sizeof(int);

  // Iterate through the melody and play each note
  for (int note = 0; note < size; note++) {
    int duration = 1000 / durations[note];  // Calculate the duration of the note in milliseconds
    int frequency = melody[note];  // Get the frequency for the note

    // Play the note using the playTone function
    playTone(frequency, duration);

    // Pause between notes (30% of the note duration)
    int pauseBetweenNotes = duration * 1.30;
    delay(pauseBetweenNotes);
  }
}

Possible Enhancements 🚀
🔹 Add multiple songs & a button to switch between them.
🔹 Allow custom song input using a serial monitor.
🔹 Integrate with an OLED screen for song display.
🔹 Sync with LEDs to blink in rhythm with the melody.

 
