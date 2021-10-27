# Control LED strip with Arduino Ultrasonic sensor 

## Overview 
In this mini-project, we will be combining an ultrasonic distance sensor and an addressable LED strip. The goal is to trigger the LED strip when a person is passing by in a certain distance. The indicator will be effective between a minimum and maximum distance.

## Required Materials
- HC SR04 Ultrasonic Sensor
- Arduino Uno
- LED Strip
- Breadboard
- Jumper wires
- Singe LED
- 220 Ohm resistors

### Steps: Prepare the UNO Board

1. Open a new Arduino sketch.
2. Navigate to: Tools
3. Select the Arduino UNO at Arduino AVR board.



Hook your Arduino UNO on to your laptop via USB 
Upload an empty sketch onto your board to empty the UNO. Problem: At this step I got a error. There was a problem uploading to the board. Solution: I did not select the right port, it needed to go to the USB port.  2/3/4

ADD THE LED
Connect your LED strip to the UNO. Here I hesitated a bit, I did not know how to get the LED connected on the board.The an idea came up, I have lots of jumper wires! FOTO's
Connect the jumper wires from the LED to the UNO going:
LED GND to GDN board
LED 5V+ to 5V Board
LED Din to Pin number 2 foto
Now lets see if the hardware is connected right by uploading code:

#include <Adafruit_NeoPixel.h>

#define PIN 2 // Here is where the LED is connected to the Arduino UNO

#define NUMPIXELS 10

// When setting up the NeoPixel library, we tell it how many pixels,
// and which pin to use to send signals. Note that for older NeoPixel
// strips you might need to change the third parameter -- see the
// strandtest example for more information on possible values.
Adafruit_NeoPixel pixels(NUMPIXELS, PIN, NEO_GRB + NEO_KHZ800);

#define DELAYVAL 890 // Tinlme (in milliseconds) to pause between pixels

void setup() {
  // These lines are specifically to support the Adafruit Trinket 5V 16 MHz.
  // Any other board, you can remove this part (but no harm leaving it):
#if defined(__AVR_ATtiny85__) && (F_CPU == 16000000)
  clock_prescale_set(clock_div_1);
#endif
  // END of Trinket-specific code.

  pixels.begin(); // INITIALIZE NeoPixel strip object (REQUIRED)
}

void loop() {
  pixels.clear(); // Set all pixel colors to 'off'

  // The first NeoPixel in a strand is #0, second is 1, all the way up
  // to the count of pixels minus one.
  for(int i=0; i<NUMPIXELS; i++) { // For each pixel...

    // pixels.Color() takes RGB values, from 0,0,0 up to 255,255,255
    // Here we're using a moderately bright green color:
    pixels.setPixelColor(i, pixels.Color(129, 230, 0));

    pixels.show();   // Send the updated pixel colors to the hardware.

    delay(DELAYVAL); // Pause before next pass through loop
  }
}


FOTO VAN DAT HET WERKT







ADD THE ULTRASONIC SENSOR
Get extra jumper wires, breadboard and the sensor for application
For now, detach the LED strip
Attach the Sensor to the breadboard and 4 jumper wires from the sensor to:
Echo to Pin 13
Trig to Pin 12
VCC to 5V
GND to GND
Get the LED strip and attach 
GND to positive side of breadboard
5V to negative side off breadboard
Din to the selected pin, witch will be Pin 2
Upload the code and see what happens
// define the sensor and the LED strip
const int echo = 13;
const int trig = 12;
const int LED1 = 2;

int duration = 0;
int distance = 0;

void setup() {
  // put your setup code here, to run once:
pinMode(trig, OUTPUT);
pinMode(echo, INPUT);
pinMode(LED1 , OUTPUT);

Serial.begin(9600);
}

void loop() {
  // put your main code here, to run repeatedly:
digitalWrite (trig, HIGH);
delayMicroseconds(1000);
digitalWrite(trig, LOW);

duration = pulseIn(echo, HIGH);
distance = (duration/2) / 28.5;
Serial.println(distance);

  if ( distance = 2 )
  {
    digitalWrite(LED1, HIGH);
  }
  else
  {
    digitalWrite(LED1, LOW);
  }

}


TRY SINGEL LED
The LED strip did not work, sadly I think it has something to do with the coding. I am not sure how to get the LED strip in the code without using NeoPixel library or something. But, don’t give up! I want to have something responding to the sensor. 
Take a single LED and attach it to the breadboard 
Take the ohm receptor and connect the sides of the breadboard
Insert the jumper wires dn attach the jumper wire to the pin that’s it declared in the code, witch is now still Pin2
Upload the code and see, It works! 
