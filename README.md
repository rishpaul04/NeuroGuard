
# NeuroGuard: IoT & AI-Powered Alzheimer's Detection 🧠
NeuroGuard is a real-time, IoT-based health monitoring system engineered for the early detection of Alzheimer's disease markers. By leveraging edge computing on a Raspberry Pi, the system continuously acquires and processes multi-modal physiological data.
The application integrates advanced hardware sensors with a robust Python data pipeline to monitor brainwave activity (EEG), cardiovascular metrics, and skin conductance. This data is synthesized in real-time to identify patterns associated with cognitive decline, serving as an advanced, non-invasive early warning system.

> **Disclaimer:** NeuroGuard is a research and development prototype. It is not intended to replace professional medical diagnosis, advice, or treatment.

## ✨ Core Capabilities

* **Real-Time Data Acquisition:** Engineered continuous data pipelines that ingest high-frequency signals with minimal latency.
* **Neurological Monitoring:** Captures and filters raw EEG (Electroencephalogram) signals for brainwave analysis.
* **Physiological Tracking:** Monitors blood oxygenation, heart rate, and emotional/stress arousal via Galvanic Skin Response.
* **Edge Computing Optimization:** All sensor interfacing, signal processing, and initial data filtering are executed locally on the Raspberry Pi.

## 🏗️ Technical & Hardware Architecture

NeuroGuard requires a synthesis of embedded hardware components and a Python-based software stack.

### Hardware Stack

* **Compute Node:** Raspberry Pi (3B+/4 recommended)
* **Analog-to-Digital Converter:** ADS1115 (16-bit ADC) — *Crucial for digitizing analog sensor signals for the Raspberry Pi.*
* **Sensors:**
* **BioAmp EXG Pill:** For capturing EEG biopotential signals.
* **MAX30102:** Pulse Oximetry and Heart Rate sensor (I2C interface).
* **Grove GSR:** Galvanic Skin Response sensor to measure electrodermal activity.

### Software Stack

* **Language:** Python 3.x
* **Libraries:** `smbus` (I2C communication), `adafruit-circuitpython-ads1x15`, `numpy`, `pandas`, `scipy` (for signal filtering/processing).
* **Model Training:** LightGBM

---

## ⚙️ Hardware Setup & Wiring Guide

Before initializing the software, ensure the hardware is wired correctly. The Raspberry Pi relies on the I2C protocol to communicate with the digital sensors and the ADC.

**1. I2C Configuration**
Ensure I2C is enabled on your Raspberry Pi:

```bash
sudo raspi-config
# Navigate to Interfacing Options > I2C > Enable

```

**2. Sensor Connections**

* **MAX30102:** Connects directly to the Raspberry Pi's I2C pins (SDA to Pin 3, SCL to Pin 5) and 3.3V power.
* **ADS1115 ADC:** Connects to the Raspberry Pi's I2C pins.
* **BioAmp EXG Pill:** Connect the analog output of the BioAmp to `A0` on the ADS1115.
* **Grove GSR:** Connect the analog output of the GSR sensor to `A1` on the ADS1115.

---

## 💻 Local Software Setup

### Prerequisites

* Raspberry Pi running Raspberry Pi OS (Bullseye or later recommended).
* Python 3.x and `pip` installed.

### Installation

**1. Clone the repository onto your Raspberry Pi**

```bash
git clone https://github.com/yourusername/NeuroGuard.git
cd NeuroGuard

```

**2. Create a virtual environment (Recommended)**

```bash
python3 -m venv venv
source venv/bin/activate

```

**3. Install Python dependencies**

```bash
pip install -r requirements.txt

```

**4. Execute the System**
Run the main data pipeline script to begin initializing sensors and reading data:

```bash
python3 src/main.py

```

*The console will display initialization statuses for the ADS1115, MAX30102, and BioAmp systems, followed by the real-time data stream.*

---
## 🔬 Data Pipeline Engineering Details

The core of the software relies on efficient data handling. The Python backend performs the following sequence:

1. **Ingestion:** Reads digital signals directly via I2C and reads analog signals asynchronously via the ADS1115.
2. **Filtering:** Applies digital bandpass and notch filters (via SciPy) to the raw EEG data to remove 50Hz/60Hz power line noise and baseline wander.
3. **Aggregation:** Synchronizes the timestamps across the MAX30102, GSR, and EEG sensors into a unified DataFrame for AI model processing.

## 🤝 Contribution Guidelines

We welcome contributions to improve sensor accuracy, optimize the data pipeline, or enhance the predictive modeling. Please fork the repository and submit a pull request with detailed notes on your changes.

## 📬 Contact & Maintainer

**Rishita Paul**
**Email:** rishitapaul2812@gmail.com
