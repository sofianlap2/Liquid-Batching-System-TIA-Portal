# Liquid Batching System - Industrial Automation Project

**Technologies:** Siemens TIA Portal V17 | S7-1200 PLC | KTP700 HMI | PROFINET

📺 **Watch Demo Video:** https://youtu.be/bf9yCLkUwGU

## 🎯 Project Overview
Automated liquid batching system that fills a tank with two liquids in sequence, heats to a setpoint temperature, mixes for a specified time, and drains. Includes comprehensive safety interlocks, alarm management, and HMI visualization.

## 🏭 Key Features
- **Sequential Control:** State machine architecture using CASE statements in SCL
- **Safety Systems:** Emergency stop, pump overload protection, high-temperature alarms
- **Analog Processing:** Temperature scaling (NORM_X/SCALE_X) from 4-20mA sensor
- **HMI Design:** Intuitive operator interface with color animations, setpoint controls, and alarm codes
- **Fault Handling:** Multi-alarm code system for quick troubleshooting

## 📋 System Specifications
- **PLC:** Siemens S7-1214C DC/DC/DC
- **HMI:** KTP700 Basic PN
- **Programming Languages:** SCL (Structured Control Language), Ladder Logic
- **Communication:** PROFINET industrial Ethernet

## 🏗️ Architecture
### Sequence of Operations:
1. Fill Liquid A (Pump + Valve A) → Level Sensor 1
2. Fill Liquid B (Valve B) → Level Sensor 2
3. Heating → Temperature Setpoint
4. Mixing → Timer-based control
5. Draining → Level Low Sensor

### Safety Features:
- E-Stop immediately halts all outputs (Step 99)
- Pump overload protection
- High-temperature alarm (>90°C)
- Interlock checking before each step

## 📂 Project Structure
PLC_Code/
├── OB1_Main.scl (Main program cycle)
├── FB_Sequence_Control.scl (State machine logic)
├── DB_HMI_Commands.db (HMI interface tags)
└── DB_Process_Data.db (Process variables)


##  Demo Video
https://youtu.be/bf9yCLkUwGU

## 🛠️ Skills Demonstrated
- PLC Programming (SCL, Ladder)
- HMI/SCADA Design
- Analog Signal Processing
- Safety System Design
- Industrial Communication (PROFINET)
- State Machine Architecture
- Alarm Management
- Factory Acceptance Testing (FAT)

## 💼 This project demonstrates my ability to:
✅ Design complete automation systems from concept to HMI  
✅ Implement industrial safety standards and fault handling  
✅ Write clean, structured, maintainable PLC code  
✅ Create intuitive operator interfaces  

---
**Author:** sofienne nabli 
**Contact:** sofianesprit@gmail.com | https://www.linkedin.com/in/sofienne-nabli-b260b0191/
