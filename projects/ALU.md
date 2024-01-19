---
layout: project
type: project
image: img/projects/SCADA-Water-System/Title.png
title: "ALU"
date: 2022
published: true
labels:
  - Circuit Design
  - Verilog
summary: "Designing a combinational digital circuit with 8 operations, each operations are 4 bit."
---

<div class="text-center p-4">
  <img width="400px" src="../img/projects/ALU/1.jpg" class="img-thumbnail" >
</div>

In this project, my main objective was to design a four-bit ALU circuit capable of performing eight distinct operations, including addition, subtraction, multiplication, division, and various bitwise operations. I individually implemented each of these eight operations on Falstad, a circuit simulator applet, to create a subcircuit design. This design was subsequently used to construct a four-bit version of the circuit, as depicted in the image below.

<div class="text-center p-4">
  <img width="400px" src="../img/projects/ALU/2.jpg" class="img-thumbnail" >
</div>

The image above depicts one of the eight distinct circuits that have been assembled. Specifically, the displayed circuit performs the adder operation of the Arithmetic Logic Unit (ALU). After constructing eight separate subcircuits, I integrated them using a multiplexer to form the ALU. At the same time, I also implement a version of the ALU in verilog.

<div class="text-center p-4">
  <img width="400px" src="../img/projects/ALU/3.jpg" class="img-thumbnail" >
</div>

Here is the code that illustrates the four bit ALU in verilog:

```v
///// FOURBITALU /////


module fourBitALU ( XIN, A, B ,S, Z, V, C, F ) ;

  input  wire         XIN     ;
  input  wire [ 3:0 ] A, B    ;
  input  wire [ 2:0 ] S       ;
  output wire         Z, V, C ;
  output wire [ 3:0 ] F       ;

  reg [ 7:0 ] temp_F             ;
  reg         overFlow, carryOut ;

  always @ ( S )
    begin

      carryOut = 1'b0 ;

      case ( S )

        3'b000   : 
          
          begin
          
            temp_F   = A + B + XIN ;
            carryOut = temp_F[ 4 ] ;

          end
        
        3'b001  : 
          
          begin

            temp_F   = ( B + XIN ) - A ;
            carryOut = temp_F[ 4 ]     ;

          end

        3'b010  : 

          begin
        
            temp_F   = ( A + XIN ) - B ;
            carryOut = temp_F[ 4 ]     ;

          end

        3'b011  : temp_F = 4'b0010 * A     ;
        3'b100  : temp_F = A / 4'b0010     ;
        3'b101  : temp_F = A * B           ;
        3'b110  : temp_F = A ^ B           ;
        3'b111  :
        
          begin

            if ( A < B ) begin

              temp_F = 8'b00001111 ;

            end else begin

              temp_F = 8'b00000000 ;

            end

          end

        default : temp_F = 8'b00000000     ;

      endcase

    end

    assign F = temp_F ;
    assign Z = ( temp_F == 8'b00000000 ) ? 1'b1 :
               1'b0 ;
    assign V = ( temp_F[ 4 ] == 1'b1 ) ? 1'b1 :
               ( temp_F[ 5 ] == 1'b1 ) ? 1'b1 :
               ( temp_F[ 6 ] == 1'b1 ) ? 1'b1 :
               ( temp_F[ 7 ] == 1'b1 ) ? 1'b1 :
               1'b0 ;
    assign C = carryOut ;


endmodule


///// FOURBITALU /////
```
