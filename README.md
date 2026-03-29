# Self Balancing Robot 🤖
> **What is this?**

A self-balancing robot is a two-wheeled robot that stays upright on its own — just like a Segway. It constantly reads its tilt angle using a gyroscope/accelerometer sensor (MPU6050), calculates how far it has leaned from the upright position, and drives its motors to correct itself in real time.
The brain behind this correction is a PID controller — a control algorithm used everywhere from drones to industrial machines. It makes the robot react fast, stay stable, and correct small drifts over time.

# Workflow
<img width="1616" height="578" alt="Workflow" src="https://github.com/user-attachments/assets/1109f280-680c-42a7-91a6-9524d71af5f8" />

**1. MPU6050 reads the tilt angle every 5ms**

**2. Complementary filter smooths the angle reading**

**3. PID controller calculates how much motor power is needed**

**4. Motors correct the lean direction**

**5. Repeat — 200 times per second**

#Components Used

