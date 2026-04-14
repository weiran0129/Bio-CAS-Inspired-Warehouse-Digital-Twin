# A Biologically-Inspired Digital Twin Architecture for Resilient Warehouse Operations

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![ROS 2](https://img.shields.io/badge/ROS%202-Humble-blue.svg)](https://docs.ros.org/en/humble/index.html)
[![NVIDIA Omniverse](https://img.shields.io/badge/NVIDIA-Omniverse-76B900.svg)](https://developer.nvidia.com/nvidia-omniverse-platform)

**Official Code Repository for the IEEE Conference Paper:** *A Biologically-Inspired Digital Twin Architecture for Resilient Warehouse Operations*

This repository contains the architecture, simulation environments, and edge-cloud deployment scripts for a dual-stream Digital Twin (DT) designed to prevent the "Global E-Stop" problem in high-speed automated warehouses.

---

## 📖 Overview

Modern automated warehouses operate at high speeds where the margin for physical error is near zero. Traditional Warehouse Management Systems (WMS) rely on global hardware stops during hazard events, resulting in massive facility-wide throughput collapse. 

To address this, we propose a biologically-inspired, closed-loop Digital Twin architecture leveraging the NVIDIA ecosystem. By decoupling the **Operational Edge** (NVIDIA Jetson, IGX) acting as rapid "reflexes" from the **Cognitive Cloud** (DGX, Omniverse, cuOpt) acting as the "brain," we achieve a highly resilient dual-stream system. 

### Key Innovations
* **Dual-Stream Decoupling:** Separates physical execution from cognitive simulation to guarantee sub-100ms Mean Time To Detection (MTTD).
* **Entropy Comparator:** Utilizes Kullback-Leibler (KL) Divergence to dynamically toggle between economical *Live-Mirroring* and GPU-intensive *Look-ahead Simulation*.
* **Edge Survival Hierarchy:** Integrates NavStack, Artificial Potential Fields (APF), and Control Barrier Functions (CBFs) to ensure absolute local safety.
* **Autonomous Self-Healing:** Uses NVIDIA cuOpt and Sensor RTX to validate synthetic recovery paths before physical execution, retaining ~85% organic throughput during catastrophic hazards.

---

## 🛠️ System Architecture

1. **The Operational Edge (Physical Reality):** Data distillation and reflexive control via NVIDIA Jetson and IGX nodes.
2. **The Cognitive Cloud (Virtual Expectation):** Global VRP routing via NVIDIA cuOpt and physically accurate simulation via Omniverse PhysX 5.
3. **The Convergence Point:** The Entropy Comparator triggers adaptive resolution workflows based on state divergence.

---

## 📂 Repository Structure

```text
├── 📁 edge_workspace/          # ROS 2 packages for AMR edge devices (Jetson)
│   ├── src/cbf_safety_filter/  # Control Barrier Function QP solver
│   └── src/apf_navigation/     # Artificial Potential Field reflexes
├── 📁 cloud_workspace/         # Cloud-level logic and routing
│   ├── src/entropy_comparator/ # KL Divergence state comparison module
│   └── src/cuopt_dispatcher/   # NVIDIA cuOpt global rerouting scripts
├── 📁 simulation/              # NVIDIA Omniverse & Isaac Sim assets
│   ├── warehouse_env.usd       # Main Universal Scene Description file
│   └── sensor_rtx_configs/     # Synthetic data generation configs
├── 📁 docs/                    # Extended documentation and architecture diagrams
├── 📄 requirements.txt         # Python dependencies
└── 📄 README.md
