# detected-early-civil-infrastructure-degradation

Electronic Components Course work

below are screenshots of the work

<img width="988" height="506" alt="Screenshot 2026-11-18 at 15 23 45" src="https://github.com/user-attachments/assets/339c9e82-6ed3-4059-a1d5-7b395e849530" />

The main purpose of my project is to develop a vibration monitoring system that can detect unusual vibrations in structures such as bridges, buildings, and other civil infrastructure. Excessive or abnormal vibrations may indicate structural problems, material fatigue, or potential damage.
The system uses an Arduino microcontroller to process sensor input and provides visual and audio warnings when vibration levels exceed a predefined threshold.
Below is a detailed explanation of each component and why it is included in the project.

<img width="1170" height="845" alt="IMAGE 2026-11-21 20:05:43" src="https://github.com/user-attachments/assets/568442f1-ddc0-439e-ae6d-720193cbcbf3" />

The main component is the Arduino Uno R3, which acts as the brain of the system. It receives signals from the vibration sensor, processes the data, and controls the other components according to the programmed instructions.

<img width="1024" height="1024" alt="IMAGE 2026-11-21 20:09:29" src="https://github.com/user-attachments/assets/12d47a4e-6cbb-4700-b8a8-d32be784ede2" />


The SW-420 vibration sensor is responsible for detecting mechanical vibrations and movements. It sends digital signals to the Arduino whenever vibration is detected. The Arduino analyzes the number of vibration events within a specific period and compares the results with a predefined threshold. This allows the system to distinguish between normal and potentially abnormal vibration activity.

<img width="600" height="600" alt="IMAGE 2026-11-21 20:10:20" src="https://github.com/user-attachments/assets/ce2ce217-32ff-40aa-92d4-e61a5c0fc953" />


The project also includes two LEDs: a green LED and a red LED. The green LED indicates normal operating conditions when vibration activity remains below the established threshold. The red LED indicates a warning condition when excessive vibration is detected. These visual indicators make it easier to understand the system’s status.

<img width="640" height="363" alt="IMAGE 2026-11-21 20:11:23" src="https://github.com/user-attachments/assets/1ac53f28-9507-43de-b809-3aed684020aa" />


A piezo buzzer is included as an additional warning component. It produces an audible alarm when the vibration level exceeds the predefined limit. This is useful because it attracts attention even when someone is not directly looking at the monitoring system.

<img width="1408" height="768" alt="IMAGE 2026-11-21 20:12:18" src="https://github.com/user-attachments/assets/bfb842eb-b408-4b61-a114-719439a273d5" />

Resistors (220–330 ohms) are used to limit the electrical current flowing through the LEDs and protect them from damage. A breadboard is used to assemble the circuit without soldering, making connections easier to modify and test. Finally, jumper wires connect all electronic components and provide the necessary electrical connections between the Arduino, sensor, LEDs, and buzzer.


All components work together as one monitoring system. The sensor detects vibrations, the Arduino processes the signals, and the LEDs and buzzer communicate the system’s status. The prototype demonstrates how microcontrollers and electronic sensors can be used for basic structural health monitoring and early warning applications.

The project is designed as a simplified prototype and does not directly diagnose structural damage. Instead, it identifies unusual vibration activity that may require further inspection.


COURSE WORK PDF
[Uploading Document 2 (4).pdf…]() 




<img width="1413" height="1000" alt="IMAGE 2026-11-18 15:49:25" src="https://github.com/user-attachments/assets/93b8def1-7d5a-4183-b973-95e1f2745855" />

In conclusion, the Structural Vibration Health Tracker demonstrates how electronic components, sensors, and microcontrollers can be combined to create a basic structural monitoring system. The project successfully illustrates the principle of detecting unusual vibrations and generating visual and audio warnings. By using an Arduino Uno, a vibration sensor, LEDs, and a buzzer, the system provides a simple way to monitor vibration activity and identify potentially abnormal conditions.

This project helped develop a better understanding of electronics, circuit connections, programming, and the practical applications of robotics in civil engineering. Although the prototype has certain limitations and cannot independently determine the actual condition of a building or bridge, it demonstrates the potential of automated monitoring systems. In the future, the project could be improved by using more accurate sensors, collecting real-time data, adding wireless communication, and implementing data analysis to make structural monitoring more reliable and effective.


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
