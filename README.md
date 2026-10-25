# universal_shift_register
Behavioral level Verilog code for the  Universal shift register controlled by {S1,S0} with synchronous reset signal.

module shift(output serial_out,reg [3:0]pl_out,input din,rst,clk,s1,s0,[3:0]pl_in);

always@(posedge clk)
    if(rst) begin 
         pl_out<=4'd0;
    end
    else begin
        if({s1,s0}==2'b00)begin
            pl_out<=pl_out;
        end
     if({s1,s0}==2'b01)begin
       pl_out<={din,pl_out[3:1]};
    end
    if({s1,s0}==2'b10)begin
         pl_out<={pl_out[2:0],din};
    end
     if({s1,s0}==2'b11)begin
     pl_out<=pl_in;
    end
  end
assign serial_out=({s1,s0}==2'b01)?pl_out[0]:({s1,s0}==2'b10)?pl_out[3]:1'bx;
endmodule
