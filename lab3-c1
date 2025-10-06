module decoder_case_c1(
    input [2:0] addr,
    output reg [7:0] out
);
    always @* begin
        if (addr == 3'b000) out = 8'b00000001;
        else if (addr == 3'b001) out = 8'b00000010;
        else if (addr == 3'b010) out = 8'b00000100;
        else out = out; 
    end
endmodule




module tb_decoder_case_c1();
    reg [2:0] addr;         
    wire [7:0] out;         
    reg [7:0] expected_out; 
    reg [7:0] prev_out;     
    integer i;              
    decoder_case_c1 uut (
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
        prev_out = 8'b00000000; 

        $display("===== 开始测试 decoder_case_c1 模块 =====");
        $display("(模块特性: 仅定义000/001/010地址，其他情况out=out产生锁存)");
        $display("时间 | 地址(addr) | 实际输出(out) | 预期输出 | 测试结果");
        $display("--------------------------------------------------");
        $display("\n----- 测试已定义地址 -----");
        addr = 3'b000;
        expected_out = 8'b00000001;
        #10;
        prev_out = out;  
        print_test_result();
        addr = 3'b001;
        expected_out = 8'b00000010;
        #10;
        prev_out = out;
        print_test_result();
        addr = 3'b010;
        expected_out = 8'b00000100;
        #10;
        prev_out = out;
        print_test_result();
        $display("\n----- 测试未定义地址的锁存行为 -----");
        for (i = 3; i < 8; i = i + 1) begin  
            addr = i[2:0];
            expected_out = prev_out;  
            
            #10;  
            print_test_result();
        end
        $display("\n----- 验证从锁存状态恢复 -----");
        addr = 3'b011;
        expected_out = prev_out; 
        #10;
        print_test_result();
        addr = 3'b000;
        expected_out = 8'b00000001;
        #10;
        prev_out = out;
        print_test_result();
        addr = 3'b111;
        expected_out = prev_out;
        #10;
        print_test_result();
        
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
        $dumpfile("decoder_case_c1_waveform.vcd");
        $dumpvars(0, tb_decoder_case_c1);  
    end
endmodule
