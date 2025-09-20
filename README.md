# Smart City IoT Simulation System — Cisco Packet Tracer

This project presents an engineering simulation of an integrated smart city infrastructure, built and tested in **Cisco Packet Tracer**.

The project uses a hierarchical network design mapped onto a geographic city layout. It connects several essential sectors—a smart hospital, smart university, smart home, and smart parking facility—to processing and control centers. The simulation incorporates machine-to-machine (M2M) communication, IoT controller automation, and fog-computing servers.

## Network Architecture

The city is divided into interconnected geographic zones. Its network backbone includes:

- **Distributed server farms:** Dedicated rack servers for sector-level control, database storage, and automation scenarios.
- **Cloud and ISP router:** Connects the city to the external internet and supports long-term storage for big data.
- **Wireless aggregation:** Cellular towers collect data from edge sensors.
- **Fog computing server:** Provides edge-processing capabilities.

## Smart City Subsystems

### 1. Smart Hospital

**Components:** Six main areas—emergency, reception, laboratory, patient rooms, storage, and doctors' room—connected to a central rack.

**Systems:**

- **Fire safety:** Smoke detectors, a fire monitor, smart fire sprinklers, and an alarm siren.
- **Security and access:** Smart doors, motion detectors, and IP webcams.
- **Environmental control (HVAC):** Smart fans, blowers, smart lamps, and central heating elements.

### 2. Smart University

**Components:** Lecture hall, central library, main entrance, and administration office.

**Systems:**

- **Access control and registration:** RFID reader and cards.
- **Fire response and evacuation:** Smoke detectors are linked to sprinklers; windows and doors open automatically during an emergency.
- **Energy management:** An IoT dashboard on the administration computer helps conserve energy based on occupancy.

### 3. Smart Home

**Components:** Bedroom, living room, kitchen, bathroom, garage, and garden.

**Systems:**

- **Network and control:** Home gateway (`R-HOME`) and a `2960` switch.
- **Home safety:** Carbon monoxide sensor in the garage, plus a kitchen smoke detector and exhaust fan.
- **Automation and convenience:** Motion-activated lights and fans, and an RFID lock at the main entrance.

### 4. Smart Parking System

**Components:** Single-board computers (SBCs), microcontrollers (MCUs), magnetic induction metal sensors, smart garage doors, and license-plate monitoring cameras.

**Displays:**

- **Individual parking-space LCDs:** Show the status of spaces `SLOT-16` through `SLOT-20` as `OCCUPIED` or `EMPTY`.
- **Main smart LED display:** Updates the number of available spaces in real time (`Available Slots: X/20`).

## IP Addressing and Routing

The network uses a combination of **OSPF Area 0** and static routing.

| Device / Router | Local LAN | WAN / Link Interfaces | Routing / Configuration |
|---|---|---|---|
| `R-UNI` (University) | `10.2.0.1/16` | `172.16.2.2/30` | OSPF Area 0 + default route |
| `R-HOSP` (Hospital) | `10.3.0.1/16` | `172.16.3.2/30` | OSPF Area 0 + default route |
| `R-HOUSE` (Home) | `10.1.0.1/16` | `172.16.1.2/30` | OSPF Area 0 + default route |
| `R-MAIN` (Central) | `10.0.0.1/24` | `172.16.5.1/30` | OSPF Area 0 + static routing |
| `R1` (Edge Router) | — | `172.16.1.1`, `172.16.4.1`, `172.16.5.2` | OSPF Area 0 + static routes |
| `R2` (Edge Router) | — | `172.16.2.1`, `172.16.3.1`, `172.16.4.2` | OSPF Area 0 + static routes |
| `Router-ISP` | `10.0.0.1/24` | `172.16.10.1/30` | Static routing |
| Central Server | LAN 1: `10.0.0.100/24` | LAN 2 (Cell Tower): `192.168.50.1/24` | Dual-NIC configuration |

## Scripts and Automation

The project uses Python and JavaScript scripts in the Packet Tracer environment.

### Python (SBC and Logic Control)

- `Parking_Slots_Logic.py`: Reads analog inputs (`analogRead`) from the five magnetic parking sensors and updates the individual displays programmatically using `customWrite`.
- `Timer_State_Control.py`: Manages the automation timer (`DEACTIVATE_TIMER`) to control how long doors remain open or lights stay on before turning off automatically.

### JavaScript (MCU Controllers)

- `MCU_Motion_Reporter.js`: Configures the microcontroller interface, reads digital sensors, and sends real-time state reports to the IoT server using `IoEClient.reportStates`.

## How to Run

1. Install **Cisco Packet Tracer** (version 8.0 or later is recommended).
2. Open the project file with the `.pkt` extension.
3. Wait a few seconds for OSPF convergence; connected interfaces should turn green.
4. To view the IoT device dashboard, open a computer such as `Container-PC` or `Laptop-PT`, launch its web browser, and navigate to the server's IP address.

---

**Engineered & Simulated by Eng. RASHEED AL-RAJEHI | SHADOW WOLF SECURITY**

---