module decoder_case_a2(
    input [2:0] addr,
    output reg [7:0] out
);
    always @* begin
        if (addr == 3'b000) out = 8'b00000001;
        else if (addr == 3'b001) out = 8'b00000010;
        else if (addr == 3'b010) out = 8'b00000100;
        else if (addr == 3'b011) out = 8'b00001000;
        else if (addr == 3'b100) out = 8'b00010000;
        else if (addr == 3'b101) out = 8'b00100000;
        else if (addr == 3'b110) out = 8'b01000000;
        else out = 8'b10000000; 
    end
endmodule




module tb_decoder_case_a2();
    reg [2:0] addr;     
    wire [7:0] out;      
    reg [7:0] expected_out;  
    integer i;          
    decoder_case_a2 uut (
        .addr(addr),
        .out(out)
    );
    reg clk;
    initial begin
        clk = 0;
        forever #10 clk = ~clk;  
    end
    initial begin
        addr = 3'b000;
        $display("开始测试 decoder_case_a2 3-8译码器模块...");
        $display("时间 | 地址(addr) | 实际输出(out) | 预期输出 | 测试结果");
        $display("--------------------------------------------------------");
        for (i = 0; i < 8; i = i + 1) begin
            addr = i[2:0];
            expected_out = 8'b00000001 << i;
            #10;
            $display("%4t |   %3b    |   %8b   |  %8b | %s",
                     $time, addr, out, expected_out,
                     (out == expected_out) ? "PASS" : "FAIL");
            if (out !== expected_out) begin
                $error("测试失败: 地址 %3b 预期输出 %8b, 实际输出 %8b",
                       addr, expected_out, out);
            end
        end
        $display("\n进行随机地址跳转测试...");
        repeat (5) begin
            addr = $urandom_range(0, 7);
            expected_out = 8'b00000001 << addr;
            
            #10;  
            
            $display("%4t |   %3b    |   %8b   |  %8b | %s",
                     $time, addr, out, expected_out,
                     (out == expected_out) ? "PASS" : "FAIL");
        end
        
        $display("\n所有测试完成!");
        $finish;  
    end
    initial begin
        $dumpfile("decoder_case_a2_waveform.vcd");
        $dumpvars(0, tb_decoder_case_a2);  
    end
endmodule


