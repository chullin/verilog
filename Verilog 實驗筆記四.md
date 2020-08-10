###### tags: `Verilog 實驗筆記`
# Verilog 實驗筆記(第四堂課 Structural modeling & Carry lookahead adder)

參考資料：
* https://www.youtube.com/watch?v=6Z1WikEWxH0

* https://chi_gitbook.gitbooks.io/personal-note/content/addition.html

* https://www.youtube.com/watch?v=9lyqSVKbyz8
    * 9:55

* https://blog.csdn.net/lanchunhui/article/details/59058047

# Carry lookahead adder (1/2)
Ripple carry adder (RCA) 是一種簡單的加法器，但它必須要等待 carry 傳遞結束才會產生運算結果；而 CLA 是一種進階的架構，它能夠一次產生所需的 carry 並運算出結果，雖然增加電路複雜度卻也減少了 gate delay，因此相較於 RCA 而言是一種較有效率的加法器

## 16-bit RCA
![](https://i.imgur.com/2tYEkLq.png)

## 16-bit CLA
![](https://i.imgur.com/xj31MWQ.png)

# Carry lookahead adder (2/2)
* CLA 可以使用 input a、b 來產生所需的 carry-out
* 當產生的 carry-out 數量增加時會因為逐漸增長的電路而增加極大複雜度，因此通常邏輯閘的輸入 (Fan-in) ≥ 4 

下圖為一個邏輯輸入 fan-in = 3 的閘
![](https://i.imgur.com/rSeT3wF.png)


![](https://i.imgur.com/iTlaLMY.png)

![](https://i.imgur.com/ZR3aKO3.png)

![](https://i.imgur.com/R0J9lqB.png)

# Basic structure : 4-bit CLA (1/5) 
圖為 4-bit CLA 架構，在 Verilog 中可透過將 4-bit CLA module 以 structural modeling 互相連接組合出更高位元的 CLA 架構，4-bit CLA 可由圖中三個部分的 module 連接而成

![](https://i.imgur.com/HYVYa1v.png)

# Basic structure : 4-bit CLA (2/5) 
* 4-bit input a、b 在 gp generator module 中產生 4-bit Generate (gi) & Propagate (pi)
    * Generate :	gi = ai & bi
    * Propagate :	pi = ai | bi
    * 
![](https://i.imgur.com/GM5DDaR.png)

![](https://i.imgur.com/XZtMKh9.png)
# Basic structure : 4-bit CLA (3/5) 
利用上一層產生的 4-bit Generate (gi) & Propagate (pi) 來產生其餘 3-bit carry-out
![](https://i.imgur.com/hUjMkxq.png)

![](https://i.imgur.com/QC6dHU9.png)

# Basic structure : 4-bit CLA (4/5) 
最後將所有 carry-out 和 4-bit input a、b 以 xor 邏輯閘合成以取得運算結果
* 在 verilog 裡面， “^” 符號代表 xor
* 
![](https://i.imgur.com/OdhsrR9.png)

![](https://i.imgur.com/VQ7L5PF.png)

# Basic structure : 4-bit CLA (5/5) 
下表為使用 structural modeling 設計方式將 module 連接完成的 4-bit CLA 架構 

![](https://i.imgur.com/wNNVYjv.png)

# Advanced structure : 16-bit CLA (1/6) 
透過 structural modeling 的設計方式將 4 個 4-bit CLA 內的 module 如樹狀般連接則可以完成 16-bit CLA 的架構
![](https://i.imgur.com/EkmYl94.png)

# Advanced structure : 16-bit CLA (2/6) 
將 16-bit input a、b 平分為 4 x 4-bit input a、b，並各自產生 4-bit g、p 

![](https://i.imgur.com/Wjd1CQ6.png)

# Advanced structure : 16-bit CLA (3/6) 
![](https://i.imgur.com/FmwvX4c.png)

![](https://i.imgur.com/rblTzxj.png)

![](https://i.imgur.com/DCsfrmd.png)

# Advanced structure : 16-bit CLA (4/6) 
![](https://i.imgur.com/fPcdP6R.png)

![](https://i.imgur.com/6GNMrWu.png)

![](https://i.imgur.com/pHNxVvN.png)

![](https://i.imgur.com/UwjsvaK.png)

# Advanced structure : 16-bit CLA (5/6) 
接下來以 cin、c4、c8、c12 合成其餘的所有 carry，最後和 16-bit input a、b 合成運算結果

![](https://i.imgur.com/mr5PVcQ.png)

# Advanced structure : 16-bit CLA (6/6) 
下表為使用 structural modeling 的設計方式將 module 連接完成的 16-bit CLA 架構 

![](https://i.imgur.com/9dY9QXx.png)

![](https://i.imgur.com/snZ7SCQ.png)

# Homework & demo (1/2)
開啟“作業”資料夾，請參考投影片教學內容並以 structural modeling 的方式設計 “16bit_CLA.v”，並以“16bit_testbench.v”驗證 10 道運算的正確性
![](https://i.imgur.com/qrvnTH2.png)

# Homework & demo (2/2)
請以 structural modeling 的方式設計 “64bit_CLA.v”，並以 “64bit_testbench.v”驗證 10 道運算的正確性
![](https://i.imgur.com/ZFSasGU.png)
