# Gauntlet System Validation — Flex-Sensor Robotic Hand

A wearable-controlled robotic hand that translates live finger movements into servo-actuated articulation, built on Arduino Uno with a custom C++ control loop and PID feedback.

---

## Overview

The Gauntlet System uses flex sensors embedded in a glove to capture finger bend angles in real time. An Arduino Uno reads those analog signals, applies PID control, and drives five servo motors that pull fishing line tendons to articulate a 3D-printed hand. Elastic cord returns each finger to its neutral position when tension is released.

---

## Hardware

| Component | Spec / Role |
|---|---|
| Arduino Uno | Microcontroller — UART, I2C, SPI |
| Flex Sensors (×5) | 2.2 in — analog bend detection per finger |
| Servo Motors (×5) | Finger actuation via tendon pull |
| Resistors (×5) | 10 kΩ pull-down — stabilizes ADC readings |
| Fishing Line | Tendons — transmits servo torque to finger joints |
| Elastic Cord | Return springs — restores fingers to neutral |
| Glove | Wearable sensor mount |
| 3D-Printed Arm | Custom chassis housing servos and routing channels |

---

## How It Works

1. **Sense** — Flex sensors form a voltage divider with 10 kΩ resistors; bend angle maps to an analog voltage read by the Arduino ADC.
2. **Process** — A PID controller computes motor commands from the error between target and measured finger position.
3. **Actuate** — PWM signals drive servos; fishing-line tendons curl the fingers while elastic cord provides passive extension.

---

## Software

- **Language**: C++ (Arduino)
- **Control**: PID loop — tunable `Kp`, `Ki`, `Kd` constants per channel
- **Communication**: Serial monitor output for live sensor debugging

---

## Getting Started

### Requirements
- Arduino IDE ≥ 2.0 or PlatformIO
- Standard Arduino libraries (no external dependencies)

### Flash
```bash
# Clone the repo
git clone https://github.com/<your-username>/gauntlet-system-validation.git

# Open in Arduino IDE, select Board: Arduino Uno, then Upload
```

### Tuning PID

Each finger's PID constants are defined at the top of `main.cpp`:
```cpp
float Kp = 1.2, Ki = 0.01, Kd = 0.05;  // adjust per servo channel
```

Increase `Kp` for faster response; reduce if oscillation occurs.

---

## Contributing

Pull requests are welcome. For significant changes, open an issue first to discuss scope. Please keep commits focused and descriptive.

![Thanos](Thanos.jpg)
