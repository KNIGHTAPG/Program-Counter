//4bit PC using verilog

////////////////////////////////////////////////////////////////////

`timescale 1ns / 1ps
module buttonCounter(btnC,load_btn,data_in,reset_btn,clk,seg,an);
input clk;
input btnC;
input reset_btn;
input load_btn;//store_btn;
input [3:0] data_in ;
output [7:0] seg;
output reg [3:0] an;
wire btn_clr;
reg prevbtn;
//reg [3:0]counter=4'b0000;

reg [15:0] counter = 16'h0000;
reg [15:0] stored_value = 16'h0000;
reg [3:0]  data_out;

decoder_7seg ss(.in1(counter),.out1(seg));
debounce uut(.clk(clk),.btn(btnC),.btn_clr(btn_clr));


always @(posedge clk)
begin
an=4'b1110;
    
  if (reset_btn) begin
        counter <= 16'h0000;
        end //else 
        //if (store_btn) begin
      // data_out <= data_in; end
       // Store current counter value
    else if (load_btn) begin
       counter <= data_in ; // Load stored value into counter
    end
      else 
if (btn_clr!=prevbtn && btn_clr==1)
    begin
    counter<=counter+16'h0001;
    if (counter==16'h000f)
        counter<=16'h0000;
    end
prevbtn<=btn_clr;
end
endmodule

////////////////////////////////////////////////////////////////////////////////////////

`timescale 1ns / 1ps
module debounce(clk,btn,btn_clr);
input clk;
input btn;
output reg btn_clr;
parameter delay = 650000; //6.5 ms delay
integer count =0;
reg xnew=0;
always @(posedge clk)
begin 
if (btn != xnew) begin
	count <=0;
	xnew<=btn;
end 
else if (count == delay) btn_clr <=xnew;
else count <=count+1;
end endmodule

/////////////////////////////////////////////////////////////////////////////////////////

`timescale 1ns / 1ps
module decoder_7seg(in1,out1);
input [15:0] in1;
//input [3:0] in1;
output reg [7:0] out1;

always @ (in1)
	case (in1[3:0])
4'b0000: out1 = 8'b11000000;  // 0  
4'b0001: out1 = 8'b11111001;  // 1  
4'b0010: out1 = 8'b10100100;  // 2  
4'b0011: out1 = 8'b10110000;  // 3  
4'b0100: out1 = 8'b10011001;  // 4
4'b0101: out1 = 8'b10010010;  // 5
4'b0110: out1 = 8'b10000010;  // 6
4'b0111: out1 = 8'b11111000;  // 7
4'b1000: out1 = 8'b10000000;  // 8
4'b1001: out1 = 8'b10011000;  // 9
4'b1010: out1 = 8'b10001000;  // A
4'b1011: out1 = 8'b10000011;  // B
4'b1100: out1 = 8'b11000110;  // C
4'b1101: out1 = 8'b10100001;  // D
4'b1110: out1 = 8'b10000110;  // E
4'b1111: out1 = 8'b10001110;  // F

endcase
endmodule
