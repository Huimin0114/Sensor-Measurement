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
 * Test plan:
 
Purpose: To evaluate the accuracy of the DHT-11 sensor in measuring temperature and humidity by comparing its readings.

Reference Standard: the accuracy is ±5%RH and ±2℃.

Testing Environment: I will test them in a controlled environment that allows for temperature and humidity adjustments (0 to 50°C for temperature and 20% to 80%RH for humidity).

* Method:
1.Let the environment's temperature and humidity to stable for at least 30 minutes at each test point.
2.Record temperature and humidity readings from both the DHT-11 and the reference instrument simultaneously.
3.Repeat measurements across various temperature and humidity points to comprehensively assess the DHT-11's performance.
 






