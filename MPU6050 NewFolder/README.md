# Introduction
The MPU-6050 is a 6-axis(combines 3-axis Gyroscope, 3-axis Accelerometer) motion tracking devices. It also includes a Digital Motion Processor™ (DMP) capable of processing complex 9-axis MotionFusion algorithms. 

<img width="202" alt="image" src="https://github.com/Huimin0114/Sensor-Measurement/assets/161892823/d980f560-0d5e-4c56-8ea5-ba49a90c720f">


The MPU6050 communicates via I2C protocol, making it compatible Mega 2560 Board. It operates at a voltage of 3.3V but can be used with 5V systems using a logic level converter. The module's key characteristics include sensitivity,  resolution, and power consumption, essential for determining its suitability for various applications.

<img width="202" alt="image" src="https://github.com/Huimin0114/Sensor-Measurement/assets/161892823/075494ee-c521-4e8c-a3c4-6e46e9810f5d">

# Background
An accelerometer is a device that measures acceleration. For example, an accelerometer at rest on the surface of the Earth will measure an acceleration due to Earth's gravity of g ≈ 9.81 m/s². In a typical implementation a mass is hung with one degree of freedom; it moves due to acceleration. The displacement (u) of the mass is linear with the force (F/u=C) on it, so displacement gives force (F). The force (F) is linear with the acceleration (F=m×a), so the force gives the acceleration (a). Integrating acceleration in time gives speed (v) and integrating speed in time gives traveled distance. Accelerometers are used in mobile phones and digital cameras so that images on screens are always displayed upright. Accelerometers are used in drones for flight stabilisation and for drop detection.

A gyroscope is a device used for measuring or maintaining orientation. A typical implementation is a spinning wheel in which the axis of rotation is free to assume any orientation by itself. Applications of gyroscopes include navigation systems.

Gyroscope suffer from drift; accelerometers are used to compensate for that.

<img width="213" alt="image" src="https://github.com/Huimin0114/Sensor-Measurement/assets/161892823/e9ec1e55-b7b2-465a-82f7-352b962c6f56">
<img width="446" alt="image" src="https://github.com/Huimin0114/Sensor-Measurement/assets/161892823/73cd4688-d7a4-4af1-ac1b-bfcee8122a1a">
<img width="392" alt="image" src="https://github.com/Huimin0114/Sensor-Measurement/assets/161892823/1cb9b075-d146-4584-815e-8d34801d7580">

# Dashsheet
<img width="590" alt="7ce8667502ab322dde17dfb75ffa665" src="https://github.com/Huimin0114/Sensor-Measurement/assets/161892823/d9bbb930-bdb4-4c60-9acd-6b726a9f229f">

# Getting started
•Materials: one MPU6050 module, one Mega 2560 board, one breadboard, one adhesive tape and six wires.

•Using jumper wires, connect the VCC pin of the MPU6050 to the 5V output on the Arduino Mega 2560.

•Connect the GND pin to one of the GND pins on the Arduino.

•Attach the SDA (Serial Data) pin of the MPU6050 to the SDA pin on the Arduino.

•Attach the SCL (Serial Clock) pin of the MPU6050 to the SCL pin on the Arduino.

<img width="523" alt="1709336829495" src="https://github.com/Huimin0114/Sensor-Measurement/assets/161892823/b7ecd5a9-b6d9-42c0-9243-06ec864d0537">


![image](https://github.com/Huimin0114/Sensor-Measurement/assets/161892823/77272d7d-0653-4dd1-a862-81137e6c9beb)

<img width="687" alt="c66b46f960a0d10cc7f6396e25df23a" src="https://github.com/Huimin0114/Sensor-Measurement/assets/161892823/72cef846-0612-44e2-8080-3ee1783f3f0c">


# Secure MPU6050 to Breadboard:

•Take a piece of adhesive tape that is suitable in length to hold the MPU6050 module.

•Place the MPU6050 on the breadboard in the desired location, ensuring that it lies flat and none of the pins are bent.

•Apply the adhesive tape over the MPU6050 module, pressing firmly to adhere it to the breadboard without covering any of the pin headers or interfering with the pin connections.

<img width="294" alt="image" src="https://github.com/Huimin0114/Sensor-Measurement/assets/161892823/cef593ba-6901-4365-8b3a-13c465ac6f0d">


