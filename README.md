# 4-bit-updown-counter

module auti(input clk, reset,up_down, output[3:0]  counter
    );
reg [3:0] counter_up_down;

// down counter
always @(posedge clk or posedge reset)
begin
if(reset)
 counter_up_down <= 4'h0;
else if(~up_down)
 counter_up_down <= counter_up_down + 4'd1;
else
 counter_up_down <= counter_up_down - 4'd1;
end 
assign counter = counter_up_down;
endmodule

Code for testbench

module snehal;

	// Inputs
	reg clk;
	reg reset;
	reg up_down;

	// Outputs
	wire [3:0] counter;

	// Instantiate the Unit Under Test (UUT)
	auti uut (
		.clk(clk), 
		.reset(reset), 
		.up_down(up_down), 
		.counter(counter)
	);
	initial begin 
clk=0;
forever #5 clk=~clk;
end

	initial begin
	reset=1;
up_down=0;
#20;
reset=0;
#200;
up_down=1;

	end
      
endmodule


Code for ucf

  NET "counter[0]"             LOC = P46   | IOSTANDARD = LVCMOS33 | SLEW = SLOW | DRIVE = 12;
    NET "counter[1]"             LOC = P47   | IOSTANDARD = LVCMOS33 | SLEW = SLOW | DRIVE = 12;
    NET "counter[2]"             LOC = P48   | IOSTANDARD = LVCMOS33 | SLEW = SLOW | DRIVE = 12;
    NET "counter[3]"             LOC = P49   | IOSTANDARD = LVCMOS33 | SLEW = SLOW | DRIVE = 12;
	  NET "Clk"                  LOC = P129  | IOSTANDARD = LVCMOS33 | PERIOD = 12MHz;
	    NET "up_down"        LOC = P70   | PULLUP  | IOSTANDARD = LVCMOS33 | SLEW = SLOW | DRIVE = 12;
    NET "reset"        LOC = P69   | PULLUP  | IOSTANDARD = LVCMOS33 | SLEW = SLOW | DRIVE = 12;
