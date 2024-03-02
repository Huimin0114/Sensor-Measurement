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

# Code
Restart the Arduino IDE and Open File >  Libraries > MPU6050 > basic.

Make sure Tools > Board is Arduino Mega or Mega 2560, and Tools > Port has the correct COM9 port.

Select Sketch > Upload to compile and upload the code to the creator.

Open the  Tools > Serial Monitor and see the output

<pre><code>#define ACCELE_RANGE 4
#define GYROSC_RANGE 500

#include<Wire.h>
const int MPU_addr = 0x68; // I2C address of the MPU-6050
float AcX, AcY, AcZ, Tmp, GyX, GyY, GyZ;
void setup() {
  Wire.begin();
  Wire.beginTransmission(MPU_addr);
  Wire.write(0x6B);  // PWR_MGMT_1 register
  Wire.write(0);     // set to zero (wakes up the MPU-6050)
  Wire.endTransmission(true);
  Serial.begin(9600);
}
void loop() {
  Wire.beginTransmission(MPU_addr);
  Wire.write(0x3B);  // starting with register 0x3B (ACCEL_XOUT_H)
  Wire.endTransmission(false);
  Wire.requestFrom(MPU_addr, 14, true); // request a total of 14 registers
  AcX = Wire.read() << 8 | Wire.read(); // 0x3B (ACCEL_XOUT_H) & 0x3C (ACCEL_XOUT_L)
  AcY = Wire.read() << 8 | Wire.read(); // 0x3D (ACCEL_YOUT_H) & 0x3E (ACCEL_YOUT_L)
  AcZ = Wire.read() << 8 | Wire.read(); // 0x3F (ACCEL_ZOUT_H) & 0x40 (ACCEL_ZOUT_L)
  Tmp = Wire.read() << 8 | Wire.read(); // 0x41 (TEMP_OUT_H) & 0x42 (TEMP_OUT_L)
  GyX = Wire.read() << 8 | Wire.read(); // 0x43 (GYRO_XOUT_H) & 0x44 (GYRO_XOUT_L)
  GyY = Wire.read() << 8 | Wire.read(); // 0x45 (GYRO_YOUT_H) & 0x46 (GYRO_YOUT_L)
  GyZ = Wire.read() << 8 | Wire.read(); // 0x47 (GYRO_ZOUT_H) & 0x48 (GYRO_ZOUT_L)
  Serial.print(" AcX = "); Serial.print(AcX / 65536 * ACCELE_RANGE-0.01); Serial.print("g ");
  Serial.print(" | AcY = "); Serial.print(AcY / 65536 * ACCELE_RANGE); Serial.print("g ");
  Serial.print(" | AcZ = "); Serial.print(AcZ / 65536 * ACCELE_RANGE+0.02); Serial.println("g ");
  // Serial.print(" | Tmp = "); Serial.println(Tmp/340.00+36.53);  //equation for temperature in degrees C from datasheet
  Serial.print(" GyX = "); Serial.print(GyX / 65536 * GYROSC_RANGE+1.7); Serial.print("d/s ");
  Serial.print(" | GyY = "); Serial.print(GyY / 65536 * GYROSC_RANGE-1.7); Serial.print("d/s ");
  Serial.print(" | GyZ = "); Serial.print(GyZ / 65536 * GYROSC_RANGE+0.25); Serial.println("d/s \n");
  delay(500);
}
</code></pre>

# Repeatability

I taped the MPU6050 to the breadboard, then taped the breadboard and Mega2560 together at the bottom, then I assembled all the pieces at night when no one was around (no extra noise) and taped them to a treadmill conveyor belt, which I measured by adjusting the pace of the conveyor belt.

<img width="264" alt="image" src="https://github.com/Huimin0114/Sensor-Measurement/assets/161892823/d6af43af-4f66-47b7-a090-8b9c2bcfbe14">

#### When the conveyor belt speed is 0.2MPH

<img width="328" alt="image" src="https://github.com/Huimin0114/Sensor-Measurement/assets/161892823/afe7d781-c6f4-47ad-a382-35a73dfe81f2">

##### the data is shown below:

<img width="846" alt="a59cacf77d659dfe0c4e9c1504669a0" src="https://github.com/Huimin0114/Sensor-Measurement/assets/161892823/ed587615-2960-4695-99e9-caf1c873a9a0">


![image](https://github.com/Huimin0114/Sensor-Measurement/assets/161892823/6af87b12-40a5-4e33-84cc-99c971e41bbc)

##### then I use Excel to calculate

<img width="313" alt="1709342869016" src="https://github.com/Huimin0114/Sensor-Measurement/assets/161892823/97b8e503-b06c-4839-86f0-56e70c38e5ea">

#### When the conveyor belt speed is 0.5MPH

![image](https://github.com/Huimin0114/Sensor-Measurement/assets/161892823/5dc0c363-0d69-4f53-ac0b-ed7724f9d24a)

##### the data is shown below:

<img width="809" alt="1709343774847" src="https://github.com/Huimin0114/Sensor-Measurement/assets/161892823/15dac665-2bbf-44d6-a88b-ad0c8bdab0ef">


<img width="591" alt="0ef17535e2d3b1f5a64aa86a6a39b6b" src="https://github.com/Huimin0114/Sensor-Measurement/assets/161892823/d5257d44-114b-4c6a-a7f8-40f2c4a8818a">

##### then I use Excel to calculate

<img width="313" alt="1709342869016" src="https://github.com/Huimin0114/Sensor-Measurement/assets/161892823/9e5dddc4-6c16-43a7-9c80-da25e81c6d97">

# Linearity

I taped the MPU6050 to the breadboard, then taped the breadboard to the back of the phone, then laid it flat on a table, moved up nine sets at a degree of about 20, and recorded the data for comparison.

<img width="316" alt="image" src="https://github.com/Huimin0114/Sensor-Measurement/assets/161892823/6555f108-c984-4112-91ea-a27c1bc3f6d5">

![image](https://github.com/Huimin0114/Sensor-Measurement/assets/161892823/f71759f0-34c5-430a-ae7d-ca25aec5401f)

##### then I use Excel to record and draw a scott diagram

<img width="454" alt="image" src="https://github.com/Huimin0114/Sensor-Measurement/assets/161892823/f2683802-ff6f-4586-9163-b2046e6232be">

<img width="463" alt="image" src="https://github.com/Huimin0114/Sensor-Measurement/assets/161892823/d814f73b-ab43-4c3b-bc7b-f9c6ad260515">

From the diagram, we can find R² is very close to '1', which means they have a very strong linear relationship.

# Conclusion

Through a series of experiments on the MPU6050 6-axis motion tracking device, I conducted an in-depth test and analysis of its repeatability and linearity. By using the treadmill as an experimental platform, I successfully simulated the operating environment of the sensor at constant speed and evaluated the performance of the MPU6050 under different dynamic conditions by precisely adjusting the speed of the conveyor belt. The results showed that at speeds of 0.2MPH and 0.5MPH, the MPU6050 demonstrated good repeatability, and its accelerometer and gyroscope data maintained a high degree of consistency over repeated tests.

In addition, by conducting linearity tests by fixing the sensor to the back of the phone at different tilt angles, I found a strong linear relationship between the accelerometer output and the tilt Angle, with an R² value very close to 1. This demonstrates the MPU6050's high accuracy and reliability in measuring inclination, further confirming its potential for use in complex motion tracking and positioning systems.

All in all, while this work validates the performance of the MPU6050 to some extent, it also exposes limitations in the design and execution of the experiment. I recognize that there are many more performance characteristics and application scenarios to be explored for a sensor as complex as the MPU6050.
