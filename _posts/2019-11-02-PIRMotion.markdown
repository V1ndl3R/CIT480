This week I made a PIR motion sensor, this is a passive infrared sensor which measures infrared light in a field or view.
For this project I used:
1 Ardunio Uno
1 PIR Motion sensor
1 Relay
1 Breadboard
1 USB Cable
1 LED - optional
Jumper cables

PIRs are made from a pyroelectric sensor which has a range of 5-7 meters in a 100 degree arc.
Because our bodies generate infrared heat it gets picked up by the motion sensor, when it detects someone enter the field.
The sensor will output a 5V signal for a specified period of time.  You can also program the delay before it will detect a person.  
There are two knobs installed on the front of the board, the right knob controls the range.  The range is from
3 to 7 meters.  Rotating the knob counter-clockwise will increase the knob and clockwise will decrease the range.
The knob on the left will increase or decrease the time delay.  If you rotate the knob to the left or counter-clockwise
it will decrease the time delay.  If you rotate the knob to the right or clockwise it will increase the time delay up to 
5 minutes.  This is the time that someone must stay within the field before they are detected.

Connecting the PIR to the Arduino

The PIR has three pins, with the side with the pins closest to you.  The left pin needs to be connected to the 5V connector
on the Arduino Uno.  The middle pin needs to be connected to pin 2 on the Arduino Uno.  The right most pin needs to be connected 
to the GND on the Uno.

Open Arduino IDE and select the board you are using, for our example we will select the Uno.  Load this code into
the sketch:

int ledPin = 13;
int inputPin = 2;
int pirState;

If you open the serial monitor and set the baud rate to 9600 bps you will be able to see output that show when motion is detected.
This is a very simple project but it can be used with many other projects.

