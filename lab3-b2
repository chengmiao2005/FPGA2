module decoder_case_b2(
    input [2:0] addr,
    output reg [7:0] out
);
    always @* begin
        case (addr)
            3'b000: out = 8'b00000001;
            3'b001: out = 8'b00000010;
            3'b010: out = 8'b00000100;
            3'b011: out = 8'b00001000;
            3'b100: out = 8'b00010000;
            3'b101: out = 8'b00100000;
            3'b110: out = 8'b01000000;
            3'b111: out = 8'b10000000;
            default: out = 8'b00000000; 
        endcase
    end
endmodule




module tb_decoder_case_b2();
    reg [2:0] addr;         
    wire [7:0] out;         
    reg [7:0] expected_out; 
    integer i;              
    decoder_case_b2 uut (
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
        $display("===== 开始测试 decoder_case_b2 3-8译码器 =====");
        $display("(模块特性: 完整覆盖所有8种地址，包含default分支)");
        $display("时间 | 地址(addr) | 实际输出(out) | 预期输出 | 测试结果");
        $display("--------------------------------------------------");
        for (i = 0; i < 8; i = i + 1) begin
            addr = i[2:0];  
            expected_out = 8'b00000001 << i;
            
            #10;  
            print_test_result();
        end
        $display("\n===== 测试default分支行为 =====");
        addr = 3'b111 + 1'b1;  
        expected_out = 8'b00000001;  
        #10;
        print_test_result();
        $display("\n===== 随机地址序列测试 =====");
        repeat (5) begin
            addr = $urandom_range(0, 7);  
            expected_out = 8'b00000001 << addr;  
            
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
        $dumpfile("decoder_case_b2_waveform.vcd");
        $dumpvars(0, tb_decoder_case_b2);  
    end
endmodule
