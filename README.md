# 🤖 RC Bluetooth Car Using Arduino

A simple DIY project that allows you to build and control a robotic car using Arduino and Bluetooth technology. This project demonstrates how to create a smartphone-controlled robot using affordable and easily available components.

## 📱 Project Overview

This project uses an Android app to send commands over Bluetooth to an Arduino-based robotic car. The robot is capable of:

- Moving **Forward**
- Moving **Backward**
- Turning **Left**
- Turning **Right**
- **Stopping**
- Controlling speed via commands
- Activating lights and a buzzer

## 🔧 Components Used

- Arduino UNO
- HC-05 Bluetooth Module
- L298N Motor Driver
- 4 DC Geared Motors
- Robot Chassis
- Android Smartphone with Bluetooth Controller App
- Jumper Wires, Power Supply

## ⚙️ System Design

- **Bluetooth Module (HC-05)** is connected to Arduino's software serial pins.
- **L298N Motor Driver** receives movement commands via digital pins (D9 to D12).
- **Motors** are split into left and right sets and connected to the motor driver.
- A custom Android app sends commands like `'F'`, `'B'`, `'L'`, `'R'`, etc. to move the car accordingly.

## 📜 Arduino Code Highlights

```cpp
#define in1 5
#define in2 6
#define in3 10
#define in4 11

int command;
int Speed = 240;

void setup() {
  pinMode(in1, OUTPUT);
  pinMode(in2, OUTPUT);
  pinMode(in3, OUTPUT);
  pinMode(in4, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  if (Serial.available() > 0) {
    command = Serial.read();
    Stop();  // Default state
    switch (command) {
      case 'F': forward(); break;
      case 'B': back(); break;
      case 'L': left(); break;
      case 'R': right(); break;
      case '0': Speed = 100; break;
      case 'q': Speed = 255; break;
      // Additional controls omitted for brevity
    }
  }
}
