# TinyML Predictive Maintenance System using Edge Impulse and Blynk

An edge-AI predictive maintenance system that detects abnormal machine behavior
on a microcontroller using an Edge Impulse model, and sends instant
notifications to your phone through the Blynk IoT app.

## Overview
An accelerometer mounted on a machine (motor, fan, pump) captures vibration data.
A model trained in Edge Impulse Studio runs directly on the ESP32 to classify
machine health in real time. When a fault or anomaly is detected, the device
pushes the status to the Blynk app and triggers a notification, so maintenance
can happen before a breakdown.

## System Architecture
Accelerometer -> ESP32 (Edge Impulse inference) -> Wi-Fi -> Blynk Cloud -> Blynk Mobile App

## Features
- On-device inference with no cloud needed for the ML itself
- Fault classification (normal, imbalance, bearing fault, loose mount) plus anomaly detection
- Spectral feature extraction (FFT) for vibration signals
- Quantized int8 model optimized with the EON Compiler
- Real-time machine status dashboard in Blynk
- Push/email notifications through Blynk events when a fault is detected
- Local alerts via LED/buzzer

## Workflow
1. **Data acquisition:** collect accelerometer data for healthy and faulty states
2. **Impulse design:** spectral analysis + neural network classifier + anomaly detection
3. **Training and testing:** check accuracy and confusion matrix in Edge Impulse Studio
4. **Deployment:** export as an Arduino library and flash to the ESP32
5. **Blynk setup:** create a template, add datastreams and an event, and add the credentials to the firmware
6. **Monitoring:** view live status and receive alerts on your phone

## Blynk Configuration
| Datastream    | Pin | Type    | Purpose                          |
|---------------|-----|---------|----------------------------------|
| Machine State | V0  | String  | Normal / Fault label             |
| Confidence    | V1  | Double  | Prediction confidence (%)        |
| Anomaly Score | V2  | Double  | Anomaly detection score          |

- Event: `fault_detected` (triggers push/email notification)
- Add your credentials in the firmware:
  `BLYNK_TEMPLATE_ID`, `BLYNK_TEMPLATE_NAME`, `BLYNK_AUTH_TOKEN`

## Hardware
- ESP32 development board
- MPU6050 / ADXL345 accelerometer
- Optional: buzzer, LED

## Software
- Edge Impulse Studio
- Arduino IDE / PlatformIO
- Blynk IoT app and Blynk library

## Project Structure
├── data/            # Sample datasets (normal / faulty)
├── firmware/        # ESP32 code: sensor reading, inference, Blynk
├── edge-impulse/    # Exported model library and project settings
├── docs/            # Wiring diagram, Blynk screenshots, results
└── README.md

## Results
| Metric           | Value |
|------------------|-------|
| Accuracy         | XX%   |
| Inference time   | XX ms |
| RAM usage        | XX KB |
| Flash usage      | XX KB |

## Edge Impulse Project
Public project link: <add your link here>

## Future Improvements
- Add temperature and current sensing
- Log data to a time-series database
- Predict remaining useful life (RUL)

## License
MIT