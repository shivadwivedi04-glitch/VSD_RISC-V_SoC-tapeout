# Week 1 – Day 5  
**Optimizations in Synthesis: If/Case Constructs, Loops, and Generate Statements**

---

## 1. Optimization in Synthesis – If and Case Constructs  

Synthesis tools optimize conditional statements (`if`, `case`) by simplifying unreachable logic or by generating multiplexers.  
⚠️ Incorrectly written conditions may lead to **latches** or **unintended hardware**.  

---

## 2. Lab – Incomplete If  

If an `if` block does not specify all possible cases, synthesis may infer **latches** to hold the missing conditions.  

### Example: Incomplete If (`incomplete_if.v`)  
~~~verilog
module incomplete_if(input en, input d, output reg q);
  always @(*) begin
    if (en)
      q = d;   // no else branch → latch inferred
  end
endmodule
~~~

#### Yosys Flow  
~~~tcl
yosys
read_verilog incomplete_if.v
synth -top incomplete_if
show
~~~

👉 You will see a **latch element** in the synthesized schematic.  

---

## 3. Lab – Incomplete / Overlapping Case  

### Example: Incomplete Case (`incomplete_case.v`)  
~~~verilog
module incomplete_case(input [1:0] sel, output reg y);
  always @(*) begin
    case(sel)
      2'b00: y = 0;
      2'b01: y = 1;
      // missing 2'b10 and 2'b11 → latch inferred
    endcase
  end
endmodule
~~~

### Example: Overlapping Case (`overlap_case.v`)  
~~~verilog
module overlap_case(input [1:0] sel, output reg y);
  always @(*) begin
    case(sel)
      2'b0?: y = 1;   // matches 00 and 01
      2'b01: y = 0;   // overlapping condition
    endcase
  end
endmodule
~~~

👉 Overlapping cases cause **priority encoders** or unintended optimizations in synthesis.  

---

## 4. For Loop vs For-Generate  

- **For loop inside `always`** → replicated sequentially in simulation, used for behavioral modeling.  
- **Generate-for** → creates multiple hardware blocks in parallel at synthesis.  

---

## 5. Lab – For Loop vs Generate For  

### Example: For Loop (`for_loop.v`)  
~~~verilog
module for_loop(input [3:0] a, output reg [3:0] y);
  integer i;
  always @(*) begin
    for (i=0; i<4; i=i+1) begin
      y[i] = ~a[i];  // invert each bit
    end
  end
endmodule
~~~

### Example: Generate For (`for_gen.v`)  
~~~verilog
module for_gen #(parameter N=4) (input [N-1:0] a, output [N-1:0] y);
  genvar i;
  generate
    for (i=0; i<N; i=i+1) begin : gen_inv
      assign y[i] = ~a[i];
    end
  endgenerate
endmodule
~~~

👉 Both achieve the same function, but `generate` explicitly instantiates multiple hardware blocks, while `for` in an `always` block is behavioral.  

---

✅ End of **Week 1**

