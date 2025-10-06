module decoder_case_b1(
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
        endcase
    end
endmodule



module tb_decoder_case_b1();
    reg [2:0] addr;         
    wire [7:0] out;         
    reg [7:0] expected_out; 
    integer i;              
    reg [7:0] prev_out;     
    decoder_case_b1 uut (
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
        
        $display("===== 开始测试 decoder_case_b1（含锁存行为） =====");
        $display("时间 | 地址(addr) | 实际输出(out) | 预期输出 | 结果");
        $display("--------------------------------------------------");
        addr = 3'b000;
        expected_out = 8'b00000001;
        #10;
        prev_out = out;
        print_test_result();
        for (i = 1; i < 8; i = i + 1) begin
            addr = i[2:0];
            case (addr)
                3'b001: expected_out = 8'b00000010;
                3'b010: expected_out = 8'b00000100;
                3'b011: expected_out = 8'b00001000;
                3'b100: expected_out = 8'b00010000;
                3'b101: expected_out = 8'b00100000;
                3'b110, 3'b111: expected_out = prev_out; 
                default: expected_out = 8'bx; 
            endcase
            
            #10; 
            print_test_result();
            if (addr < 3'b110) begin
                prev_out = out;
            end
        end
        $display("\n===== 锁存行为专项测试 =====");
        addr = 3'b101; 
        #10;
        prev_out = out;
        print_test_result();
        
        addr = 3'b110; 
        expected_out = prev_out;
        #10;
        print_test_result();
        
        addr = 3'b111; 
        expected_out = prev_out;
        #10;
        print_test_result();
        
        addr = 3'b010; 
        expected_out = 8'b00000100;
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
                $error("错误: 地址%3b 预期%8b，实际%8b", addr, expected_out, out);
            end
        end
    endtask
    initial begin
        $dumpfile("decoder_case_b1_waveform.vcd");
        $dumpvars(0, tb_decoder_case_b1);
    end
endmodule
