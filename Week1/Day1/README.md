# Week 1 – Day 1  
**Lab 1: Introduction to Verilog RTL Design and Synthesis**

---

## 1. Introduction to Open Source Simulator – Icarus Verilog (iverilog) and GTKWave

Icarus Verilog (iverilog) is an open-source Verilog simulation tool, while GTKWave is a waveform viewer used to visualize simulation outputs.

### Steps
1. Install iverilog and GTKWave:
   ~~~bash
   sudo apt update
   sudo apt install iverilog gtkwave
   ~~~

2. Write a simple Verilog file (`hello.v`):
   ~~~verilog
   module hello;
     initial begin
       $display("Hello, RISC-V with Verilog!");
       $finish;
     end
   endmodule
   ~~~

3. Compile and run:
   ~~~bash
   iverilog hello.v -o hello
   ./hello
   ~~~

---

## 2. Lab 2 – Using iverilog and GTKWave

### Example: AND Gate

1. Write the Verilog code (`and_gate.v`):
   ~~~verilog
   module and_gate(input a, input b, output y);
     assign y = a & b;
   endmodule
   ~~~

2. Write the testbench (`and_tb.v`):
   ~~~verilog
   module and_tb;
     reg a, b;
     wire y;

     and_gate uut(.a(a), .b(b), .y(y));

     initial begin
       $dumpfile("and.vcd");
       $dumpvars(0, and_tb);
       a=0; b=0; #10;
       a=0; b=1; #10;
       a=1; b=0; #10;
       a=1; b=1; #10;
       $finish;
     end
   endmodule
   ~~~

3. Compile and simulate:
   ~~~bash
   iverilog and_gate.v and_tb.v -o and_tb
   ./and_tb
   gtkwave and.vcd
   ~~~

---

## 3. Introduction to Yosys and Logic Synthesis

Yosys is an open-source framework for RTL synthesis.  
Skywater SKY130 is an open-source PDK (Process Design Kit) used for ASIC design.

### Install Yosys
   ~~~bash
   sudo apt install yosys
   ~~~

---

## 4. Lab 3 – Using Yosys and SKY130 PDKs (Yosys 1: Good MUX)

### Example: 2:1 Multiplexer

1. Write `mux.v`:
   ~~~verilog
   module mux2to1(input a, input b, input sel, output y);
     assign y = sel ? b : a;
   endmodule
   ~~~

2. Run Yosys synthesis:
   ~~~tcl
   yosys
   read_verilog mux.v
   synth -top mux2to1
   show
   ~~~

This will generate a synthesized netlist and schematic using Yosys + Sky130 libraries.

---

✅ End of **Day 1**

