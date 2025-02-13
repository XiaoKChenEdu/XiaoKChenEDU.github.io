---
layout: project
type: project
image: img/projects/SCADA-Water-System/Title.png
title: "SCADA Water/Oil System"
date: 2023
published: true
labels:
  - Circuit Design
  - Raspberry Pi
  - Python
summary: "Designed and implemented an automated water circulation system controlled by Raspberry Pi."
---

<div class="text-center p-4">
  <img width="300px" src="../img/projects/SCADA-Water-System/1.jpg" class="img-thumbnail" >
  <img width="300px" src="../img/projects/SCADA-Water-System/2.jpg" class="img-thumbnail" >
</div>

As part of a miniature urban infrastructure project, I developed a SCADA (Supervisory Control and Data Acquisition) Water/Oil system that demonstrates automated fluid management. The system consists of two reservoirs connected via a transfer tube, with only one tank active at any given time. A Raspberry Pi serves as the central control unit, managing the fluid circulation between the tanks positioned at opposite ends of the structure.

<div class="text-center p-4">
  <img width="400px" src="../img/projects/SCADA-Water-System/circuit2.png" class="img-thumbnail" >
</div>

My contribution focused on both the electronic circuit design and Raspberry Pi programming. The system employs dual water level sensors interfaced with the Raspberry Pi to determine optimal pump activation timing. Each reservoir is equipped with a dedicated pump and LED status indicator for real-time operational feedback.

The following Python code demonstrates the control logic for the pump relay system:

```py
import RPi.GPIO as GPIO
import time

GPIO.setmode(GPIO.BCM)

GPIO.setup(2, GPIO.IN, pull_up_down=GPIO.PUD_DOWN)  # Tank 1 Sensor
GPIO.setup(3, GPIO.IN, pull_up_down=GPIO.PUD_DOWN)  # Tank 2 Sensor
GPIO.setup(14, GPIO.OUT)                            # Output To Relay 1 (Pump 1)
GPIO.setup(15, GPIO.OUT)                            # Output To Relay 2 (Pump 2)

try:
    GPIO.output(14,0)
    while True:
        if (GPIO.input(2) == GPIO.LOW):     # Tower Tank Top Sensor Cover With Water
            GPIO.output(14,0)               # Close The Relay 1 (Pump 1 ON)
            GPIO.output(15,1)               # Open The Relay 2 (Pump 2 OFF)
            print("Pump 1 [ON], Pump 2 [OFF]")
        elif (GPIO.input(3) == GPIO.HIGH):  # Tower Tank Bot Sensor Not Cover With Water
            GPIO.output(14,1)               # Open The Relay 1 (Pump 1 OFF)
            GPIO.output(15,0)               # Close The Relay 2 (Pump 2 ON)
            print("Pump 1 [OFF], Pump 2 [ON]")
        time.sleep(0.1)

finally:
    GPIO.cleanup()
```
