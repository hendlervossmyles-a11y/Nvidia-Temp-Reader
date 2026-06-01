// ***Made with help from google Gemini***

#include <LiquidCrystal.h>

// initialize the library with your pin mapping
const int rs = 12, en = 11, d4 = 5, d5 = 4, d6 = 3, d7 = 2;
LiquidCrystal lcd(rs, en, d4, d5, d6, d7);

void setup() {
  // 1. Start Serial communication at 9600 baud (matches your Python script)
  Serial.begin(9600);
  
  // 2. Initialize the LCD's columns and rows
  lcd.begin(16, 2);
  
  // 3. Print a startup message so you know it's working
  lcd.print("Waiting for PC...");
}

void loop() {
  // Check if there is data. 'greater than 0' is more reliable than '== true'
  if (Serial.available() > 0) {
    
    // Give the serial buffer a tiny moment (50ms) to fill up 
    // so the whole "RTX 3060 Ti" arrives before we start reading.
    delay(50); 
    
    // Read name until the dash
    String name = Serial.readStringUntil('-');
    // Read temp until the newline
    String temp = Serial.readStringUntil('\n');
    
    // Clean up the strings (removes accidental spaces or weird bits)
    name.trim();
    temp.trim();

    // Update Display
    lcd.clear();
    lcd.setCursor(0, 0);
    lcd.print(name);
    
    lcd.setCursor(0, 1);
    lcd.print("Temp: " + temp + " C");
  }
}