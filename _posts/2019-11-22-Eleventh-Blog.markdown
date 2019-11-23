---
layout: post
title: "Week 11"
---


This week I make a simon says game from a custom pcb from hackerboxes.com. The kit came with everything needed to create the game.  

The first step is to assemble and solder all the components onto the pcb.  You have to solder the coin cell clips onto the back of the board. 
![Back of PCB][/assets/Back.jpg]
On the front of the board you need to solder four tactile buttons, a 8pin Dip socket, slide switch, and the four APA106 RGB LED's.
![Front of PCB][/assets/Front.jpg]

Once all the components are attached to the board you need to program the .ino file onto a ATtiny85 chip.
This step is not very hard but they do not give you a ton of direction on how to accomplish this step.  
I was able to program it using a breadboard and an Arduino Uno.  All you have to do is make sure the pins are connected correctly.  You will use 13, 12, 11, 10, 5v, and GND from the Arduino. 
![Tiny Connections][/assets/tiny.png]
Using the half cirlce on the front of the chip as reference, The first pin on the right is 5V.  The next three pins on the right side are connected to 13, 12 and 11 in order going down.  The top left pin on the left side is connected to the 10 on the ardunio the next 2 are skipped and the ground is connected to the bottom left pin.  
![Arduino settings][/assets/tiny85.png]
The next step you need to complete is to add the ATTiny library to the Arduino IDE.  To do this you go toFile> Preferences > near the bottom is Additional Boards Manager URLS:
Paste this link there. <https://raw.githubusercontent.com/damellis/attiny/ide-1.6.x-boards-manager/package_damellis_attiny_index.json>

Next add the Adafruit NeoPixel library by Adafruit via Library Manager. This is located under the Sketch tab.

Next you need to download the HBSimonBadge.ino which can be downloaded from hackerbox #0044.  Load this
file into Arduino IDE.  Next under sketch change the clock speed from 1MHz to 8MHz under tools> Clock.

Make sure you have Ardunio as ISP selected then select burn bootloader.  After this step you just upload your image as you normally would.  Now you can plug in your chip to your PCB and test it out.  There was another step to include a pizo buzzer but I decided to skip this step as I thought it might be annoying. 
