<div align="center">

# 🔊 Sound Level Monitoring & Alert System

### Real-Time Noise Detection using NodeMCU (ESP8266)

![Platform](https://img.shields.io/badge/Platform-NodeMCU%20ESP8266-blue?style=for-the-badge&logo=espressif&logoColor=white)
![IDE](https://img.shields.io/badge/IDE-Arduino%20IDE-00979D?style=for-the-badge&logo=arduino&logoColor=white)
![Sensor](https://img.shields.io/badge/Sensor-Analog%20Sound%20Module-purple?style=for-the-badge)
![Threshold](https://img.shields.io/badge/Alert%20Threshold-60%20dB-red?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Tested%20%26%20Working-success?style=for-the-badge)

*Too loud? The LED lights up instantly.* 🎤💡

![Hardware Setup](images/hardware-setup.jpg)

</div>

---

## 📖 Overview

Noise pollution affects concentration, sleep and long-term health, yet most spaces have no simple way to flag when it gets too loud. This project is a low-cost, standalone **sound level monitor** that measures ambient sound in real time, converts it into an approximate **decibel (dB)** value, and switches on an **alert LED** when the level crosses a configurable threshold (**60 dB**).

Every reading is also streamed to the Arduino IDE Serial Monitor for live logging. Because the ESP8266 has built-in Wi-Fi, the same hardware can later be extended into a cloud-connected IoT noise-monitoring node.

## ✨ Features

- 🎤 **Real-time sound sensing** via an electret microphone module on A0
- 📈 **Peak-to-peak sampling** over a 50 ms window for meaningful amplitude readings
- 🧮 **Approximate dB calculation** using a logarithmic conversion
- 🚨 **Instant LED alert** when the level exceeds the threshold
- 🖥️ **Live serial log** with readings and alert messages
- 🔌 **Simple, cheap build**: 5 core components, USB powered
- 📡 **Wi-Fi ready** for future IoT expansion

## 🧰 Components Required

| Component | Role |
|---|---|
| NodeMCU ESP8266 | Sampling, dB calculation, threshold logic, serial output |
| Analog Sound Sensor Module | Electret mic + amplifier; outputs a voltage proportional to sound intensity |
| LED (5 mm, any colour) | Visual alert on pin D1 |
| Jumper Wires | Connections |
| Micro-USB Cable | Power and serial link |
| Laptop / PC with Arduino IDE | Upload firmware, view Serial Monitor |

## 🔌 Pin Connections

| NodeMCU Pin | Connected To |
|---|---|
| `A0` (Analog In) | Analog output (AO) of the sound sensor |
| `D1` (Digital Out) | Anode (+) of the alert LED, through a current-limiting arrangement |
| `3V3` / `VU` | VCC of the sound sensor |
| `GND` | GND of the sensor and LED cathode |

## ⚙️ How It Works

```
 Microphone ──► Amplifier ──► A0 (ADC) ──► Peak-to-Peak ──► dB Calc ──► > 60 dB? ──► LED + Serial
```

1. 🎙️ **Sense**: the mic picks up sound and the onboard amplifier boosts it into A0's range.
2. 📊 **Sample**: sound is a fast-varying waveform, so a single reading is meaningless. The firmware reads A0 repeatedly over a **50 ms window**, tracking the max and min.
3. 📐 **Process**: peak-to-peak amplitude is converted to a voltage, then through a logarithmic relationship to an approximate **dB** value.
4. 🚦 **Decide**: compare with the 60 dB threshold.
5. 💡 **Act**: LED ON plus an alert message if exceeded, otherwise LED OFF. The value is printed to serial every cycle.

> ⚠️ **Note on accuracy:** The dB value is a *relative, empirically-scaled* measure suited to threshold comparison, not a laboratory-calibrated dB(SPL) reading.

### 🔁 Firmware Flow

**Initialisation**
- Start serial communication
- Set the LED pin as output and keep it OFF

**Main loop**
1. Open a 50 ms sampling window
2. Track max and min analog values
3. Compute peak-to-peak amplitude
4. Convert to voltage, then to approximate dB
5. Print the dB value
6. Compare with the 60 dB threshold
7. Exceeded → LED ON + alert message; otherwise LED OFF
8. Short pause, then repeat

## 🚀 Getting Started

1. Clone the repo
   ```bash
   git clone https://github.com/shoaib725/<your-repo-name>.git
   ```
2. Install the **ESP8266 board package** in Arduino IDE (Boards Manager).
3. Wire the circuit as per the pin table.
4. Open the sketch, select **NodeMCU 1.0 (ESP-12E Module)** and the correct COM port.
5. Upload, then open the Serial Monitor (set it to the baud rate used in the sketch).
6. Clap or speak near the mic and watch the readings and LED.

## 🧪 Test Results

| Test Condition | Approx. Level | LED / Output |
|---|---|---|
| 🤫 Silent room | ~25 dB | LED OFF |
| 🗣️ Normal speech near mic | ~40–50 dB | LED OFF |
| 👏 Hand clap close to sensor | 63–68 dB | LED ON, alert printed |
| 📢 Loud shout / sharp sound | 70+ dB | LED ON, alert printed |

**Observations**
- ✅ Responds within a single 50 ms sampling window, so the alert is near-instant
- ✅ Quiet-room readings stay low and steady
- ✅ LED turns on only when the threshold is genuinely exceeded and turns off when sound drops
- ✅ Serial log is useful for baseline checks and tuning the threshold

## 🌍 Applications

- 📚 Library, classroom and office quiet/loud indicator
- 👶 Baby-room or hospital ward sudden-noise alerts
- 🏭 Industrial workspace noise and hearing-protection monitoring
- 🏠 Smart-home sensing node
- 📡 Wi-Fi IoT noise-logging dashboard

## 🔮 Future Scope

- [ ] 📡 **Wi-Fi** push of readings to a cloud or web dashboard
- [ ] 🗄️ **Data logging** for noise trend analysis
- [ ] 📱 **Mobile/app alerts** when the threshold is crossed
- [ ] 🎚️ **Calibration** against a reference sound level meter
- [ ] 🚥 **Multi-level alerts** (moderate / severe) with different LED colours or a buzzer
- [ ] 🏠 **Smart-home integration** for context-aware actions

## 🧠 Skills Demonstrated

`Analog Signal Acquisition` · `Peak-to-Peak Signal Processing` · `Logarithmic dB Conversion` · `Threshold-Based Control` · `GPIO Output Control` · `Serial Debugging` · `ESP8266 / NodeMCU`

## 👨‍💻 Author

**Pathan Mohammad Shoaib Khan**
B.Tech, Electronics & Communication Engineering
Seshadri Rao Gudlavalleru Engineering College

[![GitHub](https://img.shields.io/badge/GitHub-shoaib725-181717?style=for-the-badge&logo=github)](https://github.com/shoaib725)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-shoaibkhan725-0A66C2?style=for-the-badge&logo=linkedin)](https://linkedin.com/in/shoaibkhan725)

---

<div align="center">

⭐ If you found this project useful, consider giving it a star! ⭐

</div>
