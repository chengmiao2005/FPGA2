module decoder_case_a1(
    input wire in1,
    input wire in2,
    input wire in3,
    output reg [7:0] out
);

always @(*) begin
    if ({in3, in2, in1} == 3'b000) out = 8'b00000001;
    if ({in3, in2, in1} == 3'b001) out = 8'b00000010;
    if ({in3, in2, in1} == 3'b010) out = 8'b00000100;
    if ({in3, in2, in1} == 3'b011) out = 8'b00001000;
    if ({in3, in2, in1} == 3'b100) out = 8'b00010000;
    if ({in3, in2, in1} == 3'b101) out = 8'b00100000;
    if ({in3, in2, in1} == 3'b110) out = 8'b01000000;
    if ({in3, in2, in1} == 3'b111) out = 8'b10000000;
end
endmodule



module tb_decoder_case_a1();
    reg in1;
    reg in2;
    reg in3;
    wire [7:0] out;
    reg [2:0] test_vector;
    reg [7:0] expected_out;
    integer i;
    decoder_case_a1 uut (
        .in1(in1),
        .in2(in2),
        .in3(in3),
        .out(out)
    );
    reg clk;
    initial begin
        clk = 0;
        forever #10 clk = ~clk;
    end
    initial begin
        in1 = 0;
        in2 = 0;
        in3 = 0;
        $display("开始测试 decoder_case_a1 模块...");
        $display("时间 | in3 in2 in1 | 实际输出 | 预期输出 | 结果");
        $display("------------------------------------------------");
        for (i = 0; i < 8; i = i + 1) begin
            test_vector = i;
            {in3, in2, in1} = test_vector;
            expected_out = 8'b00000001 << i;
            #10; 
            $display("%4t |  %b   %b   %b  |  %b |  %b | %s",
                     $time, in3, in2, in1, out, expected_out,
                     (out == expected_out) ? "PASS" : "FAIL");
            if (out !== expected_out) begin
                $display("错误: 输入组合 %b%b%b 预期输出 %b, 实际输出 %b",
                         in3, in2, in1, expected_out, out);
            end
        end
        $display("\n测试锁存器行为...");
        in3 = 0; in2 = 0; in1 = 0; 
        #10;
        expected_out = 8'b00000001;
        $display("%4t |  %b   %b   %b  |  %b |  %b | %s",
                 $time, in3, in2, in1, out, expected_out,
                 (out == expected_out) ? "PASS" : "FAIL");
        #20;
        $display("%4t |  %b   %b   %b  |  %b |  %b | %s",
                 $time, in3, in2, in1, out, expected_out,
                 (out == expected_out) ? "PASS" : "FAIL");
        
        $display("\n所有测试完成!");
        $finish;
    end
    initial begin
        $dumpfile("decoder_case_a1_waveform.vcd");
        $dumpvars(0, tb_decoder_case_a1);
    end
endmodule
