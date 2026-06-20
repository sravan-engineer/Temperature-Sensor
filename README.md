# Temperature Sensor Arduino Project 🌡️

An Arduino UNO-based temperature monitoring system using an analog temperature sensor (LM35/TMP36-type). The system reads ambient temperature, displays it on the Serial Monitor, and triggers LEDs based on temperature thresholds.

## 📽️ Demo

> Add your video link here after uploading (see "Adding the Demo Video" section below).

```
[Demo Video](PASTE_VIDEO_LINK_HERE)
```

## 📌 Overview

A temperature sensor is an electronic component that measures temperature and sends the value to a controller like an Arduino. In this project, the sensor is connected to analog pin A0 of the Arduino UNO, and the code converts the raw sensor voltage into a temperature reading in Celsius.

**Common sensors used:**
- **LM35** → Gives output directly in °C
- **TMP36**
- **DHT11 / DHT22** (digital sensors)

This project uses an LM35/TMP36-type analog temperature sensor.

## ⚙️ Working Principle

1. The temperature sensor senses heat and outputs a corresponding analog voltage.
2. The Arduino reads this analog voltage via `analogRead(A0)` (ADC range: 0V → 0, 5V → 1023).
3. The code applies an offset and scaling factor, then uses `map()` to convert the raw value into a temperature range of **-20°C to 120°C**.
4. The temperature is printed to the Serial Monitor.
5. LEDs turn ON/OFF based on the current temperature level.

## 🧩 Components Used

| Component | Purpose |
|---|---|
| Arduino UNO | Controls the entire system |
| Temperature Sensor (TMP36/LM35) | Senses temperature, connected to A0 |
| Green LED (Pin 12) | ON when temperature < 30°C |
| Yellow LED (Pin 11) | ON when temperature < 60°C |
| Red LED (Pin 10) | ON when temperature < 90°C |
| Breadboard & Wires | Circuit connections |

## 💡 LED Control Logic

| Temperature Range | LED Behavior |
|---|---|
| < 30°C | Green LED ON |
| < 60°C | Yellow LED ON |
| < 90°C | Red LED ON |

## 🔧 Circuit Simulation

The circuit was designed and simulated in **Tinkercad**, with the temperature sensor connected to analog pin A0, and three LEDs connected to digital pins 12, 11, and 10 via a breadboard.

## 💻 Source Code

The Arduino sketch is available in [`temperature_sensor.ino`](./temperature_sensor.ino):

```cpp
int temp = 0;

void setup() {
  pinMode(A0, INPUT);
  Serial.begin(9600);
  pinMode(12, OUTPUT);
  pinMode(11, OUTPUT);
  pinMode(10, OUTPUT);
}

void loop() {
  temp = map(((analogRead(A0) - 20) * 3.043), 0, 1023, -20, 120);
  Serial.println(temp);

  if (temp < 30) { digitalWrite(12, HIGH); } else { digitalWrite(12, LOW); }
  if (temp < 60) { digitalWrite(11, HIGH); } else { digitalWrite(11, LOW); }
  if (temp < 90) { digitalWrite(10, HIGH); } else { digitalWrite(10, LOW); }

  delay(10);
}
```

## 📁 Repository Structure

```
temperature-sensor-arduino/
├── README.md
├── temperature_sensor.ino
├── temperature_sensor_project_combined.pdf
└── demo/
    └── screen_recording_demo.mp4   (or a link to hosted video, see below)
```

## 🚀 Applications

- Room/environment temperature monitoring
- Overheating alerts in electronics enclosures
- Smart home climate indicators
- Industrial temperature warning systems

## 📄 Full Report

See [`temperature_sensor_project_combined.pdf`](./temperature_sensor_project_combined.pdf) for the complete project report, including a line-by-line code explanation and circuit diagrams.

## 👤 Author

Add your name, college/institution, and contact/social links here.

## 📜 License

Add a license of your choice (e.g., MIT) — see [choosealicense.com](https://choosealicense.com/) if unsure.

