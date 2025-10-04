# VSDBabySoC Week 2 Lab – Fundamentals & Functional Modelling

## Objective
Build a solid understanding of SoC fundamentals and practice functional modelling and simulation of the BabySoC using Icarus Verilog and GTKWave.

## Steps to Run

1. **Clone Repository**
    ```
    git clone https://github.com/YOUR_GITHUB/VSDBabySoC-Week2-Lab.git
    cd VSDBabySoC-Week2-Lab
    ```

2. **Simulation (Compilation + Run)**
    ```
    cd src
    make all
    ```

   Or, run manually (if Makefile not used):
    ```
    iverilog -o baby_soc_tb.vvp baby_soc_tb.v baby_soc.v other_modules.v
    vvp baby_soc_tb.vvp | tee ../logs/simulation.log
    ```

   This generates `baby_soc.vcd` in `waveforms/`.

3. **View Waveforms**
    ```
    gtkwave ../waveforms/baby_soc.vcd
    ```
    - Load signals: `reset`, `clk`, key state/data signals.

4. **Document Results**
    - Take screenshots (reset, clocking, dataflow).
    - Store in `screenshots/`.
    - Add concise explanations for each.

---


