`timescale 1ns / 1ps

// 
module carry_save_adder_with_rca (
    input [3:0] A, B, C,
    output [3:0] Final_Sum,
    output Final_Cout
);

    wire [3:0] Sum_CSA, Carry_CSA;
    
    // Perform Carry Save Addition
    carry_save_adder_4bit csa (.A(A), .B(B), .C(C), .Sum(Sum_CSA), .Carry(Carry_CSA));
    
    // Shift Carry Left by 1 Bit
    wire [3:0] Carry_Shifted = {Carry_CSA[2:0], 1'b0}; 
    
    // Perform Ripple Carry Addition to get Final Result
    ripple_carry_adder_4bit rca (.A(Sum_CSA), .B(Carry_Shifted), .Cin(1'b0), .Sum(Final_Sum), .Cout(Final_Cout));

endmodule


module carry_save_adder_4bit (
    input [3:0] A, B, C,
    output [3:0] Sum,
    output [3:0] Carry
);

    // Sum and Carry generation using bitwise operations
    assign Sum = A ^ B ^ C;
    assign Carry = (A & B) | (B & C) | (A & C);

endmodule


module ripple_carry_adder_4bit (
    input [3:0] A, B,
    input Cin,
    output [3:0] Sum,
    output Cout
);
    wire C1, C2, C3;

    // Instantiate 4 Full Adders
    fulladder fa0 (.A(A[0]), .B(B[0]), .Cin(Cin), .Sum(Sum[0]), .Cout(C1));
    fulladder fa1 (.A(A[1]), .B(B[1]), .Cin(C1), .Sum(Sum[1]), .Cout(C2));
    fulladder fa2 (.A(A[2]), .B(B[2]), .Cin(C2), .Sum(Sum[2]), .Cout(C3));
    fulladder fa3 (.A(A[3]), .B(B[3]), .Cin(C3), .Sum(Sum[3]), .Cout(Cout));
endmodule


module fulladder (
    input A, B, Cin,
    output Sum, Cout
);
    assign Sum = A ^ B ^ Cin;
    assign Cout = (A & B) | (B & Cin) | (A & Cin);
endmodule
