# Week 1 – Day 4  
**Gate-Level Simulation (GLS), Blocking vs Non-Blocking, and Synthesis-Simulation Mismatch**

---

## 1. GLS Concepts and Flow using Icarus Verilog (iverilog)

**Gate-Level Simulation (GLS)** is the simulation of the synthesized netlist instead of the RTL code.  
It helps verify:  
- Timing behavior of gates  
- Correctness after synthesis  
- Mismatches between RTL simulation and synthesized logic  

### GLS Flow
1. Write RTL code (`rtl.v`)  
2. Write testbench (`tb.v`)  
3. Run RTL simulation with `iverilog`  
4. Synthesize RTL using Yosys → gate-level netlist  
5. Simulate gate-level netlist with `iverilog`  

### Example: Simple AND Gate GLS
#### Verilog (`rtl.v`)
~~~verilog
module and_gate(input a, input b, output y);
  assign y = a & b;
endmodule
~~~

#### Testbench (`tb.v`)
~~~verilog
module tb;
  reg a, b;
  wire y;

  and_gate uut(.a(a), .b(b), .y(y));

  initial begin
    $dumpfile("gls.vcd");
    $dumpvars(0, tb);
    a=0; b=0; #10;
    a=0; b=1; #10;
    a=1; b=0; #10;
    a=1; b=1; #10;
    $finish;
  end
endmodule
~~~

#### Yosys Synthesis + GLS
~~~tcl
yosys
read_verilog rtl.v
synth -top and_gate
write_verilog netlist.v
~~~

~~~bash
iverilog netlist.v tb.v -o gls_sim
./gls_sim
gtkwave gls.vcd
~~~

---

## 2. Synthesis-Simulation Mismatch: Blocking vs Non-Blocking Statements

In Verilog:  
- **Blocking (`=`)** executes statements sequentially.  
- **Non-blocking (`<=`)** schedules assignments to occur concurrently.  

Improper use can cause **RTL simulation and synthesized netlist mismatch**.  

---

## 3. Caveats with Blocking Statements  

Example where blocking assignment causes mismatch:  

#### RTL Code (`block_mismatch.v`)  
~~~verilog
module block_mismatch(input clk, input d, output reg q1, output reg q2);
  always @(posedge clk) begin
    q1 = d;   // blocking
    q2 = q1;  // q2 gets updated with old q1 in RTL sim
  end
endmodule
~~~

- **RTL Simulation:** `q2` lags one cycle behind `q1`.  
- **Synthesized Netlist:** Both `q1` and `q2` may update in the same cycle.  

---

## 4. Lab – GLS Synthesis-Simulation Mismatch  

Run both RTL simulation and GLS on the same code. Compare waveforms in GTKWave to observe mismatches.  

---

## 5. Lab – Synthesis-Simulation Mismatch with Blocking Statement  

1. Write Verilog with blocking assignments (like above).  
2. Run RTL simulation → observe expected output.  
3. Run synthesis + GLS → observe mismatched behavior.  

This demonstrates why **non-blocking assignments (`<=`)** are recommended for sequential logic.  

---

✅ End of **Day 4**

