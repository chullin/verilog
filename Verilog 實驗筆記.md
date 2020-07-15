###### tags: `Verilog 實驗筆記`
# Verilog 實驗筆記(一看就上手)
# 安裝
安裝 Icarus Verilog for Windows，點選下載點
[下載點](http://bleyer.org/icarus/)
![](https://i.imgur.com/iQrZ4bi.jpg)

點選最新版

iverilog-v11-20190809-x64_setup.exe [17.0MB]

下載後會包含一個叫做 gtkwave 的輕量級波形檢視軟體

# 第一支程式 hello.v

打開 Visual Studio Code (或使用任意編譯器寫一段verilog程式碼) 取名做 hello.v


 
```
module tb;

initial begin
    $display("*************************");
    $display("hello world");
    $display("*************************");
end

endmodule
```

# 執行

打開終端機，上面的 hello.v 檔要在安裝好的 verilog 資料夾裡面

在資料夾上面直接輸入 cmd 開啟
![](https://i.imgur.com/cT3WEYU.png)

開啟後輸入
## (這裡為編譯)
`
iverilog -o 編譯後檔名 程式碼名稱
`

`
iverilog -o test hello.v
`

執行後會跑出一個叫做 test 的檔案

而 a.out 則是預設輸出檔名!

![](https://i.imgur.com/HHUCO1k.png)

接著在 cmd 輸入 vvp 編譯後檔案名稱，就會跑出結果

## (這裡為模擬)

`vvp test`

![](https://i.imgur.com/anqi6xB.png)

# 執行學長給的範例檔
下載兩個檔案
1. add2.v
2. testbench_add2.v

此為 add2.v 程式碼
作用為加法器
![](https://i.imgur.com/mCoo3xX.png)

此為 testbench_add2.v 主要程式
![](https://i.imgur.com/bcs0OoD.png)

![](https://i.imgur.com/s2Hoa9d.png)

接著在 cmd 輸入以下指令

編譯後並取名為 test
`iverilog -o test testbench_add2.v`

接著進行模擬編譯好的檔案
`vvp test`

而後會得到一個 fsdb 檔(寫在程式裡)

用 gtkwave 打開
`gtkwave add.fsdb`

![](https://i.imgur.com/wmaB3id.png)
1. 點選 SST 區域中的 testbench_add2
2. 選取變數並點擊 Insert
3. 在 Signals 選取變數，並點擊右鍵選擇 Data Format 選取 Decimal
(為了方便觀察，所以選擇10進位)
4. 點選不知道是什麼的放大鏡開始執行
5. 放大到看到波型變動，確認結果是否正確

# 練習 
![](https://i.imgur.com/VMnAAh6.png)

1. 完成 4bit 4-Operand adder並設計Testbench驗證之，並能夠解釋為什麼此Testbench足以驗證此MPY正確，並能顯示波形圖
2. 完成 4bit MUX並設計Testbench驗證之，並能夠解釋為什麼此Testbench足以驗證此MUX正確，並能顯示波形圖

## Homework (1/2)
![](https://i.imgur.com/KxmGVPW.png)
寫出主要 averilog 檔
![](https://i.imgur.com/fzkmfT8.png)

寫出 testbench 檔
![](https://i.imgur.com/aAYDnyc.png)
![](https://i.imgur.com/n0ygo0C.png)
monitor：層級比運算元後面，執行完程式才印出
display：層級比運算元前面，印出後才執行完程式


編譯並模擬
![](https://i.imgur.com/M4XGT1m.png)

打開 gtkwave 驗證是否正確
![](https://i.imgur.com/5LGQ9FC.png)


## Homework (2/2)
![](https://i.imgur.com/geTX4G5.png)

寫出主要 averilog 檔
![](https://i.imgur.com/79zzwcK.png)

寫出 testbench 檔
![](https://i.imgur.com/QewiZmA.png)
![](https://i.imgur.com/Z8jH6JS.png)

always #20 指的是每經過 20 個 cycles ，就跑一次後面的式子。
clk 變成 -clk

編譯並模擬
![](https://i.imgur.com/M8c8LU6.png)
![](https://i.imgur.com/IzHQdYm.png)

monitor 會一直變換 =a, =b, =a, =b，所以 out = 1, =2, =1, =2

打開 gtkwave 驗證是否正確
![](https://i.imgur.com/SERiq22.png)


# Lexical Convention (1/2)
### Comment
* Single line: //
* Multiple line: /*.. .. .. */

### Operators
#### Arithmetic Description:
* A=B+C;
* A=B-C;
* A=B*C;
* A=B/C;
* A=B%C;

#### Bit-wise Operators:
* A=~B; // INVERT
* A=B&C; // AND
* A=B|C; // OR
* A=B^C; // XOR 

#### Logical Operators:
* A=!B;
* A=B&&C;
* A=B||C;

#### Shift Operator:
* A=B>>2; // shit right „B‟ by 2-bit
* A=B<<2; // shift left „B‟ by 2-bit

# Lexical Convention (2/2)

`exempli gratia 為拉丁文` 
