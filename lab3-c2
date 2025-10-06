module decoder_case_c2(
    input [2:0] addr,
    output reg [7:0] out
);
    always @* begin
        if (addr == 3'b000) out = 8'b00000001;
        else if (addr == 3'b001) out = 8'b00000010;
        else if (addr == 3'b010) out = 8'b00000100;
        else out = 8'b00000000; 
    end
endmodule




module tb_decoder_case_c2();
    reg [2:0] addr;         
    wire [7:0] out;         
    reg [7:0] expected_out; 
    integer i;              
    decoder_case_c2 uut (
        .addr(addr),
        .out(out)
    );
    reg clk;
    initial begin
        clk = 1'b0;
        forever #10 clk = ~clk; 
    end
    initial begin
        addr = 3'b000;
        $display("===== 开始测试 decoder_case_c2 模块 =====");
        $display("(模块特性: 定义000/001/010地址，其他情况显式输出00000000)");
        $display("时间 | 地址(addr) | 实际输出(out) | 预期输出 | 测试结果");
        $display("--------------------------------------------------");
        $display("\n----- 测试已定义地址 -----");
        addr = 3'b000;
        expected_out = 8'b00000001;
        #10;
        print_test_result();
        addr = 3'b001;
        expected_out = 8'b00000010;
        #10;
        print_test_result();
        addr = 3'b010;
        expected_out = 8'b00000100;
        #10;
        print_test_result();
        $display("\n----- 测试未定义地址的默认输出 -----");
        for (i = 3; i < 8; i = i + 1) begin  
            addr = i[2:0];
            expected_out = 8'b00000000;  
            
            #10;  // 等待稳定
            print_test_result();
        end
        $display("\n----- 随机地址序列测试 -----");
        repeat (6) begin
            addr = $urandom_range(0, 7);  
            if (addr == 3'b000) expected_out = 8'b00000001;
            else if (addr == 3'b001) expected_out = 8'b00000010;
            else if (addr == 3'b010) expected_out = 8'b00000100;
            else expected_out = 8'b00000000;
            
            #10; 
            print_test_result();
        end
        
        $display("\n===== 所有测试完成 =====");
        $finish;  
    end
    task print_test_result;
        begin
            $display("%4t |   %3b    |   %8b   |  %8b | %s",
                     $time, addr, out, expected_out,
                     (out == expected_out) ? "PASS" : "FAIL");
            if (out !== expected_out) begin
                $error("错误: 地址%3b 预期输出%8b, 实际输出%8b",
                       addr, expected_out, out);
            end
        end
    endtask
    initial begin
        $dumpfile("decoder_case_c2_waveform.vcd");
        $dumpvars(0, tb_decoder_case_c2);  
    end
endmodule
