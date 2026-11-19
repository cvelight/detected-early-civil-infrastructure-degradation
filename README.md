# detected-early-civil-infrastructure-degradation

Electronic Components Course work

below are screenshots of the work

<img width="988" height="506" alt="Screenshot 2026-11-18 at 15 23 45" src="https://github.com/user-attachments/assets/339c9e82-6ed3-4059-a1d5-7b395e849530" />

The simulation is built using an Arduino Uno, a vibration sensor, LEDs, resistors, and a buzzer.

The vibration sensor detects movements and sends signals to the Arduino. The Arduino processes the data and activates the LEDs or buzzer when unusual vibrations are detected.

The circuit demonstrates a basic early-warning system for monitoring structural vibrations.

COURSE WORK PDF
[Uploading Document 2 (4).pdf…]() 


The Structural Vibration Health Tracker is a robotics project designed to monitor vibrations in buildings, bridges, and other civil infrastructure.

The main idea is to use vibration sensors to detect unusual movements or vibrations in structures. These changes may indicate possible damage or structural weaknesses.

The purpose of this project is to help identify potential infrastructure problems at an early stage, improve safety, and reduce the risk of serious structural failures.

The system collects vibration data using sensors and processes the information through a microcontroller (Arduino). If unusual vibration levels are detected, the system can trigger an alert using LEDs or a buzzer.

The project demonstrates how robotics and sensor technology can be used for structural health monitoring and early warning systems.

<img width="1413" height="1000" alt="IMAGE 2026-11-18 15:49:25" src="https://github.com/user-attachments/assets/93b8def1-7d5a-4183-b973-95e1f2745855" />



The Arduino program monitors structural vibrations using a vibration sensor. It counts vibration events within a five-second interval and compares them with a predefined threshold. If excessive vibration is detected, the system activates a red LED and buzzer as a warning. Otherwise, the green LED indicates normal conditions.


const int vibrationSensor = 2;
const int greenLED = 3;
const int redLED = 4;
const int buzzer = 10;

int vibrationCount = 0;
int lastSensorState = HIGH;

unsigned long lastDetectionTime = 0;
unsigned long startTime = 0;

const unsigned long monitoringPeriod = 5000;
const unsigned long debounceDelay = 50;

const int vibrationThreshold = 3;

void setup() {
pinMode(vibrationSensor, INPUT_PULLUP);
pinMode(greenLED, OUTPUT);
pinMode(redLED, OUTPUT);
pinMode(buzzer, OUTPUT);

Serial.begin(9600);

digitalWrite(greenLED, HIGH);
digitalWrite(redLED, LOW);
noTone(buzzer);

startTime = millis();

Serial.println("Structural Vibration Health Tracker");
Serial.println("System started...");
}

void loop() {
int sensorState = digitalRead(vibrationSensor);


if (sensorState == LOW &&
lastSensorState == HIGH &&
millis() - lastDetectionTime > debounceDelay) {
vibrationCount++;
lastDetectionTime = millis();

Serial.println("Vibration detected!");
}

lastSensorState = sensorState;

if (millis() - startTime >= monitoringPeriod) {
Serial.print("Vibration count: ");
Serial.println(vibrationCount);

if (vibrationCount >= vibrationThreshold) {
  
  digitalWrite(greenLED, LOW);
  digitalWrite(redLED, HIGH);
  tone(buzzer, 1000);

  Serial.println("WARNING: High vibration detected!");
  Serial.println("Check structural condition.");
} 
else {
 
  digitalWrite(greenLED, HIGH);
  digitalWrite(redLED, LOW);
  noTone(buzzer);

  Serial.println("Status: NORMAL");
}

vibrationCount = 0;
startTime = millis();
}
}


For the development of the Structural Vibration Health Tracker, I chose C++ as the primary programming language because it is widely used in robotics, embedded systems, and microcontroller-based projects. Since this project is built around an Arduino microcontroller, C++ is a suitable and practical choice for controlling electronic components and processing sensor data.

1. Compatibility with Arduino
   
Arduino uses a programming framework based on C and C++. Its development environment (Arduino IDE) supports C++ syntax and provides built-in libraries and functions that simplify hardware programming.
This makes C++ directly compatible with the Arduino board used in my project. It allows the program to communicate with the vibration sensor, LEDs, and buzzer without requiring additional software platforms.

2. Direct Hardware Control
   
One of the most important reasons for choosing C++ is its ability to interact directly with electronic hardware.
In this project, several Arduino functions are used:
pinMode() — configures Arduino pins as inputs or outputs.
digitalRead() — reads signals received from the vibration sensor.
digitalWrite() — controls the green and red LEDs.
tone() — generates an audible warning through the buzzer.
Serial.println() — displays sensor information and system status in the Serial Monitor.
These functions allow the microcontroller to receive information from the environment and respond to it automatically.

3. Real-Time Data Processing
   
The main purpose of the project is to detect unusual vibration activity in a structure.
C++ allows the Arduino to continuously monitor the vibration sensor, count detected vibration events, and compare the results with a predefined threshold.
For example, the system analyzes the number of detected vibrations within a five-second interval. If the number reaches or exceeds the defined threshold, the program activates the warning system.
This ability to process sensor signals and respond quickly is important for embedded systems and real-time monitoring applications.

4. High Performance and Efficiency
   
Arduino boards have limited memory and processing capabilities compared to computers. Therefore, the programming language must be efficient and suitable for resource-constrained devices.
C++ is a compiled language, which means that the source code is translated into machine code before execution. This allows programs to run efficiently with relatively low memory and processing requirements.
This makes C++ appropriate for small electronic devices that need to operate continuously.

5. Automation and Decision-Making
    
Another advantage of C++ is that it supports logical operations, conditional statements, loops, and functions.
In my project, these programming features are used to create an automated monitoring system:
The sensor continuously detects vibrations.
The program collects and counts vibration events.
The collected data is compared with a predefined threshold.
The system determines whether the detected vibration level is normal or potentially abnormal.
LEDs and the buzzer provide visual and audible feedback.
This allows the system to operate automatically without requiring constant human supervision.

6. Future Development Possibilities

C++ also provides opportunities to expand the project in the future.
Additional features could include:
Integration of more accurate vibration sensors.
Monitoring vibration intensity and frequency.
Recording sensor data over longer periods.
Adding an LCD display to show the current system status.
Connecting the system to wireless communication modules such as Wi-Fi or Bluetooth.
Sending alerts to a computer or mobile device.
These improvements could transform the basic prototype into a more advanced structural monitoring system.

Conclusion
In conclusion, C++ was selected because of its compatibility with Arduino, efficient hardware control, fast execution, and ability to process sensor data in real time.
It provides all the essential programming tools required for the Structural Vibration Health Tracker.
The use of C++ makes it possible to connect software with physical electronic components and create an automated system that detects unusual vibration activity and provides warning signals. Therefore, C++ is an appropriate programming language for this robotics project.
