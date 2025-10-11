# 🧠 Week 3 – Post-Synthesis GLS & STA Fundamentals  

---

## 🎯 Objective  
Understand and perform **Gate-Level Simulation (GLS)** after synthesis, validate functionality, and gain hands-on exposure to **Static Timing Analysis (STA)** using **OpenSTA**.  
You’ll compare post-synthesis results with functional simulation and explore timing analysis of the BabySoC.

---

## ⚙️ Part 1 – Post-Synthesis Gate-Level Simulation (GLS)

### 🔍 Purpose  
Validate that the synthesized BabySoC behaves identically to its pre-synthesis RTL model.

### 🔗 Reference  
[GLS Flow – VSD_HDP (Day 6)](https://github.com/Ananya-KM/VSD_HDP/blob/main/Day%206.md)

### 🧩 Steps  
1. **Synthesize** the BabySoC design using Yosys or OpenLANE.  
2. Generate the **synthesized netlist** (`baby_soc_synth.v`).  
3. **Simulate** the gate-level design with Icarus Verilog:  
   ```bash
   iverilog -o gls_sim baby_soc_synth.v testbench.v
   vvp gls_sim
   ```
4. Generate waveform:  
   ```bash
   gtkwave dump.vcd
   ```
5. Compare **functional vs gate-level** waveforms → logic must match (delays may differ).

### ✅ Deliverables  
- Synthesis & GLS logs  
- `.vcd` waveform screenshots  
- Note confirming **GLS = Functional Output**

---

## ⏱️ Part 2 – Fundamentals of Static Timing Analysis (STA)

### 🎓 Learning Resource  
[STA Fundamentals – Udemy Course (Free for Limited Time)](https://www.udemy.com/course/vlsi-academy-stachecks/?couponCode=F960AEDD365E0CD12546)

### 🧠 Key Concepts  

| Concept | Description |
|----------|--------------|
| **Setup Time** | Minimum time before clock edge when data must be stable |
| **Hold Time** | Minimum time after clock edge when data must remain stable |
| **Slack** | Margin = Required Time − Arrival Time |
| **Clock Definition** | Defines period and skew for STA analysis |
| **Path Analysis** | Timing from launch flop → capture flop |

### 📝 Task  
Write concise notes on each concept and explain why STA is vital post-synthesis.

### 📄 Deliverable  
A 1-page summary covering:  
- Setup & Hold checks  
- Slack and violation interpretation  
- Clocking constraints  
- STA’s role in chip sign-off  

---

## 📊 Part 3 – Generate Timing Graphs with OpenSTA

### 🔗 References  
- [OpenSTA GitHub](https://github.com/The-OpenROAD-Project/OpenSTA)  
- [Example Script – VSD HDP Day 19](https://github.com/arunkpv/vsd-hdp/blob/main/docs/Day_19.md)  
- [OpenSTA Documentation (PDF)](https://github.com/The-OpenROAD-Project/OpenSTA/blob/master/doc/OpenSTA.pdf)

### 🧠 Goal  
Use **OpenSTA** to analyze the synthesized BabySoC’s timing, identify critical paths, setup/hold violations, and slack.

### ⚙️ Steps  
```tcl
# Load design and libraries
read_verilog baby_soc_synth.v
read_liberty slow.lib
read_sdc constraints.sdc
link_design baby_soc

# Define clocks and I/O constraints
create_clock -name clk -period 10 [get_ports clk]
set_input_delay 2 -clock clk [all_inputs]
set_output_delay 2 -clock clk [all_outputs]

# Generate timing reports
report_timing
report_checks
report_slack
```

### 📈 Observations  
- Identify the **critical path** (max delay path).  
- Check for **setup/hold violations**.  
- Note positive/negative **slack** values.  
- Relate timing results to overall chip performance.

### ✅ Deliverables  
- OpenSTA input scripts (`.tcl`)  
- Timing reports & graphs (screenshots with timestamp + userid)  
- Short observation summary: critical path, slack meaning, violations  

---

## 🧩 Learning Outcomes  
By the end of Week 3, you will be able to:  
1. Perform GLS and validate post-synthesis functionality.  
2. Understand and summarize STA core principles.  
3. Use OpenSTA to analyze timing and interpret slack values.  
4. Relate functional and timing correctness in the SoC design flow.
