# Make a Digital Timer!
 
## Part A. Revisiting Blink

**1. Blinking LEDs with Arduino**

**a. What line(s) of code do you need to change to make the LED blink (like, at all)?**
```sh
pinMode(9, OUTPUT);
digitalWrite(9, HIGH);
digitalWrite(9, LOW);
```
**b. What line(s) of code do you need to change to change the rate of blinking?**
```sh
// constants won't change. They're used here to set pin numbers:
const int buttonPin = 2; // the number of the pushbutton pin
const int ledPin = 9; // the number of the LED pin

// variables will change:
int buttonState = 0; // variable for reading the pushbutton status

void setup() {
// initialize the LED pin as an output: pinMode(ledPin, OUTPUT);
// initialize the pushbutton pin as an input:
pinMode(buttonPin, INPUT);
}

void loop() {
// read the state of the pushbutton value:
buttonState = digitalRead(buttonPin);

// check if the pushbutton is pressed. If it is, the buttonState is HIGH:
if (buttonState == HIGH) {
// turn LED on:
digitalWrite(ledPin, HIGH);
} else {
// turn LED off:
digitalWrite(ledPin, LOW);
}
}
```
**3. Fading LEDs on and off using Arduino**

**a) Which line(s) of code do you need to modify to correspond with your LED pin?**
The ledPin is already allign with the example code.
**b) How would you change the rate of fading?**
fadeValue += 5 
fadeValue -= 5

**c) (Extra) Since the human eye doesn't see increases in brightness linearly and the diode brightness is also nonlinear with voltage, how could you change the code to make the light appear to fade linearly?**

## Part B. Advanced Inputs

### 1. Potentiometer
**a. Post a copy of your new code in your lab write-up.**
```sh
int sensorPin = A0; // select the input pin for the potentiometer
int ledPin = 9; // select the pin for the LED
int sensorValue = 0; // variable to store the value coming from the sensor

void setup() {
// declare the ledPin as an OUTPUT:
pinMode(ledPin, OUTPUT);
}
void loop() {
// read the value from the sensor:
sensorValue = analogRead(sensorPin);
// turn the ledPin on
digitalWrite(ledPin, HIGH);
// stop the program for milliseconds:
delay(sensorValue);
// turn the ledPin off:
digitalWrite(ledPin, LOW);
// stop the program for for milliseconds:
delay(sensorValue);
}
```
### 2. Force Sensitive Sensor

**a. What resistance values do you see from your force sensor?**
range from 0 ~ 1023
**b. What kind of relationship does the resistance have as a function of the force applied? (e.g., linear?)**
nearly linear after the force is larger than 50g.
**c. Can you change the LED fading code values so that you get the full range of output voltages from the LED when using your FSR?**
The max value of LED is 255. We need to control the light of LED by the sensorValue/4.
The sensorValue is the value from FSR.

## Part C. Writing to the LCD
 
**a. What voltage level do you need to power your display?**
**b. What voltage level do you need to power the display backlight?**
3V
  
