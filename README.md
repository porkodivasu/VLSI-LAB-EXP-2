
EXPERIMENT - 2:

SIMULATION AND IMPLEMENTATION OF  COMBINATIONAL LOGIC CIRCUITS

AIM:

 To simulate and synthesis ENCODER, DECODER, MULTIPLEXER, DEMULTIPLEXER, MAGNITUDE COMPARATOR using Xilinx ISE.

APPARATUS REQUIRED:

Xilinx 14.7
Spartan6 FPGA


PROCEDURE:


STEP:1  Start  the Xilinx navigator, Select and Name the New project.


STEP:2  Select the device family, device, package and speed.


STEP:3  Select new source in the New Project and select Verilog Module as the Source type.


STEP:4  Type the File Name and Click Next and then finish button. Type the code and save it.


STEP:5  Select the Behavioral Simulation in the Source Window and click the check syntax.


STEP:6  Click the simulation to simulate the program and  give the inputs and verify the outputs as per the truth table.   


STEP:7  Select the Implementation in the Sources Window and select the required file in the Processes Window.


STEP:8  Select Check Syntax from the Synthesize  XST Process. Double Click in the  FloorplanArea/IO/Logic-Post Synthesis process in the User Constraints process group. UCF(User constraint File) is obtained. 


STEP:9  In the Design Object List Window, enter the pin location for each pin in the Loc column Select save from the File menu.


STEP:10 Double click on the Implement Design and double click on the Generate Programming File to create a bitstream of the design.(.v) file is converted into .bit file here.


STEP:11  On the board, by giving required input, the LEDs starts to glow light, indicating the output.


**LOGIC DIAGRAM**


ENCODER

![image](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/6987778/3cd1f95e-7531-4cad-9154-fdd397ac439e)


VERILOG CODE

```
module encoder(
  input [7:0] D,
  output [2:0] y);
  
  assign y[2] = D[4] | D[5] | D[6] | D[7];
  assign y[1] = D[2] | D[3] | D[6] | D[7];
  assign y[0] = D[1] | D[3] | D[5] | D[7];
endmodule
```

OUTPUT WAVEFORM:


 ![Screenshot (21)](https://github.com/porkodivasu/VLSI-LAB-EXP-2/assets/160757120/28e614f0-1989-48d7-97b6-ac75309861dd)

DECODER

![image](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/6987778/45a5e6cf-bbe0-4fd5-ac84-e5ad4477483b)

 VERILOG CODE:
 
```
   module decoder(
  input [2:0] D,
  output reg [7:0] y);
  
  always@(D) begin
    y = 0;
    case(D)
      3'b000: y[0] = 1'b1;
      3'b001: y[1] = 1'b1;
      3'b010: y[2] = 1'b1;
      3'b011: y[3] = 1'b1;
      3'b100: y[4] = 1'b1;
      3'b101: y[5] = 1'b1;
      3'b110: y[6] = 1'b1;
      3'b111: y[7] = 1'b1;
      default: y = 0;
    endcase
  end
endmodule
```

OUTPUT WAVEFORM:

![Screenshot (28)](https://github.com/porkodivasu/VLSI-LAB-EXP-2/assets/160757120/72263be6-0dd4-4b71-a4fc-710b13aaf3c6)


MULTIPLEXER:

![image](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/6987778/427f75b2-8e67-44b9-ac45-a66651787436)

VERILOG CODE:

```
module multi(i,s,y);
input[7:0]i;
input[2:0]s;
output reg y;
always@(*)
begin
case({s[2],s[1],s[0]})
3'b000:y=i[0];
3'b001:y=i[1];
3'b010:y=i[2];
3'b011:y=i[3];
3'b100:y=i[4];
3'b101:y=i[5];
3'b110:y=i[6];
3'b111:y=i[7];
endcase end
endmodule
```
OUTPUT WAVEFORM:


![Screenshot (86)](https://github.com/porkodivasu/VLSI-LAB-EXP-2/assets/160757120/f514f0f2-a320-4a40-b9ac-dc217ceec89a)


DEMULTIPLEXER

![image](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/6987778/1c45a7fc-08ac-4f76-87f2-c084e7150557)

VERILOG CODE:

```
module demultiplexer(d1,d2,d3,d4,d5,d6,d7,d8,i,s0,s1,s2);
input i,s0,s1,s2;
output d1,d2,d3,d4,d5,d6,d7,d8;
wire w1,w2,w3;
not g1(w1,s0);
not g2(w2,s1);
not g3(w3,s2);
and g4(d1,w1,w2,w3,i);
and g5(d2,w1,w2,s2,i);
and g6(d3,w1,s1,w3,i);
and g7(d4,w1,s1,s2,i);
and g8(d5,s0,w2,w3,i);
and g9(d6,s0,w2,s2,i);
and g10(d7,s0,s1,w3,i);
and g11(d8,s0,s1,s2,i);
endmodule
```

OUTPUT WAVEFORM:


![Screenshot (27)](https://github.com/porkodivasu/VLSI-LAB-EXP-2/assets/160757120/bf937f95-6e99-4885-a392-f494594c5d86)


MAGNITUDE COMPARATOR

![image](https://github.com/navaneethans/VLSI-LAB-EXP-2/assets/6987778/b2fe7a05-6bf7-4dcb-8f5d-28abbf7ea8c2)

VERILOG CODE:

```
module comparator(
  input [3:0] A, B,
  output reg A_grt_B, A_less_B, A_eq_B);
  
  always@(*) begin
    A_grt_B = 0; A_less_B = 0; A_eq_B = 0;
    if(A>B) A_grt_B = 1'b1;
    else if(A<B) A_less_B = 1'b1;
    else A_eq_B = 1'b1;
  end
endmodule
```

OUTPUT WAVEFORM:


![Screenshot (31)](https://github.com/porkodivasu/VLSI-LAB-EXP-2/assets/160757120/e1e78e69-c092-49e3-93e9-21de65fd7d6d)


RESULT

Thus the simulation and synthesis of ENCODER, DECODER, MULTIPLEXER,
DEMULTIPLEXER, 2bit MAGNITUDE COMPARATOR using vivado is successfully
completed and executed.


