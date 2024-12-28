---
layout: project
type: project
image: img/projects/ALU/Title.png
title: "4-Bit Arithmetic Logic Unit (ALU)"
date: 2022
published: true
labels:
  - Digital Circuit Design
  - Verilog HDL
  - Combinational Logic
  - Computer Architecture
summary: "Design and implementation of a 4-bit ALU supporting 8 arithmetic and logical operations using Verilog and circuit simulation."
---

<div class="text-center p-4">
  <img width="400px" src="../img/projects/ALU/1.jpg" class="img-thumbnail" >
  <p class="fst-italic">Complete ALU circuit implementation in Falstad simulator</p>
</div>

## Project Overview
This project involved designing and implementing a 4-bit Arithmetic Logic Unit (ALU) capable of performing eight distinct operations. The ALU supports fundamental computer arithmetic including addition, subtraction, multiplication, division, and bitwise operations. The design process involved both hardware simulation using Falstad circuit simulator and Hardware Description Language (HDL) implementation using Verilog.

Source code available at: [GitHub Repository](https://github.com/XiaoKChenEdu/ALU)

## Design Process
Each operation was first prototyped individually in Falstad to verify the logic and ensure correct functionality. The subcircuits were then combined using multiplexers to create the complete ALU. The design follows these specifications:

- Input width: 4 bits (A, B inputs)
- Operation selection: 3 bits (allowing 8 operations)
- Carry in support (XIN)
- Status flags: Zero (Z), Overflow (V), Carry out (C)

<div class="text-center p-4">
  <img width="400px" src="../img/projects/ALU/2.jpg" class="img-thumbnail" >
  <p class="fst-italic">4-bit adder subcircuit implementation</p>
</div>

## Supported Operations
The ALU implements the following operations selected by the 3-bit control signal (S):
- 000: Addition (A + B + XIN)
- 001: Subtraction (B - A + XIN)
- 010: Subtraction (A - B + XIN)
- 011: Multiplication by 2 (A × 2)
- 100: Division by 2 (A ÷ 2)
- 101: Multiplication (A × B)
- 110: XOR (A ⊕ B)
- 111: Compare (A < B)

<div class="text-center p-4">
  <img width="400px" src="../img/projects/ALU/3.jpg" class="img-thumbnail" >
  <p class="fst-italic">Complete ALU integration with multiplexer control</p>
</div>

## Verilog Implementation
The ALU was implemented in Verilog HDL, incorporating all operations and status flags. The implementation includes:

```v
module fourBitALU (
    input XIN,              // Carry input
    input [3:0] A, B,      // 4-bit operands
    input [2:0] S,         // Operation select
    output reg Z,          // Zero flag
    output reg V,          // Overflow flag
    output reg C,          // Carry flag
    output reg [3:0] F     // Result output
);

    // Temporary variables for calculations
    reg [4:0] temp;
    reg [7:0] mult;

    always @(*) begin
        // Default assignments
        {C, F} = 5'b0;
        V = 1'b0;
        
        case(S)
            3'b000: {C, F} = A + B + XIN;           // Addition
            3'b001: {C, F} = B - A + XIN;           // Subtraction (B-A)
            3'b010: {C, F} = A - B + XIN;           // Subtraction (A-B)
            3'b011: {C, F} = A << 1;                // Multiply by 2
            3'b100: F = A >> 1;                      // Divide by 2
            3'b101: begin                            // Multiplication
                mult = A * B;
                F = mult[3:0];
                C = |mult[7:4];                      // Carry if upper bits non-zero
            end
            3'b110: F = A ^ B;                      // XOR
            3'b111: F = {3'b000, A < B};            // Compare
        endcase

        // Set zero flag
        Z = (F == 4'b0000);
        
        // Set overflow flag for arithmetic operations
        if (S <= 3'b010) begin
            case(S)
                3'b000: V = (~A[3] & ~B[3] & F[3]) | (A[3] & B[3] & ~F[3]);
                3'b001, 3'b010: V = (~A[3] & B[3] & F[3]) | (A[3] & ~B[3] & ~F[3]);
            endcase
        end
    end
endmodule
```

## Testing and Validation
The ALU was thoroughly tested using a testbench that verified:
- All arithmetic operations with various input combinations
- Correct flag generation (Zero, Overflow, Carry)
- Edge cases handling
- Timing requirements

## Learning Outcomes
This project provided hands-on experience with:
- Digital circuit design principles
- HDL implementation techniques
- Testing and verification methodologies
- Computer arithmetic concepts
- Hardware simulation tools

The combination of both circuit simulation and HDL implementation helped reinforce understanding of digital logic design principles and their practical applications.
