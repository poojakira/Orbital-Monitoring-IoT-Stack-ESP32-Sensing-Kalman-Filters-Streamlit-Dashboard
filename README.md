# Orbital-IoT-Monitor (Astraeus-9)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow)](LICENSE)
[![Platform: ESP32 + Python](https://img.shields.io/badge/Platform-ESP32%20%2B%20Python-blue)]()
[![Protocol: MQTT](https://img.shields.io/badge/Protocol-MQTT-green)]()

**Fault-tolerant orbital mission control system combining ESP32 embedded sensing, Kalman filtering, physics-based re-entry simulation, and neural anomaly detection.**

---

## Overview

Astraeus-9 integrates three core technologies into a cohesive orbital monitoring platform:

1. **ESP32 Embedded Sensing Kernel** — SpatialKalman filter for real-time hardware telemetry smoothing and velocity estimation
2. **Physics-Based Re-Entry Simulator** — Models orbital decay from 550 km LEO to impact with atmospheric drag, heat flux, and skin temperature modeling
3. **Neural Anomaly Detection** — MLP Regressor Autoencoder detecting hardware faults via reconstruction error analysis

It bridges embedded hardware constraints with ML-driven orbital monitoring workflows.

---

## System Architecture

| Module | Language | Role |
|---|---|---|
| `Astraeus_Kernel.ino` | C++ (Arduino) | ESP32 sensing kernel + SpatialKalman filter |
| `Kalman_Filter.h` | C++ | SpatialKalman filter header library |
| `mission_simulator.py` | Python | Orbital decay simulation from 550 km LEO to impact |
| `physics_engine.py` | Python | Atmospheric density + orbital torque computation |
| `thermodynamics.py` | Python | Re-entry heat flux + skin temperature modeling |
| `anomaly_ml.py` | Python | MLP Regressor Autoencoder for hardware fault detection |
| `main.py` | Python | Streamlit mission control dashboard |
| `black_box.sql` | SQL | PostgreSQL schema for mission-critical telemetry logs |

---

## Physics Simulation

| Parameter | Value |
|---|---|
| Starting Altitude (LEO) | 550 km |
| Decay Model | Atmospheric drag |
| Anomaly Injection | Cosmic Ray Bit-Flips + radiation damage |
| Thermal Model | Re-entry heat flux + skin temperature estimation |
| Orbital Torque | Computed by `physics_engine.py` |

---

## ML Anomaly Detection

| Parameter | Value |
|---|---|
| Model Type | MLP Regressor Autoencoder |
| Detection Method | Reconstruction error analysis |
| Fault Categories | Cosmic Ray Bit-Flips, radiation damage, sensor degradation |
| Analysis | Neural spectral analysis for hardware condition assessment |

---

## Quick Start

### Prerequisites
- Docker & Docker Compose
- Python 3.9+

### Initialization

```bash
# Step 1: Start services (Mosquitto Broker + PostgreSQL + Streamlit Dashboard)
bash setup.sh

# Step 2: Launch orbital decay simulation
python mission_simulator.py

# Step 3: Access Dashboard
# http://localhost:8501
```

---

## Infrastructure

- **Docker Compose**: Containerizes Mosquitto MQTT broker, PostgreSQL, and Streamlit dashboard
- **MQTT Protocol**: ESP32 transmits telemetry over WiFi to `astraeus/telemetry` topic
- **PostgreSQL**: Persists flight data (timestamp, altitude, heat flux, anomaly scores) in `mission_logs` table
- **Streamlit UI**: Custom dark mode (`style.css`) with real-time kinetic vector visualization

---

## Team Contributions

**Pooja Kiran** — Lead ML & Data Engineering
- Neural anomaly detection (`anomaly_ml.py`): MLP Regressor Autoencoder
- PostgreSQL telemetry schema (`black_box.sql`)
- Streamlit mission control dashboard (`main.py`) with custom dark mode CSS
- Docker Compose infrastructure (Mosquitto + PostgreSQL + Streamlit)

**Rhutvik Pachghare** — Lead Robotics, GNC & Embedded Systems
- ESP32 embedded sensing kernel (`Astraeus_Kernel.ino`) with SpatialKalman filter
- MQTT telemetry pipeline (ESP32 → WiFi → MQTT broker)
- Physics-based re-entry simulator (`mission_simulator.py`)
- Thermodynamic and physics engines (`physics_engine.py`, `thermodynamics.py`)

---

## License

MIT — see [LICENSE](LICENSE).

---

## Author

**Pooja Kiran** & **Rhutvik Pachghare**

- GitHub: [@poojakira](https://github.com/poojakira)
- Platform: ESP32 + Python 3.9+ | Protocol: MQTT over WiFi
