# Week 2 — BabySoC Fundamentals & Functional Modelling

**Course:** VSD – RISC-V SoC Tapeout Program  
**Objective:** To build a solid understanding of System-on-Chip (SoC) fundamentals and practice functional modelling of the BabySoC using simulation tools (**Icarus Verilog** & **GTKWave**).

---

## 1. What is a System-on-Chip (SoC)?
A **System-on-Chip (SoC)** is an integrated circuit that combines most or all components of a computing system onto a single silicon die.  
Instead of using separate chips for CPU, memory, and peripherals, an SoC integrates these components together — reducing power consumption, cost, and size while improving performance.

---

## 2. Components of a Typical SoC
- **CPU / Processor Core:** Executes instructions and performs computations.  
- **On-chip Memory:** Stores program code and data (e.g., SRAM, ROM, Flash).  
- **Peripherals:** Interfaces for input/output such as UART, GPIO, SPI, timers, etc.  
- **Interconnect / Bus Fabric:** Provides communication between the CPU, memory, and peripherals (e.g., AMBA, AXI, AHB).

---

## 3. Why BabySoC is a Simplified Learning Model
**BabySoC** is a minimal SoC model designed for educational and conceptual understanding.  
It contains:
- A simple CPU core  
- Basic on-chip memory  
- A few peripherals for interaction  

This simplified structure allows learners to focus on understanding SoC fundamentals, communication mechanisms, and functional simulation without complex industrial design details.

---

## 4. Role of Functional Modelling
**Functional modelling** defines how each component of the SoC behaves before RTL or physical design.  
It helps:
- **Validate architecture:** Ensure correct instruction flow and memory access.  
- **Debug early:** Detect issues before expensive synthesis or layout.  
- **Simulate quickly:** Test the design efficiently using Icarus Verilog and GTKWave.

---

## 5. Deliverables
- `README.md` – Summary of SoC fundamentals and BabySoC concept.  
- `lab/` – Verilog model, testbench, and simulation script.  
- `report/` – Lab report summarizing simulation results.  
- `waveforms/` – GTKWave output files generated from simulation.

---



