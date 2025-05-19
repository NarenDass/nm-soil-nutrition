# nm-soil-nutrition
NAAN MUDHALVAN PROJECT

\#include \<LiquidCrystal\_I2C.h>

// Initialize the LCD with I2C address 0x27 (or 0x3F depending on your LCD)
LiquidCrystal\_I2C lcd(0x27, 16, 2);

// Analog pins for potentiometers (NPK sensors)
const int nitrogenPin = A0;
const int phosphorusPin = A1;
const int potassiumPin = A2;

// LED pins for nutrient alerts
const int nitrogenLED = 2;
const int phosphorusLED = 3;
const int potassiumLED = 4;

void setup() {
// Start serial communication
Serial.begin(9600);

// Initialize LED pins as OUTPUT
pinMode(nitrogenLED, OUTPUT);
pinMode(phosphorusLED, OUTPUT);
pinMode(potassiumLED, OUTPUT);

// Initialize LCD
lcd.begin(16, 2);
lcd.print("Soil Nutrients:");
delay(2000);  // Display message for 2 seconds
lcd.clear();
}

void loop() {
// Read values from potentiometers
int nitrogen = analogRead(nitrogenPin);
int phosphorus = analogRead(phosphorusPin);
int potassium = analogRead(potassiumPin);

// Map the readings to nutrient levels (0-100 scale)
int N = map(nitrogen, 0, 1023, 0, 100);
int P = map(phosphorus, 0, 1023, 0, 100);
int K = map(potassium, 0, 1023, 0, 100);

// Display nutrient levels on LCD
lcd.setCursor(0, 0);
lcd.print("N: ");
lcd.print(N);
lcd.print(" P: ");
lcd.print(P);
lcd.setCursor(0, 1);
lcd.print("K: ");
lcd.print(K);

// Print nutrient values to Serial Monitor
Serial.print("N: "); Serial.print(N); Serial.print(" P: "); Serial.print(P); Serial.print(" K: "); Serial.println(K);

// Turn on LEDs if any nutrient is too low (<30)
digitalWrite(nitrogenLED, N < 30 ? HIGH : LOW);
digitalWrite(phosphorusLED, P < 30 ? HIGH : LOW);
digitalWrite(potassiumLED, K < 30 ? HIGH : LOW);

delay(1000);  // Wait for 1 second before updating
}  this code display non i have to connect physical device to check the soil and send the input to arduino and the output in lcd

