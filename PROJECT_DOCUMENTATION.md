# SMART WATER TANK CONTROLLER
## Automated Water Level Monitoring and Pump Control System Using STM32F103C8T6

## 1. Abstract

The Smart Water Tank Controller is an embedded system developed to automate water-level monitoring and water pump operation. The system uses an STM32F103C8T6 microcontroller and an HC-SR04 ultrasonic sensor to measure the distance between the sensor and the water surface. Based on the measured distance, the controller calculates the water level percentage and automatically controls the pump through a relay.

The system also provides real-time information through a 16×2 LCD, LED indicators, a buzzer alert, and a servo motor for visual indication. The firmware is developed using Embedded C and the STM32 HAL library, with STM32CubeMX and STM32CubeIDE. The project is functionally tested using the Wokwi simulation environment.

## 2. Problem Statement

Conventional water tank management often depends on manual observation and pump operation. This can lead to water overflow, unnecessary pump operation, and inefficient water usage. The proposed system addresses these issues through automatic water-level monitoring and relay-based pump control.

## 3. Objectives

- Monitor water levels automatically.
- Measure the distance between the sensor and the water surface.
- Calculate the water level percentage.
- Automatically control pump operation.
- Display water-level information on an LCD.
- Provide LED status indications and low-water buzzer alerts.
- Prevent unnecessary pump switching using hysteresis.

## 4. Hardware Components

| Component | Function |
|---|---|
| STM32F103C8T6 | Main microcontroller |
| HC-SR04 | Ultrasonic distance measurement |
| Relay Module | Pump switching control |
| 16×2 LCD | Water-level display |
| Red LED | Low/empty indication |
| Yellow LED | Normal-level indication |
| Green LED | Full-level indication |
| Buzzer | Low-water alert |
| Servo Motor | Visual indication |

## 5. Software and Development Tools

- STM32CubeMX – Microcontroller configuration and code generation.
- STM32CubeIDE – Embedded C development and compilation.
- Embedded C – Main application programming.
- STM32 HAL Library – Peripheral interfacing.
- Wokwi – Circuit simulation and functional verification.

## 6. System Architecture

The HC-SR04 ultrasonic sensor is positioned above the water surface. It sends distance information to the STM32F103C8T6 microcontroller.

The microcontroller processes the sensor measurement, calculates the water level, and controls the output devices. The relay controls the pump, while the LCD, LEDs, buzzer, and servo provide status information.

### Block Diagram

```text
       WATER TANK
           |
           v
    HC-SR04 SENSOR
           |
           v
    STM32F103C8T6
           |
     +-----+------------------+
     |          |             |
     v          v             v
   RELAY       LCD       LED INDICATORS
     |                        |
     v                        v
 WATER PUMP                 BUZZER
                            SERVO
```

## 7. Working Principle

### 7.1 Distance Measurement

The HC-SR04 ultrasonic sensor sends an ultrasonic pulse towards the water surface. The reflected signal is received by the sensor, and the echo pulse duration is measured by the STM32 microcontroller.

The distance is calculated using:

Distance (cm) = Echo Duration (µs) / 58

### 7.2 Water-Level Calculation

The system uses a calibrated distance range of 10 cm to 90 cm.

- 10 cm or less represents 100% water level.
- 90 cm or more represents 0% water level.

The water-level percentage is calculated using:

Water Level (%) = ((90 - Distance) / 80) × 100

The calculated value is restricted to the range of 0% to 100%.

### 7.3 Automatic Pump Control

The STM32 microcontroller controls the relay according to predefined water-level thresholds.

- When the measured distance exceeds 70 cm, the pump is switched ON.
- When the measured distance reaches 10 cm or less, the pump is switched OFF.
- Between these thresholds, the previous pump state is maintained.

This method is called hysteresis-based control. It prevents frequent switching when the water level fluctuates near a threshold.

### 7.4 LCD Display

The 16×2 LCD displays the calculated water-level percentage and measured distance, allowing the user to monitor the tank condition.

### 7.5 LED Indicators

Three LEDs provide visual information about the water-level condition:

- Red LED – Empty or very low water level.
- Yellow LED – Normal water level.
- Green LED – Full water level.

### 7.6 Buzzer Alert

The buzzer provides an audible alert when the water level reaches the low-water condition.

### 7.7 Servo Motor

The servo motor acts as an additional visual indicator of the water-level condition.

## 8. Simulation and Testing

The project was developed and functionally verified using the Wokwi simulation environment.

### Test Case 1: Low Water Level

- Distance: 81 cm
- Water Level: 10%
- Pump Status: ON

### Test Case 2: Intermediate Water Level

- Distance: 33 cm
- Water Level: 70%
- Pump Status: ON

### Test Case 3: Full Water Level

- Distance: 10 cm
- Water Level: 100%
- Pump Status: OFF

## 9. Results and Discussion

The simulation demonstrated the intended operation of the water-level monitoring and automatic pump-control logic. The LCD displayed the calculated water level and distance, while the relay, LED indicators, buzzer, and servo provided the corresponding outputs.

The observed results matched the configured water-level thresholds and pump-control behaviour.

**Note:** The results represent simulation-based verification. Physical hardware implementation and testing are required for real-world validation.

## 10. Future Enhancements

- IoT-based remote water-level monitoring.
- Mobile application notifications.
- Dry-run protection for the pump.
- Water leakage detection.
- Wireless monitoring and control.
- Physical hardware implementation.

## 11. Conclusion

The Smart Water Tank Controller demonstrates an embedded-system approach to automated water-level monitoring and pump control. By combining an ultrasonic sensor, STM32 microcontroller, relay, and multiple output indicators, the system provides an automated method of monitoring tank conditions and controlling pump operation.

## 12. Project Repository

The complete source code, STM32 configuration files, and Wokwi simulation files are available in this GitHub repository.
