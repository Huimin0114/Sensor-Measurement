# Introduction
The MPU-6050 is a 6-axis(combines 3-axis Gyroscope, 3-axis Accelerometer) motion tracking devices. It also includes a Digital Motion Processor™ (DMP) capable of processing complex 9-axis MotionFusion algorithms. 

The MPU6050 communicates via I2C protocol, making it compatible Mega 2560 Board. It operates at a voltage of 3.3V but can be used with 5V systems using a logic level converter. The module's key characteristics include sensitivity,  resolution, and power consumption, essential for determining its suitability for various applications.

<img width="202" alt="image" src="https://github.com/Huimin0114/Sensor-Measurement/assets/161892823/075494ee-c521-4e8c-a3c4-6e46e9810f5d">

# Background
An accelerometer is a device that measures acceleration. For example, an accelerometer at rest on the surface of the Earth will measure an acceleration due to Earth's gravity of g ≈ 9.81 m/s². In a typical implementation a mass is hung with one degree of freedom; it moves due to acceleration. The displacement (u) of the mass is linear with the force (F/u=C) on it, so displacement gives force (F). The force (F) is linear with the acceleration (F=m×a), so the force gives the acceleration (a). Integrating acceleration in time gives speed (v) and integrating speed in time gives traveled distance. Accelerometers are used in mobile phones and digital cameras so that images on screens are always displayed upright. Accelerometers are used in drones for flight stabilisation and for drop detection.

A gyroscope is a device used for measuring or maintaining orientation. A typical implementation is a spinning wheel in which the axis of rotation is free to assume any orientation by itself. Applications of gyroscopes include navigation systems.

Gyroscope suffer from drift; accelerometers are used to compensate for that.
