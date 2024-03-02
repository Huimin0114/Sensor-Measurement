# DHT-11 Module 
# Introduction
 The DHT11 is a basic, ultra low-cost digital temperature and humidity sensor. It uses a capacitive humidity sensor and a thermistor to measure the surrounding air, and spits out a digital signal on the data pin (no analog input pins are needed).
 
![image](https://github.com/Huimin0114/Sensor-Measurement/assets/161893598/9baae72e-b110-4443-8948-cf5e8316f980)
# Wiring Diagrams and Pictures of Actual Experiment Setup

In this example, we can directly connect the pins of DHT11 Module to the pins of Mega 2560 Board, and we use pin 4 to read the signal of DHT11 Module. Connect the pin「+」of DHT11 Module to 5V, the pin「-」 to GND, and the pin OUT to pin 4.

![image](https://github.com/Huimin0114/Sensor-Measurement/assets/161893598/85097740-6d5d-4cf7-bd81-84ce10d03f69)!![image](https://github.com/Huimin0114/Sensor-Measurement/assets/161893598/c7d242cf-a51f-453e-b6e4-b003de7416d6)

# Specification table
![image](https://github.com/Huimin0114/Sensor-Measurement/assets/161893598/c0726ff7-c7cf-41e2-91a2-22cafaf618e7)

# Arduino code
<pre><code>
#include "DHT.h"

#define DHTPIN 4  // Set the pin connected to the DHT11 data pin
#define DHTTYPE DHT11 // DHT 11 

DHT dht(DHTPIN, DHTTYPE);

void setup() {
  Serial.begin(9600);
  Serial.println("DHT11 test!");
  dht.begin();
}

void loop() {
  // Wait a few seconds between measurements.
  delay(2000);

  // Reading temperature or humidity takes about 250 milliseconds!
  // Sensor readings may also be up to 2 seconds 'old' (it's a very slow sensor)
  float humidity = dht.readHumidity();
  // Read temperature as Celsius (the default)
  float temperature = dht.readTemperature();

  // Check if any reads failed and exit early (to try again).
  if (isnan(humidity) || isnan(temperature)) {
    Serial.println("Failed to read from DHT sensor!");
    return;
  }
  // Print the humidity and temperature
  Serial.print("Humidity: "); 
  Serial.print(humidity);
  Serial.print(" %\t");
  Serial.print("Temperature: "); 
  Serial.print(temperature);
  Serial.println(" *C");
}
</code></pre>

 # Accuracy
 * Test plans:
 
Purpose: To evaluate the accuracy of the DHT-11 sensor in measuring temperature and humidity by comparing its readings.

Reference Standard: the accuracy is ±5%RH and ±2℃.

Testing Environment: I will test them in a controlled environment that allows for temperature and humidity adjustments (0 to 50°C for temperature and 20% to 80%RH for humidity).

* Method:

1.Let the environment's temperature and humidity to stable for at least 30 minutes at each test point.

2.Divide the measurements into  four groups , with an interval of five minutes between each group.

3.Record temperature and humidity readings from both the DHT-11 and the reference instrument simultaneously.  

4.Repeat measurements across various temperature and humidity points to comprehensively assess the DHT-11's performance.

* Testing figure

![image](https://github.com/Huimin0114/Sensor-Measurement/assets/161893598/487f5896-1090-4eb1-a013-582cb61c3daa)

![image](https://github.com/Huimin0114/Sensor-Measurement/assets/161893598/1910b7ba-eb37-4a92-a2e1-7a673fb1d92a)

![image](https://github.com/Huimin0114/Sensor-Measurement/assets/161893598/eba21d6c-7d99-47a5-b9ac-d7413b1fe471)

![image](https://github.com/Huimin0114/Sensor-Measurement/assets/161893598/3b40491e-f561-40b0-acf2-da46c71a6826)

# Matlab code
I will use the matlab to caculate the error

 * Matlab code of humidity

<pre><code>
% Define the humidity data
dht11_readings = {
    repmat(29.9, 1, 10),  % Group 1: 10 readings of 29.9%
    repmat(30.0, 1, 10),  % Group 2: 10 readings of 30%
    [repmat(29.8, 1, 7), repmat(29.9, 1, 3)],  % Group 3: 7 readings of 29.8% and 3 readings of 29.9%
    [repmat(29.9, 1, 7), repmat(30.0, 1, 3)]   % Group 4: 7 readings of 29.9% and 3 readings of 30%
};
true_humidity = [31, 30, 30, 30];  % True humidity values

% Calculate the average humidity readings for each group
avg_dht11_readings = cellfun(@mean, dht11_readings);

% Calculate the humidity errors for each group
humidity_errors = avg_dht11_readings - true_humidity;

% Calculate the average error
avg_error = mean(humidity_errors);

% Calculate the standard deviation of the errors
std_dev = std(humidity_errors);

% Display the results
fprintf('Average error (accuracy): %.3f%%\n', avg_error);
fprintf('Standard deviation of humidity errors: %.3f%%\n', std_dev);
</code></pre>

 * Matlab code of Temperature 
<pre><code>
% Define the temperature data
dht11_temperatures = {
    repmat(28.1, 1, 10), % Group 1: 10 readings of 28.1°C
    repmat(28.1, 1, 10), % Group 2: 10 readings of 28.1°C
    [repmat(28.1, 1, 9), 28.0], % Group 3: 9 readings of 28.1°C and 1 reading of 28°C
    [repmat(28.1, 1, 5), repmat(28.0, 1, 5)] % Group 4: 5 readings of 28.1°C and 5 readings of 28°C
};
true_temperatures = [27.22, 27.78, 27.22, 27.22]; % True temperature values

% Calculate the average temperature readings for each group
avg_dht11_temperatures = cellfun(@mean, dht11_temperatures);

% Calculate the temperature errors for each group
temperature_errors = avg_dht11_temperatures - true_temperatures;

% Calculate the average error
avg_error = mean(temperature_errors);

% Calculate the standard deviation of the errors
std_dev = std(temperature_errors);

% Display the results
fprintf('Average error (accuracy): %.3f°C\n', avg_error);
fprintf('Standard deviation of temperature errors: %.3f°C\n', std_dev);
</code></pre>

* Results

![image](https://github.com/Huimin0114/Sensor-Measurement/assets/161893598/99fbcaee-10d1-404a-b4c3-7c697f4d0b2f)

![image](https://github.com/Huimin0114/Sensor-Measurement/assets/161893598/f7a9fc88-532a-4a4a-bfe1-ac87642b52c6)

* Comparison
  
Based on the experimental results, we can observe that the average errors in both temperature and humidity measurements of the DHT-11 are within the specifications provided by the manufacturer(±5%RH and ±2℃), and the fluctuations are minimal. This indicates that the DHT-11 demonstrates good accuracy and consistency under the test conditions.

# Range
* Test plans :

Purpose:To assess the DHT-11 sensor's measurement  range for both temperature and humidity under controlled conditions.

Reference Standard：

1.Temperature Range：	 0°C to 50°C 

2.Humidity Range：	20% to 80%

Testing Environment: I will test them in a controlled environment that allows for temperature and humidity adjustments (0 to 50°C for temperature and 20% to 80%RH for humidity).

* Materials



1.High-accuracy reference hygrometer/thermometer (for temperature and humidity)

2.Humidifier and dehumidifier (for humidity variation)

3.Refrigerator and water kettle  (for temperature variation)

4.Enclosed testing environment

 * Testing figure

I changed it from an environment of 20 degrees Celsius to a refrigerator of 0 degrees Celsius and measured its temperature.

![image](https://github.com/Huimin0114/Sensor-Measurement/assets/161893598/fadce85d-0dc6-4c48-ba6a-d7b46d04d3a8)



