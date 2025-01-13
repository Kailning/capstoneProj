# 实验二
## 全加器
![image](https://github.com/user-attachments/assets/9f5a107a-50a6-4cfb-8b1f-28748c3d8fbf)
```
module fullAdder(
    input [7:0] A,  // 8 位输入 A
    input [7:0] B,  // 8 位输入 B
    input res,      // 复位信号，低电平有效
    input Cin,      // 进位输入
    output Cout,    // 进位输出
    output [7:0] Sum  // 8 位和输出
);

    // 生成 8 位和输出和进位输出
    wire [8:0] Carry;  // 用于存储进位的 9 位向量

    // 初始化进位向量
    assign Carry[0] = Cin;

    // 生成每个位的和和进位
    genvar i;
    generate
        for (i = 0; i < 8; i = i + 1) begin : full_adder_loop// label
            // 生成每个位的和
            assign Sum[i] = (A[i] ^ B[i] ^ Carry[i]) & ~res;
            // 生成每个位的进位
            assign Carry[i + 1] = ((A[i] & B[i]) | (A[i] & Carry[i]) | (B[i] & Carry[i])) & ~res;
        end
    endgenerate

    // 最终的进位输出
    assign Cout = Carry[8] & ~res;

endmodule
```
测试：
```
module fullAdder_tb;
// 输入信号
reg [7:0] A;
reg [7:0] B;
reg Cin;
reg res;
// 输出信号
wire [7:0] Sum;
wire Cout;
fullAdder fullAdder(
        .A(A),
        .B(B),
        .res(res),
        .Cin(Cin),
        .Cout(Cout),
        .Sum(Sum)
    );
// 生成测试输入信号
initial begin
            A = 8'b00000000;B = 8'b00000001;Cin = 0;res = 1;// 初始化复位信号为高电平
    #10     A = 8'b00001111;B = 8'b00001111;Cin = 0;res = 1;// 测试 1: 无进位，无复位
    #10     A = 8'b11110000;B = 8'b00001111;Cin = 1;res = 1;// 测试 2: 有进位，无复位
    #10     A = 8'b11111111;B = 8'b11111111;Cin = 1;res = 0;// 测试 3: 复位
    #10     $stop;
end
endmodule
```

仿真结果：
![image](https://github.com/user-attachments/assets/d3a4e6cf-3a04-4736-9825-0b81a72a8d56)

![image](https://github.com/user-attachments/assets/b0a4f53b-42b1-4c1d-8b2e-c1025673ca3b)
