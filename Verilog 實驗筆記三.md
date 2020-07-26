###### tags: `Verilog 實驗筆記`
# Verilog 實驗筆記(第三堂課 RCA & Timing Simulation)

# 複習第一節課的部分
## Verilog初學者最常見的問題：『什麼時候該用wire?什麼時候又該用reg?』

### 大體上來說，wire和reg都類似於C/C++的變數，但若此變數要放在begin...end內，該變數就須使用reg，在begin...end之外，則使用wire。

另外使用wire時，須搭配assign；reg則不必。

input，ouput，inout預設值都是wire。

若wire和reg用錯地方，compiler都會提醒，所以不必太擔心。

一個很重要的觀念，在Verilog中使用reg，並不表示合成後就是暫存器(register)。若在組合電路中使用reg，合成後仍只是net，唯有在循序電路中使用reg，合成後才會以flip-flop形式表示成register。

參考資料：[(原創) wire與reg的差異? (初級) (IC Design) (Verilog)](https://www.cnblogs.com/oomusou/archive/2007/10/10/919339.html)

# 組成電腦的基礎元件 -- 邏輯閘
## 基本邏輯閘 (Logic Gate)
![](https://i.imgur.com/mY2V89R.png)
![](https://i.imgur.com/RFaqT8w.png)
![](https://i.imgur.com/XCsBnfm.png)
![](https://i.imgur.com/z4CBMfO.png)

### 使用 and、or、not 做出 xor閘
![](https://i.imgur.com/9X5PwSv.png)

Structural modeling 設計：
```
module xorgate(a, b, cout);
    input a, b;
    output cout;
    wire x, y;
    
    andgate and1(a, ~b, x);
    andgate and2(~a, b, x);
    orgate or1(x, y, cout);
endmodule
```

# 半加器、全加器
將兩個輸入相加的電路，稱為「半加器」(half adder)，而將三個輸入相加的電路，則稱為「全加器」(full adder)。

if( 半加器 = a )
    全加器 = 2a;
多個全加器 = 波紋進位加法器( Ripple carry adder )

## 半加器
![](https://i.imgur.com/XKFoCyZ.png)
![](https://i.imgur.com/9DsQEXO.png)
上述的輸出 S 只有在 A , B 兩者不同的時候才會是 1，這完全符合 XOR 電路的行為模式，因此我們可以用一個 XOR 電路輕易地完成 S 的輸出動作。

而 C 則是在 A, B 兩者均為 1 的情況下才會是 1，否則就會是 0。這與 AND 閘的真值表完全一致，因此我們只要用一個 AND 閘就可以做到 C 的功能了。

但是、雖然我們想做的事情是兩組二進位數字的加法，但是由於相加之後可能會產生進位，因此必須要考慮到三個位元相加的情況，這時就需要將半加器進一步擴充為全加器，以便進行三位元相加的運算。

以下是全加器的電路圖與真值表，其中的輸出 S 只要用兩個 XOR 閘就能做到，因為 S 只有在奇數個 1 的時候才會輸出 1，偶數個 1 的時候就會輸出 0，這種組合完全符合 n 輸入的 XOR 閘之行為。

## 全加器
![](https://i.imgur.com/GvVDqdq.png)
## 波紋進位加法器
RCA 的架構是由許多個全加器 (FA) 所連續組合而成，因為其中任一全加器都必須要等待前一全加器的進位傳入後才會開始進行運算，故此種硬體架構有如漣波 (ripple) 般持續傳遞的特性

![](https://i.imgur.com/H0oPQeO.png)

    