**b. What was one mistake you made when wiring up the display? How did you fix it?**
I run the wrong script so the LCD is not displyaing the right messages. 
**c. What line of code do you need to change to make it flash your name instead of "Hello World"?**
change 
```sh
lcd.print("hello, world!")
```
```sh
lcd.print("Betty Chou")
```
**d. Include a copy of your Lowly Multimeter code in your lab write-up.**
```sh
// include the library code:
#include <LiquidCrystal.h>

int sensorPin = A0; // select the input pin for the potentiometer
int sensorValue = 0; // variable to store the value coming from the sensor
// initialize the library by associating any needed LCD interface pin
// with the arduino pin number it is connected to
const int rs = 12, en = 11, d4 = 5, d5 = 4, d6 = 3, d7 = 2;
LiquidCrystal lcd(rs, en, d4, d5, d6, d7);

void setup() {
// set up the LCD's number of columns and rows:
lcd.begin(16, 2);
}
void loop() {
// read the value from the sensor:
sensorValue = analogRead(sensorPin);
// set the cursor to column 0, line 1
// (note: line 1 is the second row, since counting begins with 0):
lcd.setCursor(0, 1);
// print the number of seconds since reset:
lcd.print(sensorValue);
}
```
**e. Include a copy of your FSR thumb wrestling code in your lab write-up.**
```sh
#include <LiquidCrystal.h>

// initialize the library by associating any needed LCD interface pin
// with the arduino pin number it is connected to
const int rs = 12, en = 11, d4 = 5, d5 = 4, d6 = 3, d7 = 2;
LiquidCrystal lcd(rs, en, d4, d5, d6, d7);

int sensorPin1 = A0;
int sensorPin2 = A1;
int sensorValue1 = 0;
int sensorValue2 = 0;

void setup() {
  // set up the LCD's number of columns and rows:
  lcd.begin(16, 2);
}

void loop() {
  // set the cursor to column 0, line 1
  // (note: line 1 is the second row, since counting begins with 0):
  sensorValue1 = analogRead(sensorPin1);
  sensorValue2 = analogRead(sensorPin2);
  lcd.setCursor(0,1);
  if (sensorValue1 > sensorValue2){
    lcd.print(sensorValue1);
    lcd.print("player 1 win!");}
  else if (sensorValue2 > sensorValue1){
    lcd.print(sensorValue2);
    lcd.print("player 2 win!");
  } else{
      lcd.print(sensorValue2);
      lcd.print("Tie!");
  }
  delay(1000);
}
```

## Part D. Timer

Make a timer that uses any of the input devices to set a time, and then automatically (or manually, if you prefer) begin counting down, displaying the time left. Make your timer show an alert once the time is up with one of the output devices we connected during this lab, or you have available. (Hint: the sample code for [Examples->LiquidCrystal->HelloWorld](https://www.arduino.cc/en/Tutorial/HelloWorld) displays the time in seconds since the Arduino was reset...)
 
Note that for some of you, the time may seem to be decremented by 10 each second (that is, from 670=>660). Why is this? Do you think it's a hardware or software issue? Think about how 100 vs. 99 is written to the screen, and ask an instructor.

**a. Make a short video showing how your timer works, and what happens when time is up!**

**b. Post a link to the completed lab report to the class Slack.**

## OPTIONAL:
## Part E. Tone

Let's make the Arduino make some noise! We are going to start with the Tone example program:
 
`Examples->Digital->toneMelody`

The official Arduino tutorial for this code is [here](https://www.arduino.cc/en/Tutorial/ToneMelody?from=Tutorial.Tone)
Add a 75 Ohm resistor to limit the current to the speaker when you hook it up on your breadboard. If you would like it a little louder, you can use a lower value resistor, up to a minimum of 5 Ohms.

Wire it to your circuit with the black to ground and the red to Arduino Micro pin 8. 

**a. How would you change the code to make the song play twice as fast?**
 
Now change the speed back, and replace the melody[] and noteDurations[] arrays with the following:
```c++

int melody[] = {
  NOTE_D3,NOTE_D3,NOTE_D3,NOTE_G3,NOTE_D4,NOTE_C4,NOTE_B3,NOTE_A3,NOTE_G4,NOTE_D4, \
  NOTE_C4,NOTE_B3,NOTE_A3,NOTE_G4,NOTE_D4,NOTE_C4,NOTE_B3,NOTE_C4,NOTE_A3,0};
 
int noteDurations[] = {
  10,10,10,2,2,10,10,10,2,4, \
  10,10,10,2,4,10,10,10,2,4};
 ```
You'll also have to increase the for() loop index max from 8 to 20:
 ```c++
  for (int thisNote = 0; thisNote < 20; thisNote++) {
 ```
**b. What song is playing?**
 



---
How to upload code using your [RaspberryPi over command line](https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices/wiki/Uploading-code-to-the-Arduino-via-Raspberry-Pi-SSH).

How to upload the [code with x11](https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices/wiki/Uploading-code-to-the-Arduino-via-Raspberry-Pi-XWindows).