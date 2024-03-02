# Ultrasonic Sensor Module HC-SR04

The HC-SR04 ultrasonic sensor uses sonar to determine distance to an object like bats or dolphins do. It offers excellent non-contact range detection with high accuracy and stable readings in an easy-to-use package. From 2cm to 400 cm or 1" to 13 feet. It operation is not affected by sunlight or black material like Sharp rangefinders are (although acoustically soft materials like cloth can be difficult to detect). It comes complete with ultrasonic transmitter and receiver module.

## Explanation
  The HC-SR04 module contains two main parts: an ultrasonic transmitter and a receiver. When the module receives the signal, it will immediately transmit an ultrasonic wave. This wave travels through the air and, if it meets any object, it will reflect back and pick up by the receiver on the module. After the receiver receives this wave, the module will send a signal and calculate the distance between the module and the object. To get the characteristics, we need to Fix the sensor in one position, then place the target object at different distances to get the data.

## Wiring Diagrams and Pictures of Actual Experiment Setup
<img width="425" alt="image" src="https://github.com/Huimin0114/Sensor-Measurement/assets/161894946/132b7b75-7da3-4dee-a2bf-027127962fa2"> <img width="409" alt="image" src="https://github.com/Huimin0114/Sensor-Measurement/assets/161894946/54015007-a358-4378-81dd-296f93a151c0">

## Arduino Codes
<pre><code>
const int echoPin = 4;

const int trigPin = 5;


void setup(){

  Serial.begin(9600);
  
  pinMode(echoPin, INPUT);
  
  pinMode(trigPin, OUTPUT);
  
  Serial.println("Ultrasonic sensor:");  
}

void loop(){

  float distance = readSensorData();
  
  Serial.print(distance);
  
  Serial.println(" cm");
  
  delay(400);
}

float readSensorData(){

  digitalWrite(trigPin, LOW); 
  
  delayMicroseconds(2);
  
  digitalWrite(trigPin, HIGH); 
  
  delayMicroseconds(10);
  
  digitalWrite(trigPin, LOW);  
  
  float distance = pulseIn(echoPin, HIGH)/58.00;  //Equivalent to (340m/s*1us)/2
  
  return distance;
}
</code>code></pre>pre>

## Measured Data and Analysis
### Data Sheet

<img width="887" alt="1709336161911" src="https://github.com/Huimin0114/Sensor-Measurement/assets/161894946/618747e7-c882-4911-b4a5-28a593546aea">


### 1.Range

Experimental operation：Fix the sensor in one position, then place the target object at different distances (from 2 cm to 400 cm), and record whether the sensor can successfully measure the distance.

Conclusion: The measurement range of HC-SR04 is approximately 2cm to 400cm, which is consistent with the data in the data sheet.

<img width="41" alt="08f412c5724f4ef1f9d8453e6cbbaca" src="https://github.com/Huimin0114/Sensor-Measurement/assets/161894946/8c62d460-77dc-4203-90ff-1a964ebbe672"> <img width="52" alt="e9ac55744198a9959d2a04ad14e9246" src="https://github.com/Huimin0114/Sensor-Measurement/assets/161894946/ec90507a-b7d6-47a3-99a0-7d620c1329bd">


### 2.Resolution

Experimental operation：Slightly change the position of the target object and check whether the sensor can detect  this change. 

Conclusion: The minimum error of HC-SR04 after changing the distance is about 0.3cm, which is consistent with the value of the data sheet.

<img width="470" alt="image" src="https://github.com/Huimin0114/Sensor-Measurement/assets/161894946/4d0432b6-bb93-42ab-98f8-cc510130906b">

### 3.Static Error

Experimental operation Measure several times at a known distance and compare the measured values with the  actual values to determine the static error.

Conclusion: The error between the measured value and the actual value is smaller than 0.1cm which is the same data as the data sheet.

<img width="357" alt="image" src="https://github.com/Huimin0114/Sensor-Measurement/assets/161894946/18cfb9ec-c14e-44f1-b9fe-5e2aa73a0dd1"> <img width="366" alt="image" src="https://github.com/Huimin0114/Sensor-Measurement/assets/161894946/50c3fd6b-3bcd-425a-8857-47909b0da717">

## Summarized final results and discussions
  The final results of the experiment with the HC-SR04 ultrasonic sensor module demonstrated that the sensor's performance closely aligns with the manufacturer's datasheet specifications. The experiment confirmed the sensor's range to be approximately 2 cm to 400 cm, with a resolution allowing for detection of distance changes as small as 0.3 cm. Static error tests showed a minimal discrepancy between measured values and actual distances, indicating high accuracy. Challenges such as incorrect measurements and program operation issues were encountered but did not significantly impact the overall success of the experiment.























