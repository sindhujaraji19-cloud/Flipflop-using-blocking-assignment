# EXPERIMENT 3A: Simulation of All Flip-Flops using Blocking Statement

## AIM
To design and simulate basic flip-flops (SR, D, JK, and T) using **blocking statements** in Verilog HDL, and verify their functionality through simulation in Vivado 2023.1.

## APPARATUS REQUIRED
- Vivado 2023.1
- Computer with HDL Simulator

## DESCRIPTION
Flip-flops are the basic memory elements in sequential circuits.  
In this experiment, different types of flip-flops (SR, D, JK, T) are modeled using **behavioral modeling** with **blocking assignment (`=`)** inside the `always` block.  
Blocking assignments execute sequentially in the given order, which makes it easier to describe simple synchronous circuits.

## PROCEDURE
1. Open **Vivado 2023.1**.  
2. Create a **New RTL Project** (e.g., `FlipFlop_Simulation`).  
3. Add Verilog source files for each flip-flop (SR, D, JK, T).  
4. Add a testbench file to verify all flip-flops.  
5. Run **Behavioral Simulation**.  
6. Observe waveforms of inputs and outputs for each flip-flop.  
7. Verify that outputs match the truth table.  
8. Save results and capture simulation screenshots.

---

## VERILOG CODE

### SR Flip-Flop (Blocking)
```verilog
`timescale 1ns / 1ps


module srff(s,r,clk,rst,q);
input s,r,clk,rst;
output reg q;
always @ (posedge clk)
begin
if (rst==1)
q=0;
else if(s==0 && r==0)
q=q;
else if(s==0 && r==1)
q=1'b0;
else if(s==1 && r==0)
q=1'b1;
else
q=1'bx;
end
endmodule

```
### SR Flip-Flop Test bench 
```verilog
module srff_tb;
reg s,r,clk,rst;
wire q;
srff uut(s,r,clk,rst,q);
always #5 clk=~clk;
initial
begin
clk=0;
s=0;r=0;
rst=1;
#10 rst=0;
#10 s=1;r=0; //set
#10 s=0;r=0; //hold
#10 s=0;r=1; //reset
#10 s=1;r=1; //invalid condition
#10 s=1;r=0; //hold
#20 $finish;
end
endmodule






```
#### SIMULATION OUTPUT

------- paste the output here -------
---<img width="1917" height="1199" alt="Screenshot 2025-09-26 083233" src="https://github.com/user-attachments/assets/d2f23bcb-3281-4504-a86d-db14c50b6481" />


### JK Flip-Flop (Blocking)
```verilog
`timescale 1ns / 1ps


module jkflipflop(j,k,clk,rst,q);
input j,k,clk,rst;
output reg q;
always @ (posedge clk)
begin
if (rst==1)
q=0;
else if(j==0 && k==0)
q=q;
else if(j==0 && k==1)
q=1'b0;
else if(j==1 && k==0)
q=1'b1;
else
q=~q;
end
endmodule
```
### JK Flip-Flop Test bench 
```verilog


module jkfliplflop_tb;
reg j,k,clk,rst;
wire q;
jkflipflop uut(j,k,clk,rst,q);
always #5 clk=~clk;
initial
begin
clk=0;
j=0;k=0;
rst=1;
#10 rst=0;
#10 j=1;k=0; //set
#10 j=0;k=0; //hold
#10 j=0;k=1; //reset
#10 j=1;k=1; //invalid condition
#10 j=1;k=0; //hold
#20 $finish;
end
endmodule





```
#### SIMULATION OUTPUT

------- paste the output here -------
---<img width="1904" height="1199" alt="Screenshot 2025-09-26 083724" src="https://github.com/user-attachments/assets/d2635a45-75ba-4d9a-af6f-7fd8d4bb85d5" />

### D Flip-Flop (Blocking)
```verilog
`timescale 1ns / 1ps


module dflipflop(d,clk,rst,q);
input d,clk,rst;
output reg q;
always @ (posedge clk)
begin
if (rst==1)
q=0;
else if(d==0)
q=0;
else
q=1;
end
endmodule

```
### D Flip-Flop Test bench 
```verilog


module jkfliplflop_tb;
reg j,k,clk,rst;
wire q;
jkflipflop uut(j,k,clk,rst,q);
always #5 clk=~clk;
initial
begin
clk=0;
j=0;k=0;
rst=1;
#10 rst=0;
#10 j=1;k=0; //set
#10 j=0;k=0; //hold
#10 j=0;k=1; //reset
#10 j=1;k=1; //invalid condition
#10 j=1;k=0; //hold
#20 $finish;
end
endmodule






```

#### SIMULATION OUTPUT

------- paste the output here -------
---<img width="1898" height="1131" alt="Screenshot 2025-09-26 084258" src="https://github.com/user-attachments/assets/92f5a587-fee6-49fd-9e56-7f342eaa73c2" />

### T Flip-Flop (Blocking)
```verilog

`timescale 1ns / 1ps
module tflipflop(t,clk,rst,q);
input t,clk,rst;
output reg q;
always @ (posedge clk)
begin
if (rst==1)
q=0;
else if(t==0)
q=q;
else
q=~q;
end
endmodule

```
### T Flip-Flop Test bench 
```verilog
module tfliplflop_tb;
reg t,clk,rst;
wire q;
tflipflop uut(t,clk,rst,q);
always #5 clk=~clk;
initial
begin
clk=0;
t=0;
rst=1;
#10 rst=0;t=0;
#10 t=1;
#20 $finish;
end
endmodule








```

#### SIMULATION OUTPUT

------- paste the output here -------

---<img width="1851" height="1082" alt="Screenshot 2025-09-26 084319" src="https://github.com/user-attachments/assets/3a405ecc-1f33-4d25-9876-66867f8ce884" />


### RESULT

All flip-flops (SR, D, JK, T) were successfully simulated using blocking statements in Verilog HDL.
The outputs matched the expected truth table values, demonstrating correct sequential behavior.
