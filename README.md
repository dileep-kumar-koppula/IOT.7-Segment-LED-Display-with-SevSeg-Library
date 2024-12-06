# 7-Segment LED Display with SevSeg Library

This example demonstrates how to use a 7-segment LED display to show numbers from 0 to 9 using the **SevSeg** library. The display will show each number for 1 second, and then it will loop back to 0 after displaying 9.

## Code

```cpp
#include "SevSeg.h"

// Create a SevSeg object
SevSeg sevseg;

void setup() {
      // Set to 1 for a single-digit display
      byte numDigits = 1;
      
      // Defines common pins for multi-digit display (empty for single-digit)
      byte digitPins[] = {};
      
      // Defines Arduino pin connections in order: A, B, C, D, E, F, G, DP
      byte segmentPins[] = {9, 8, 7, 6, 5, 4, 3, 2};
      
      // Display type: use COMMON_CATHODE for common cathode display
      byte displayType = COMMON_CATHODE; // Use COMMON_ANODE for Common Anode display
      
      // Set to 'false' if resistors are connected to the common pin
      bool resistorsOnSegments = true; 
      
      // Initialize sevseg object
      sevseg.begin(displayType, numDigits, digitPins, segmentPins, resistorsOnSegments);
      
      // Set display brightness
      sevseg.setBrightness(90);
}

void loop() {
   // Display numbers 0-9 with a 1-second delay
   for(int i = 0; i <= 10; i++) {
     if (i == 10) {
        i = 0; // Reset the counter to 0 after displaying 9
     }
     sevseg.setNumber(i);  // Set the number to display
     sevseg.refreshDisplay(); // Refresh the display to show the new number
     delay(1000); // Wait for 1 second
   }
}
