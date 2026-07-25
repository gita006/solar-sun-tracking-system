#include <Servo.h> 
 
Servo solarServo;  // Servo object 
 
// LDR pins 
int LDR4 = A0;  // Top Left 
int LDR3 = A1;  // Top Right 
int LDR2 = A2;  // Bottom Left 
int LDR1 = A3;  // Bottom Right 
 
// Servo pin 
int servoPin = 9; 
 
// LED pins 
int LED1 = 11;  // Bottom Right LED 
int LED2 = 10;  // Bottom Left LED 
int LED3 = 6;   // Top Right LED 
int LED4 = 3;   // Top Left LED 
 
// Variables 
int servoPos = 90;        // Initial servo position 
int errorThreshold = 15;  // Sensitivity threshold 
unsigned long lastPrintTime = 0;  // For 5-second Serial print delay 
 
void setup() { 
  Serial.begin(9600); 
  solarServo.attach(servoPin); 
  solarServo.write(servoPos); 
 
  pinMode(LED1, OUTPUT); 
  pinMode(LED2, OUTPUT); 
  pinMode(LED3, OUTPUT); 
  pinMode(LED4, OUTPUT); 
 
  delay(1000); 
} 
 
void loop() { 
  // --- Read LDR values --- 
  int val4 = analogRead(LDR4);  // Top Left 
  int val3 = analogRead(LDR3);  // Top Right 
  int val2 = analogRead(LDR2);  // Bottom Left 
  int val1 = analogRead(LDR1);  // Bottom Right 
 
  // --- Calculate averages --- 
  int topAvg = (val4 + val3) / 2; 
  int bottomAvg = (val2 + val1) / 2; 
  int leftAvg = (val4 + val2) / 2; 
  int rightAvg = (val3 + val1) / 2; 

  // --- Differences for tracking --- 
  int verticalDiff = topAvg - bottomAvg; 
  int horizontalDiff = leftAvg - rightAvg; 
 
  // --- Smooth Servo Movement --- 
  if (abs(horizontalDiff) > errorThreshold) { 
    if (horizontalDiff > 0 && servoPos > 0) 
      servoPos--;   // Move left 
    else if (horizontalDiff < 0 && servoPos < 180) 
      servoPos++;   // Move right 
 
    solarServo.write(servoPos); 
    delay(40);  // smooth step delay 
  } 
 
  // --- LED Control: darkest LDR LED ON --- 
  int minLight = min(min(val1, val2), min(val3, val4)); 
 
  // Turn OFF all LEDs first 
  digitalWrite(LED1, LOW); 
  digitalWrite(LED2, LOW); 
  digitalWrite(LED3, LOW); 
  digitalWrite(LED4, LOW); 
 
  // Light only the LED with the lowest (darkest) LDR value 
  if (minLight == val1) digitalWrite(LED1, HIGH);  // Bottom Right 
  else if (minLight == val2) digitalWrite(LED2, HIGH);  // Bottom Left 
  else if (minLight == val3) digitalWrite(LED3, HIGH);  // Top Right 
  else if (minLight == val4) digitalWrite(LED4, HIGH);  // Top Left 
 
  // --- Print every 5 seconds --- 
  if (millis() - lastPrintTime >= 5000) { 
    lastPrintTime = millis(); 
    Serial.print("LDR1="); Serial.print(val4); 
    Serial.print(" LDR2="); Serial.print(val3); 
    Serial.print(" LDR3="); Serial.print(val2); 
    Serial.print(" LDR4="); Serial.print(val1); 
    Serial.print("  Servo="); Serial.println(servoPos); 
  } 
}
