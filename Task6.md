Title:
# MUSIC SYNTHESISER USING A BUZZER 


Video:

https://drive.google.com/file/d/1w8FLy4LdniThm21uAwTlpec0eZnXa9df/view?usp=drive_link

Code:
# CODE FOR STAR WARS THEME

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
