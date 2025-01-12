# 实验一
## 与非门
![image](https://github.com/user-attachments/assets/d23cce92-aece-46b0-ae61-cdf90cfb2832)

```
module NANDgate(
        A,
        B,
        Y
    );
input   A;
input   B;
output  Y;
assign  Y=~(A&B);
endmodule
```
测试
```
`timescale 1ns / 1ps

module NANDgate_tb;
reg a;
reg b;
wire y;
NANDgate NANDgate(
            .A(a),
            .B(b),
            .Y(y)
            );
initial begin
            a<=0;b<=0;
        #10 a<=0;b<=1;
        #10 a<=1;b<=0;
        #10 a<=1;b<=1;
        #10 $stop;
end
endmodule

```
仿真结果
![image-3](https://github.com/user-attachments/assets/b2ae600d-7679-42bd-a3c5-6266e198e75e)
![image-4](https://github.com/user-attachments/assets/ad7d4d74-9ee9-44d0-9305-539815f2c522)

## 四-十六译码器
![image-8](https://github.com/user-attachments/assets/d3fcfe8f-66a2-44fe-8cde-6cff1ce1d4ca)
```
module decoder4_16(
                A0,
                A1,
                A2,
                A3,
                Y
    );
input           A0;
input           A1;
input           A2;
input           A3;
output[15:0]    Y;

assign Y[0] = ~(A3 & A2 & A1 & A0);
assign Y[1] = ~(A3 & A2 & A1 & ~A0);
assign Y[2] = ~(A3 & A2 & ~A1 & A0);
assign Y[3] = ~(A3 & A2 & ~A1 & ~A0);
assign Y[4] = ~(A3 & ~A2 & A1 & A0);
assign Y[5] = ~(A3 & ~A2 & A1 & ~A0);
assign Y[6] = ~(A3 & ~A2 & ~A1 & A0);
assign Y[7] = ~(A3 & ~A2 & ~A1 & ~A0);
assign Y[8] = ~(~A3 & A2 & A1 & A0);
assign Y[9] = ~(~A3 & A2 & A1 & ~A0);
assign Y[10] = ~(~A3 & A2 & ~A1 & A0);
assign Y[11] = ~(~A3 & A2 & ~A1 & ~A0);
assign Y[12] = ~(~A3 & ~A2 & A1 & A0);
assign Y[13] = ~(~A3 & ~A2 & A1 & ~A0);
assign Y[14] = ~(~A3 & ~A2 & ~A1 & A0);
assign Y[15] = ~(~A3 & ~A2 & ~A1 & ~A0);

endmodule

```
测试
```
`timescale 1ns / 1ps
module decoder_tb;
reg         a0;
reg         a1;
reg         a2;
reg         a3;
wire[15:0]  y;

decoder4_16 decoder4_16(
                .A0(a0),
                .A1(a1),
                .A2(a2),
                .A3(a3),
                .Y(y)
                );
initial begin
                a0<=0;a1<=0;a2<=0;a3<=0;
        #10     a0<=0;a1<=0;a2<=0;a3<=1;
        #10     a0<=0;a1<=0;a2<=1;a3<=0;
        #10     a0<=0;a1<=0;a2<=1;a3<=1;
        #10     a0<=0;a1<=1;a2<=0;a3<=0;
        #10     a0<=0;a1<=1;a2<=0;a3<=1;
        #10     a0<=0;a1<=1;a2<=1;a3<=0;
        #10     a0<=0;a1<=1;a2<=1;a3<=1;
        #10     a0<=1;a1<=0;a2<=0;a3<=0;
        #10     a0<=1;a1<=0;a2<=0;a3<=1;
        #10     a0<=1;a1<=0;a2<=1;a3<=0;
        #10     a0<=1;a1<=0;a2<=1;a3<=1;
        #10     a0<=1;a1<=1;a2<=0;a3<=0;
        #10     a0<=1;a1<=1;a2<=0;a3<=1;
        #10     a0<=1;a1<=1;a2<=1;a3<=0;
        #10     a0<=1;a1<=1;a2<=1;a3<=1;
        #10     $stop;
end

endmodule

```
仿真结果
![image-6](https://github.com/user-attachments/assets/2dde602a-d725-4d88-90a4-4069a33755b5)
![image-7](https://github.com/user-attachments/assets/d6891ffe-5f61-4bdc-8a13-dbd8697724b4)
出现错误：有序端口连接不能与命名端口连接混合使用
![image-5](https://github.com/user-attachments/assets/c774652b-5b04-4e51-86ba-9b420e72e03d)
最后一行不能有逗号
