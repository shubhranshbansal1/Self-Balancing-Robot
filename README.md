# Self Balancing Robot 🤖

A self-balancing robot is a two-wheeled robot that stays upright on its own — just like a Segway. It constantly reads its tilt angle using a gyroscope/accelerometer sensor (MPU6050), calculates how far it has leaned from the upright position, and drives its motors to correct itself in real time.
The brain behind this correction is a PID controller — a control algorithm used everywhere from drones to industrial machines. It makes the robot react fast, stay stable, and correct small drifts over time.

# Workflow
<img width="1616" height="578" alt="Workflow" src="https://github.com/user-attachments/assets/1109f280-680c-42a7-91a6-9524d71af5f8" />

**1. MPU6050 reads the tilt angle every 5ms**

**2. Complementary filter smooths the angle reading**

**3. PID controller calculates how much motor power is needed**

**4. Motors correct the lean direction**

**5. Repeat — 200 times per second**

# Components Used

## 1. Arduino Nano
The brain of the robot. Runs the PID loop, reads sensor data, and sends commands to the motor driver. Chosen over Uno for its compact size — critical for keeping the robot lightweight and balanced.

## 2. MPU6050 (IMU Sensor)
A 6-axis Inertial Measurement Unit that combines:

* **Accelerometer — measures tilt using gravity (slow but accurate)**

* **Gyroscope — measures rotation rate (fast but drifts over time)**

Both are blended together using a Complementary Filter to get a smooth, accurate angle.

Connected via I2C (SDA → A4, SCL → A5 on Nano).

## 3. TB6612FNG (Motor Driver)
Controls the speed and direction of both motors. Receives PWM signals from Arduino and drives the motors accordingly.
Why TB6612FNG over the popular L298N:

* No internal voltage drop (L298N wastes ~2V as heat)
* Much smaller and lighter
* Handles up to 13.5V — perfect for 11.1V Li-ion
* Cleaner PWM response for smoother balancing

## 4. N20 Gear Motor (12V, 300 RPM) × 2
Compact, high-torque gear motors that run perfectly on 11.1V.

* 300 RPM is the sweet spot for a ~15–20cm tall robot
* Too fast → overcorrects and oscillates
* Too slow → can't react in time and falls

## 5. 3S Li-ion Battery (11.1V)
Powers the entire system.

* 11.1V goes directly to the TB6612FNG motor driver
* An IC (Lm7805) steps it down to 5V for the Arduino Nano
* Never connect 11.1V directly to the Nano — it will fry it

# Full Wiring Diagram

<img width="680" height="784" alt="self_balancing_robot_wiring" src="https://github.com/user-attachments/assets/73967fd9-9b97-4431-9343-77ebd47109ad" />


