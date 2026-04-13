# Dog-Water-Bowl-Home-Assistant

So the FSR largely is orphaned. I couldn't get it to work but I'm leaving it up so whomever can work on it. However, the load cell version I did get to work. 

Note I attached some MP3 files. I made them mix with some random sound I found, and AI voice. 

# What is this?

This project was born out of a week-long search for an "off-the-shelf" solution that simply didn't exist. It ensures that human error doesn't lead to thirsty pets. By monitoring the weight of a water bowl, the system assumes a low weight equals low water and alerts the household.

Local visual feedback is provided via a color-coded LED system, making status checks easy at a glance without opening an app.


# Features

* Real-time Local Status: 4-LED system (Blue for Full, Yellow for Mid, Red for Empty, Green for WiFi).
* Rolling Error Animation: If the sensor loses signal for 3 minutes (or fails on boot), the LEDs will roll Red → Yellow → Blue to signal a hardware issue.
* Home Assistant Integration: A binary sensor reports "Problem" states directly to your dashboard.
* Smart "Nag" Loop: Integrates with Home Assistant automations to remind you every 15 minutes until the bowl is filled.
* On-the-Fly Calibration: Adjust thresholds, brightness, and calibration factors via the Home Assistant UI without reflashing.

Note: The automation basically waits for the bowl to be below a point after 5 minutes. I did this because if someone is cleaning the bowl or maybe a dog is drinking and it hasn't crossed that line. I don't want it to start nagging. But if no one fills it (at least get it in the yellow (between red and blue). Then every 15 min after it will nag. 

# Hardware Requirements

* Microcontroller: Seeed Studio XIAO ESP32-C6 (or equivalent ESP32).

* Sensor: * Primary: Geekstory 20kg Load Cell + HX711 Kit https://www.amazon.com/dp/B0B6NRW8GG (this is what I used since it has most everything you need)
* Alternative (Experimental): Force Sensitive Resistor (FSR).
* Visuals: 4x 5mm LEDs (Red, Yellow, Blue, Green).

Resistors:

* 4x 220Ω (Current limiting for LEDs).
* 1x 10kΩ (Pull-down if using FSR). You don't need this if you are using the load cell. 

# 3D Printing & Enclosure

The housing for this project can be printed using the model linked below:

https://makerworld.com/en/models/2628200-orphaned-dog-water-bowl-sensor#profileId-2901745


# Wiring Diagram (Load Cell - Recommended)

Note the exact for mine is XIAO C6. Check your chip.

HX711 VCC > 3.3V
HX711 GND > GND
HX711 DT > GPIO18 (D4)
HX711 SCK > GPIO19 (D5)

Load cell to hx711

Red > e+
Black > e-
White > a-
Green > a+

LED

Pin > resistor > ground

Red = D8
Yellow = D10
Blue = D2
Green = D9

# Build notes

* Use lead-free rosin core solder (SAC305 or Sn99.3) as this project resides near pet water.
* Use hot glue over the DuPont connections and the ESP32 mounting points to prevent wires from wiggling loose.
* Set your "Empty" value slightly above true zero (e.g., at 5% capacity) to ensure your dog never actually hits a dry bowl before the alert triggers.

# Legal

This project is open-source. If you can profit from making a version that helps people with disabilities or simplified lives, please do. This project was designed to overcome motor skill challenges, memory issues, and provide a reliable, automated safety net for pets.
