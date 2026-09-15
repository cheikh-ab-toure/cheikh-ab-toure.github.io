---
layout: post
title: Smart Parking Assistant
description: A real-time ultrasonic distance-sensing system built on an Arduino, simulating a vehicle parking sensor with tiered visual and audio feedback.
skills: 
- Circuit Analysis
- Embedded Systems
- Microcontroller Programming
- Sensor Integration
- Real-Time Monitoring & Control
main-image: /t725.png
---

---
# Objective
I designed and programmed a distance-sensing system using an HC-SR04 ultrasonic sensor and an ELEGOO UNO R3 microcontroller that delivers real-time visual and auditory feedback based on proximity zones, simulating the behavior of a modern vehicle parking sensor. This project was built for ECEN 102 under Dr. Walter M. Gilmore.

{% include image-gallery.html images="breadboard-wiring.png, breadboard-active.png" height="400" %}

# How It Works: Time-of-Flight

The system relies on Time-of-Flight (ToF), a measurement technique that determines distance by timing how long a signal takes to travel from a source to a target and back to a receiver. The HC-SR04 applies this principle with ultrasonic sound waves instead of light.

When the Arduino sends a 10 µs HIGH pulse to the sensor's Trig pin, the sensor emits an 8-pulse burst at 40,000 Hz. These pulses travel outward, reflect off a surface, and return. The Echo pin stays HIGH for exactly the round-trip travel time, which the Arduino reads using pulseIn().

It's the same principle bats use for echolocation — emit a pulse, wait for the reflection, infer distance from timing — and the same physics behind radar and sonar systems in aerospace and autonomous vehicles.

# The Math

The speed of sound in dry air at 20°C is:

V = 343 m/s

More precisely, it's temperature-dependent:

V = 331.3 + (0.606 × T) m/s

where T is temperature in °C — for every 1°C increase, the speed of sound rises by about 0.6 m/s, meaning sensor readings drift slightly with temperature.

Converting to the units the Arduino formula needs (cm/µs):

343 m/s × 100 cm × (1 s / 1,000,000 µs) = 0.0343 cm/µs ≈ 0.034 cm/µs

# Zone Logic

The sensing range is divided into three proximity zones:

| Zone | Condition | Green LED | Yellow LED | Red LED | Buzzer |
|----------|----------||----------|----------||----------|----------|
| Row 1, Col 1 | Row 1, Col 2 | Row 1, Col 1 | Row 1, Col 2 | Row 1, Col 1 | Row 1, Col 2 |
| Row 2, Col 1 | Row 2, Col 2 | Row 1, Col 1 | Row 1, Col 2 | Row 1, Col 1 | Row 1, Col 2 |

# Error Analysis

The HC-SR04 datasheet specifies ±3 mm accuracy under ideal conditions, which introduces measurable error at each zone boundary:

At the Safe/Caution boundary (20 cm): 1.5% error
At the Caution/Stop boundary (10 cm): 3.0% error

This means a reading near 10 cm could register anywhere from 9.7 cm to 10.3 cm, potentially causing the zone to flicker between Caution and Stop. Because the code uses a fixed constant of 0.034 cm/µs based on 20°C, any significant shift in ambient temperature also introduces systematic error.

# Conclusion

This project demonstrated the Time-of-Flight principle using acoustic waves for distance measurement. The three-zone feedback mechanism — visual via LEDs, auditory via buzzer — accurately simulated a vehicle parking sensor across the full measurement range. Key limitations are the temperature dependence of the speed of sound and the sensor's ±3 mm accuracy, both of which produce measurable error, particularly near zone boundaries.
