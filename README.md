# Astraeus-9-C-C

The ASTRAEUS-9 system functions as a fault-tolerant mission control system which oversees activities during orbital re-entry. The system uses three technologies to achieve real-time hardware degradation detection through embedded hardware sensing and physics-driven simulation and machine learning.

## Robotics & GNC
**Lead Engineer: Rhutvik Pachghare**

### 1. Embedded Kernel (`/Astraeus_Kernel.ino`)
- **Platform**: ESP32 Microcontroller
- **Logic**: The system operates **SpatialKalman filter** (`Kalman_Filter.h`) which processes raw sensor data to produce smoothed results and velocity estimations.
- **Comms**: Transmits telemetry data via MQTT protocol over WiFi.

### 2. Mission Simulation (`/mission_simulator.py`)
- **Scenario**: Models an orbital decay process from 550km (LEO) to impact.
- **Physics**: Uses atmospheric drag to simulate increasing "jitter" as altitude decreases.
- **Anomaly Injection**: Randomly introduces "Cosmic Ray Bit-Flips" and radiation damage based on exposure duration.

### 3. Physics & Thermal Engines
- **`physics_engine.py`**: Computes atmospheric density and orbital torque.
- **`thermodynamics.py`**: Models re-entry heat flux and skin temperature estimates.

---

## ML & Data Engineering
**Lead Engineer: Pooja Kiran**

### 1. Intelligence & Diagnostics
- **`anomaly_ml.py`**: MLP Regressor (Autoencoder) evaluates hardware faults through reconstruction error analysis.
- **`black_box.sql`**: Schema for persisting mission-critical telemetry and diagnostic logs.

### 2. Mission Control Dashboard (`/main.py`)
- **Interface**: Streamlit-based UI with a custom "dark mode" (`style.css`).
- **Telemetry**: Real-time kinetic vector visualization.
- **Diagnostics**: Neural spectral analysis for hardware condition assessment.

### 3. Infrastructure & Setup
The system uses **Docker** to containerize the MQTT broker (Mosquitto), Postgres database, and the Python dashboard.

#### Prerequisites
- **Docker & Docker Compose**
- **Python 3.9+** (for local simulation)

#### Quick Start
1. **Initialize Services**:
   ```bash
   bash setup.sh
   ```
   *Launches Mosquitto Broker, Postgres DB, and Streamlit Dashboard.*

2. **Launch Simulation**:
   ```bash
   python mission_simulator.py
   ```
   *Publishes telemetry to `astraeus/telemetry`.*

3. **Access Dashboard**: 
   Navigate to [http://localhost:8501](http://localhost:8501).

---

## Dependencies
- **Python**: `streamlit`, `numpy`, `scikit-learn`, `paho-mqtt`, `plotly`, `scipy`, `psycopg2-binary`.
- **Services**: `eclipse-mosquitto`, `postgres:latest`.

## Data Logs
Flight data is persisted to the `mission_logs` Postgres table, recording timestamp, altitude, heat flux, and anomaly scores.

![Dashboard](https://github.com/user-attachments/assets/31d4fced-840b-4a10-8817-b493f7fad03e)


