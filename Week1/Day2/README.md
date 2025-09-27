# Week 1 – Day 2  
**Timing Libraries, Hierarchical vs Flat Synthesis, and Efficient Flop Coding Styles**

---

## 1. Introduction to Timing `.lib` Files  

- A **timing library (.lib)** defines standard cell properties:  
  - Functional behavior (truth tables)  
  - Timing characteristics (delays, setup/hold times)  
  - Power information  
- Tools like **Yosys** and **OpenSTA** use `.lib` files during synthesis and timing analysis.  

---

## 2. Lab 4 – Introduction to `.lib`  

### Example: Reading a Timing Library in Yosys
~~~tcl
yosys
read_liberty -lib sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog and_gate.v
synth -top and_gate
dfflibmap -liberty sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty sky130_fd_sc_hd__tt_025C_1v80.lib
show
~~~

👉 This maps logic gates from RTL into the **Sky130 standard cell library**.  

---

## 3. Hierarchical vs Flat Synthesis  

- **Hierarchical synthesis** preserves module boundaries → easier debug, modular design, but may miss cross-module optimizations.  
- **Flat synthesis** flattens all modules into one → allows global optimization, but harder debug.  

---

## 4. Lab 5 – Hierarchical vs Flat Synthesis  

### Example: Hierarchical Design (`top.v`)  
~~~verilog
module sub1(input a, b, output y);
  assign y = a & b;
endmodule

module sub2(input a, b, output y);
  assign y = a | b;
endmodule

module top(input a, b, output y1, y2);
  sub1 u1(.a(a), .b(b), .y(y1));
  sub2 u2(.a(a), .b(b), .y(y2));
endmodule
~~~

#### Yosys Commands  
~~~tcl
yosys
read_verilog top.v
synth -top top -flatten 0   # hierarchical
show

synth -top top -flatten     # flat
show
~~~

👉 Compare schematics to observe difference in module preservation.  

---

## 5. Why Flops and Flop Coding Styles  

- **Flops (D Flip-Flops)** are fundamental sequential elements used to store state.  
- Efficient flop coding ensures proper synthesis and avoids mismatches.  

### Common Styles:  
1. **Simple DFF**  
2. **DFF with Reset**  
3. **DFF with Enable**  

---

## 6. Lab – Flo

