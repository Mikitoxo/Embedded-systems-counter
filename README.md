//Embedded systems display counter from 0 to 9999 at 50 Hz using a 4 digit, seven segment display.
//code is as follows: 



#include <SevSeg.h> // install on ARUINO  by tools>>manage libraries>>search>>Sevseg by Dean Reading
// makes it efficient to work with a seven segment display

SevSeg sevseg;  // Instantiate a seven-segment object

void setup() {
  byte numDigits = 4;                  // Number of digits in the display; this code works wit a 4 digit seven segment display
  byte digitPins[] = {2, 3, 4, 5};     // Pins connected to each digit of the 7-segment display
  byte segmentPins[] = {6, 7, 8, 9, 10, 11, 12, 13};  // Pins for each segment (A-G, DP)

  bool resistorsOnSegments = false;    // Set to false as there are no resistors
  byte hardwareConfig = COMMON_CATHODE; // COMMON_CATHODE or COMMON_ANODE :ie, types of seven segment displays
  bool updateWithDelays = false;       // Recommended to set false
  bool leadingZeros = false;           // No leading zeros
  bool disableDecPoint = true;         // Disable decimal points
  
  sevseg.begin(hardwareConfig, numDigits, digitPins, segmentPins, resistorsOnSegments, updateWithDelays, leadingZeros, disableDecPoint);
  sevseg.setBrightness(90);            // Set brightness (0-100); up to you
}                 

void loop() {
 
 //Count from 0 to 9999 at 50 Hz
  for (int i = 0; i < 10000; i++) {
    sevseg.setNumber(i);               // Display the current number without leading zeros
    sevseg.refreshDisplay();           // Update display
    delay(20);                         // Display at 50 Hz (0.02 second delay)
  }
}
