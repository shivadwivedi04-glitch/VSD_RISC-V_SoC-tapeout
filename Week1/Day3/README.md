# Week 1 – Day 3  
**Combinational and Sequential Optimizations**

---

## 1. Introduction to Optimizations  

During synthesis, tools like **Yosys** can simplify logic by removing redundancies, unused signals, or optimizing gate-level structures.  
Optimizations are performed in two major categories:  
- **Combinational Logic Optimizations**  
- **Sequential Logic Optimizations**  

---

## 2. Combinational Logic Optimizations  

These optimizations simplify Boolean expressions and remove unnecessary logic (e.g., redundant gates).  

### Example: Redundant Logic  
#### Original Code (`comb_red.v`)  
~~~verilog
module comb_red(input a, input b, output y);
  assign y = (a & b) | (a & b); // redundant logic
endmodule
~~~

#### Yosys Commands  
~~~tcl
yosys
read_verilog comb_red.v
synth -top comb_red
opt_clean
show
~~~

Yosys will optimize `(a & b) | (a & b)` to just `a & b`.  

---

## 3. Lab 6 – Combinational Logic Optimizations  

### Example: Simplifying Logic Expressions  
#### Verilog (`comb_opt.v`)  
~~~verilog
module comb_opt(input a, input b, input c, output y);
  assign y = (a & b) | (a & b & c); // redundant 'c'
endmodule
~~~

#### Yosys Flow  
~~~tcl
yosys
read_verilog comb_opt.v
synth -top comb_opt
opt_clean
show
~~~

Output will simplify to:  
`y = a & b`  

---

## 4. Sequential Logic Optimizations  

Sequential optimizations focus on reducing registers, eliminating unused outputs, and removing unnecessary state elements.  

---

## 5. Lab 7 – Sequential Logic Optimization  

### Example: Unused Registers  
#### Verilog (`seq_opt.v`)  
~~~verilog
module seq_opt(input clk, input d, output q);
  reg q_reg, unused;

  always @(posedge clk) begin
    q_reg <= d;
    unused <= d; // unused register
  end

  assign q = q_reg;
endmodule
~~~

#### Yosys Flow  
~~~tcl
yosys
read_verilog seq_opt.v
synth -top seq_opt
opt_clean
show
~~~

Yosys will remove the `unused` register since it has no fanout.  

---

## 6. Sequential Optimization – Unused Outputs  

Optimizations also eliminate logic driving signals that are never used.  
This reduces circuit area and improves efficiency.  

---

✅ End of **Day 3**

