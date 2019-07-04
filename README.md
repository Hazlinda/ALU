# ALU
ALU design.sv



    module ALU8bit (opcode, operand1, operand2, result, flagC, flagZ);
  
      input [2:0] opcode;
      input [7:0] operand1, operand2;
      output reg[15:0] result;
      output reg flagC, flagZ;
  
      parameter [2:0] Add = 3'b000,Sub = 3'b001,Mul = 3'b010,And = 3'b011,Or = 3'b100,Nand = 3'b101,Nor = 3'b110,Xor = 3'b111;
  
      always @(opcode or operand1 or operand2)
        begin
          case (opcode)
        
            Add:begin
                result = operand1 + operand2;
                flagC = result[8];
                flagZ = (result == 16'b0);
                end
            Sub:begin
                result = operand1 - operand2;
                flagC = result[8];
                flagZ = (result == 16'b0);
                end
            Mul:begin
                result = operand1 * operand2;
                flagZ = (result == 16'b0);
                end
            And:begin
                result = operand1 & operand2;
                flagZ = (result == 16'b0);
                end
            Or:begin
                result = operand1 | operand2;
                flagZ = (result == 16'b0);
                end
            Nand:begin
                result = ~(operand1 & operand2);
                flagZ = (result == 16'b0);
                end
            Nor:begin
                result = ~(operand1 | operand2);
                flagZ = (result == 16'b0);
                end
            Xor:begin
                result = operand1 ^ operand2;
                flagZ = (result == 16'b0);
                end
           default:begin
             result=16'b0;
             flagC=1'b0;
             flagZ=1'b0;
          end
       endcase
    end 
    endmodule 
    
    
 Testbench for ALU:
 
 
        module ALU8bit_tb;
        reg [2:0] Opcode;
        reg [7:0] Operand1, Operand2;
        wire [15:0] Result;
        wire FlagC;
        wire FlagZ;
  
        //temporary memory
        reg[2:0] count = 3'b0;
        //integer i;
  
        //instantiate with UUT
        ALU8bit my_uut (.opcode(Opcode),.operand1(Operand1), .operand2(Operand2),.result(Result),.flagC(FlagC),.flagZ(FlagZ));
  
           initial begi
            // Dump waves
                $dumpfile("dump.vcd");
                $dumpvars(1);

           // Initialize Inputs

            Opcode   = 3'b0;
            Operand1 = 8'd0;
            Operand2 = 8'd0;

        // Wait 100 ns for global reset to finish
        #100;    

        // Add stimulus here  

        Operand1 = 8'hAA;
        Operand2 = 8'h55;  

    for (count = 0; count < 8; count = count + 1'b1) 

        begin
        Opcode = count;
        #20;
        end

        end     

     endmodule


EDA playground link:
https://www.edaplayground.com/x/3Ejf
