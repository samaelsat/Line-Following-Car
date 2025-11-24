# Line-Following-Car
 Autonomous line-following robot using Arduino, L298N motor driver, 2 TT gear motors &amp; 2 IR sensors. Detects and tracks black lines with real-time path correction. Features optimized PWM control for smooth movement. Simple logic: forward when clear, turn on line detection, stop when both sensors active. Perfect beginner robotics project.
# Arduino Line Following Robot Car 🚗

An autonomous robot that uses IR sensors to detect and follow a black line on a white surface. This project demonstrates basic robotics concepts including sensor integration, motor control, and autonomous navigation.

## 📋 Table of Contents
- [Features](#features)
- [Hardware Requirements](#hardware-requirements)
- [Circuit Diagram](#circuit-diagram)
- [How It Works](#how-it-works)
- [Usage](#usage)
- [Customization](#customization)
- [Troubleshooting](#troubleshooting)

## ✨ Features

- **Autonomous line tracking** using dual IR sensors
- **Real-time path correction** with instant motor response
- **Optimized PWM control** (7812.5 Hz) for smooth low-speed operation
- **Simple decision logic** easy to understand and modify
- **Adjustable speed** via single constant

## 🔧 Hardware Requirements

| Component | Quantity | Description |
|-----------|----------|-------------|
| Arduino Uno/Nano | 1 | Main microcontroller |
| L298N Motor Driver | 1 | Dual H-bridge for motor control |
| TT Gear Motors | 2 | DC motors with gearbox |
| IR Sensors | 2 | Infrared obstacle/line sensors |
| Robot Chassis | 1 | With wheels and mounting |
| Battery Pack | 1 | 7-12V (rechargeable recommended) |
| Jumper Wires | - | For connections |

## 🔌 Circuit Diagram

### Pin Connections

**IR Sensors:**
```
Right IR Sensor → Arduino Pin 11
Left IR Sensor  → Arduino Pin 12
VCC            → 5V
GND            → GND
```

**L298N Motor Driver - Right Motor:**
```
ENA (Enable) → Arduino Pin 6 (PWM)
IN1          → Arduino Pin 7
IN2          → Arduino Pin 8
OUT1 & OUT2  → Right Motor
```

**L298N Motor Driver - Left Motor:**
```
ENB (Enable) → Arduino Pin 5 (PWM)
IN3          → Arduino Pin 9
IN4          → Arduino Pin 10
OUT3 & OUT4  → Left Motor
```

**Power:**
```
L298N 12V    → Battery + (7-12V)
L298N GND    → Battery - & Arduino GND
Arduino VIN  → Battery + (or separate 5V supply)
```

## ⚙️ How It Works

The robot uses a simple decision-making algorithm based on IR sensor readings:

| Left Sensor | Right Sensor | Action |
|-------------|--------------|--------|
| OFF (LOW) | OFF (LOW) | Move Forward |
| OFF (LOW) | ON (HIGH) | Turn Right |
| ON (HIGH) | OFF (LOW) | Turn Left |
| ON (HIGH) | ON (HIGH) | Stop |

**IR Sensors:** Detect the black line by measuring reflected infrared light. Black surfaces absorb IR light (LOW signal), white surfaces reflect it (HIGH signal when no line detected).

**Motor Control:** The L298N driver receives PWM signals to control speed and digital signals for direction, allowing independent control of each motor for turning.

**PWM Optimization:** The code modifies Timer0 to increase PWM frequency to 7812.5 Hz, enabling smooth operation at lower speeds without motor stalling.

## 🚀 Usage

1. **Prepare the Track:**
   - Use black electrical tape on white surface
   - Create a path with gentle curves (avoid sharp angles)
   - Width: 2-3 cm recommended

2. **Position the Robot:**
   - Place robot on the line
   - Ensure IR sensors are positioned over/near the line
   - Sensors should be 1-2 cm above the surface

3. **Power On:**
   - Connect battery to L298N and Arduino
   - Robot should immediately start following the line

4. **Adjust if Needed:**
   - If too fast: Decrease `MOTOR_SPEED` value
   - If too slow: Increase `MOTOR_SPEED` value
   - Sensor height: Adjust for optimal detection

## 🎨 Customization

### Adjust Speed
```cpp
#define MOTOR_SPEED 180  // Change value (0-255)
```

### Change Pin Configuration
```cpp
#define IR_SENSOR_RIGHT 11  // Change to your pin
#define IR_SENSOR_LEFT 12   // Change to your pin
```

### Modify Behavior
Edit the `loop()` function to change robot logic:
```cpp
// Example: Continue forward when both sensors detect line
if (rightIRSensorValue == HIGH && leftIRSensorValue == HIGH)
{
    rotateMotor(MOTOR_SPEED, MOTOR_SPEED); // Instead of stop
}
```

## 🐛 Troubleshooting

**Robot doesn't move:**
- Check battery voltage (should be 7-12V)
- Verify all motor connections to L298N
- Ensure L298N jumpers are in place for ENA/ENB

**Robot moves but doesn't follow line:**
- Adjust IR sensor height (1-2 cm from surface)
- Check sensor sensitivity (use potentiometer on sensor)
- Verify black line has good contrast with background

**Robot is too fast/uncontrollable:**
- Reduce `MOTOR_SPEED` value (try 120-150)
- Check that PWM frequency modification is working

**One motor doesn't work:**
- Swap motor connections to test if motor or driver issue
- Check corresponding pins and connections

**Erratic behavior:**
- Ensure common ground between Arduino and L298N
- Check for loose connections
- Verify sensor readings using Serial monitor

## 📚 Learning Resources

This project teaches:
- Arduino programming basics
- Digital sensor reading
- PWM motor control
- H-bridge motor driver usage
- Autonomous robotics concepts
- Real-time decision making

## 🤝 Contributing

Contributions are welcome! Feel free to:
- Report bugs
- Suggest new features
- Submit pull requests
- Improve documentation

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 👨‍💻 Author

Created by Sarabjeet Singh

## 🙏 Acknowledgments

- Arduino community for excellent documentation
- Robotics enthusiasts for inspiration and support

---

**Happy Building! 🤖**

If you found this helpful, please ⭐ star this repository!
