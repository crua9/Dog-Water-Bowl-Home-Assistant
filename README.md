# Dog-Water-Bowl-Home-Assistant
Making a dog water bowl alert system which connects to home assistant 
This is project is practical, uses affordable hardware, and solves a real problem. Here is a clean, professional README draft tailored to your specific setup.
I made this because after searching for a week or so for solutions that just work that I can just buy. I couldn't find anything. And this should make it where the human being stupid doesn't cause the dog to be thursty.


In short this uses the weight of the bowl. I highly suggest modifying this for your system. Like our dogs have a silicone pad the bowl is on. Due to this I'm not as worried about spills messing things up. 

---

# Dog Water Level Monitor (Home Assistant Integrated)

A smart water level monitor for pet bowls using a **Seeed Studio XIAO ESP32-C6** and a **Force Sensitive Resistor (FSR)**. This system provides local visual feedback via LEDs and integrates with Home Assistant for remote monitoring and persistent "nag" refill alerts.

## Features
* **Real-time Local Status:** 3-LED system (Blue/Yellow/Red) for instant water level visibility.
* **Home Assistant Binary Sensor:** Flips to "Problem" state automatically when water hits the critical low threshold.
* **Smart "Nag" Loop:** A Home Assistant automation that alerts you every 15 minutes until the bowl is actually refilled.

## Hardware Requirements
* **Microcontroller:** Seeed Studio XIAO ESP32-C6 or other ESP32
* **Sensor:** Force Sensitive Resistor (FSR). This is the one I used https://www.amazon.com/dp/B0FX2754JR
* **Visuals:** 3x 5mm LEDs (Red, Yellow, Blue)
* **Resistors:**
    * 1x 10k  (Pull-down for FSR)
    * 3x 220 (Current limiting for LEDs)

You will obviously need wiring, power, etc. 



---

## Wiring Diagram


Component,Pin on XIAO C6,Wiring Path

The sensor
* 3.3V → FSR Leg 1 → FSR Leg 2 → D1 (GPIO 1) → 10k resistor → GND

The LED. Note you can get the LED pin/color by the code you upload to the ESP32. 
* ESP Pin → LED → 200 → GND
Note you can do the restory before or after the LED. 1 resistor per LED.

---

## Build Notes
* **Soldering:** Use **lead-free rosin core solder** (SAC305 or Sn99.3) for safety, as this project lives near pet food/water.
* **Enclosure:** I made a 3D housing. I'm sure others can do a good job on it. I will update with a link where you can get my model.
* **Calibration:** Ensure you calibrate your "Empty" and "Full" values in your ESPHome/Arduino code to avoid the "red-blue flickering" loop.

Something to note with the calibration. Currently with how I have it setup, it basically looks at when it gets too low I would recommend offsetting this some. Like for example, you might want to have it say eympty when it is really at 5%. This preventing the dog from running out of water. The % the thing kicks out is more of the % you are at when you are in the yellow. Like you could do 100% for full and 0% when there is no water. But this in my opinion takes away from the usefulness of things. 
Also note I made it where you should be able to calibrate it in real time. This allowing you to simply just use and switch out bowls as needed without reuploading the firmware. 

---


Note I will upload later the automation for this. 


Right now for mine I use 2 helpers. A 15 minute timer and a toggle.

Basically if the bowl goes eympty for 5 minutes it flips the toggle on and alerts us. It starts a timer and when it is done if the toggle is still on then alert us again. If you add water and enough weight is applied to push it outside of eympty then it toggles off the thing. 
