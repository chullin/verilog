###### tags: `Verilog 實驗筆記`
# Verilog 實驗筆記(第二堂課 Nexys4 & vivado)

# 工具 Nexys4
![](https://i.imgur.com/Dv1nprW.png)
![](https://i.imgur.com/PA6caIh.png)


* Nexys4上的FPGA可以用RTL來描述其電路行為
* Nexys4上有現成的電路像是LED、switch、七段顯示器等開發板周邊，可用作FPGA的輸入以及輸出

## FPGA
#### 場域可程式化邏輯閘陣列 (Field Programmable Gate Array) 
目前以硬體描述語言（Verilog或VHDL）描述的邏輯電路，可以利用邏輯合成和布局、布線工具軟體，快速地燒錄至FPGA上進行測試，這一過程是現代積體電路設計驗證的技術主流。


# 課程實驗一
* 使用16顆 switches (sw0~sw15)分別控制16顆LED (led0~led15)的明滅
![](https://i.imgur.com/q0e85ur.jpg)
開關為輸入，LED燈為輸出，由右至左分別是 sw0 到 sw15，開關往上撥為打開

## xdc檔設定
* Xilinx Design Constraints file(xdc file) 
    * Nexys4上的周邊元件設定檔
    * 依據開發板上要用的元件PIN腳名稱去設定
![](https://i.imgur.com/dVBHhZn.png)
![](https://i.imgur.com/obGECDZ.png)

## .v檔
編寫
![](https://i.imgur.com/3KHWYDb.png)


## Vivado建立專案(1/4)
開啟Vivado > Create Project > Next > 輸入專案名稱 > Next
![](https://i.imgur.com/MKcZZ0b.png)
![](https://i.imgur.com/5g7X1XW.png)
![](https://i.imgur.com/UAXZh4L.png)

## Vivado建立專案(2/4)
選擇RTL Project > Next > Next
![](https://i.imgur.com/9Xbic5h.png)
![](https://i.imgur.com/QMwreJy.png)

## Vivado建立專案(3/4)
Next > Family:Artix-7 > Package:csg324 > Speed grade:-3 > xc7a100tcsg324-3

![](https://i.imgur.com/mh8q0FY.png)
![](https://i.imgur.com/JNOk5jO.png)

## Vivado建立專案(4/4)
![](https://i.imgur.com/8qtfnvR.png)

## Vivado創建專案原始檔(1/3)
* 按加號新增檔案
* 選擇檔案類型 > Add or create constraints
    * constraints :新增.xdc檔
        * .xdc用來描述.v與實體線路的連接關係
    * design sources :新增.v檔
        * .v用來描述硬體行為 

![](https://i.imgur.com/8lqnMAf.png)
![](https://i.imgur.com/SEuQAJc.png)

## Vivado創建專案原始檔(2/3)
* 匯入.xdc檔
    * Add or create constraints > Next > Add files > 選擇下載的.xdc檔 > Finish

![](https://i.imgur.com/NjQ6raV.png)

## Vivado創建專案原始檔(3/3)
* 匯入top.v檔
    * Add or create design sources > Next > add file > 選擇.v檔 > Finish

## 燒錄至 FPGA (1/2)
* 專案完成後要將電路燒錄至FPGA上
    * 左方欄位選擇Generate Bitstream > OK > 等待右上角跳出成功訊息
![](https://i.imgur.com/37LtXpg.png)

## 燒錄至FPGA(2/2)
* Open Target > Auto Connect > Program Device > Program
燒錄完即可確認是否成功
![](https://i.imgur.com/BBOm2Ah.png)
![](https://i.imgur.com/61iBJVx.png)
![](https://i.imgur.com/xWSNSm8.png)

# 作業一
* 將Lab1作業四個4-bits的加法器在FPGA上實作，使用Nexys4開發板上從右到左每四個switches當作一個input，相加結果以6-bits來表示顯示在LED上。
![](https://i.imgur.com/5uSMyWp.jpg)

# 7-seg display 七段顯示器

## 七段顯示器原理與架構 (1/2)
![](https://i.imgur.com/p9dbACH.png)

* 什麼是七段顯示器
    *  七段顯示器(seven-segment display)為一用來 顯示數字的電子元件
    * 藉由七個發光二極體(LED)以不同組合來顯  示數字 (若有小數點位則八個)
    * 分為共陽極及共陰極兩種
## 七段顯示器原理與架構 (2/2)
![](https://i.imgur.com/neysU2d.png)

* 共陽極與共陰極的差別
    * 共陽極與共陰極指的是七段顯示器內的一端提供相同的電位
    * 因此共陽極透過改變陰極電位來控制七段顯示器顯示
    * 而共陰極透過改變陽極電位來控制七段顯示器顯示

### E.g:Nexys-4內的七段顯示器為共陽極，透過輸入控制訊號，告訴FPGA版LED陰極是否要接地來控制LED顯示(若訊號為0則接地，LED亮起)

## Practice Questions 1
### 已知Nexys-4使用的七段顯示器為共陽極，且透過七位元訊號控制LED，則若要顯示數字4則需要輸入什麼訊號?
#### ABCDEFG等七個LED的控制訊號分別放在七位元訊號的第0到6位，且訊號1代表高電位，訊號0代表低電位(接地)

#### 解答：0011001


## 多個七段顯示器控制(1/2)
為了減少硬體的複雜度，通常會將多個七段顯示器相同名稱的接腳連接在一起，並且每一個七段顯示器有獨立的驅動腳(如右圖)，各自接收訊號決定七段顯示器是否顯示。

![](https://i.imgur.com/ab2jURi.png)

## Practice Questions 2
### 已知Nexys-4使用的七段顯示器為共陽極，且透過七位元訊號控制LED，並另外透過八位元訊號控制驅動腳，則若要使第3位的七段顯示器顯示數字5則需要輸入什麼訊號?

#### CA、CB……CG等七個LED的控制訊號分別放在七位元訊號的第0到6位，且訊號1代表高電位，訊號0代表低電位(接地)。

#### AN7、AN6……AN0等八個驅動腳的控制訊號由右至左放在八位元訊號的第0到第7位，且訊號1代表七段顯示器不顯示，0則代表該七段顯示器顯示。

#### 解答：0010010,11011111

## 多個七段顯示器控制(2/2)
* 前述架構的七段顯示器無法在不同顯示器上同時顯示不同值，為了看起來像是多個七段顯示器顯示不同值，我們需以人眼無法察覺的速度去掃描多個七段顯示器。

* 人類的視覺暫留平均時間為1/16秒，因此每個七段顯示器的顯示時間必須小於1/(16 * N)秒，其中N為七段顯示器的位數。

* 但若七段顯示器的掃描時間太短，則通過的電流會過小導致顯示器過暗甚至不亮。
![](https://i.imgur.com/h8HZWIU.png)

# 教材說明(1/3)
## Xilinx Design Constraints file(xdc file) 
* T10、R10……L18為LED控制PIN腳
* J17、J18…….U13為七段顯示器驅動腳
![](https://i.imgur.com/UHoxjRh.png)

# 教材說明(2/3)
* 先定義輸入輸出與宣告，輸入為clk和Switch元件訊號，輸出為驅動腳控制訊號及LED控制訊號。
    * clk為時脈訊號，在同步電路中扮演計時器的角色。

* 將sw[11:6]與sw[5:0]分別放在不同的wire，表示兩筆不同的數字。
![](https://i.imgur.com/IsZGGk8.png)

![](https://i.imgur.com/nRN8M7f.png)

# 教材說明(3/3)
![](https://i.imgur.com/HX6PFKE.png)

![](https://i.imgur.com/SZDgxgm.png)

# 作業二
* 用 12 顆 switches (sw0~sw11) 分別控制兩筆輸入，將兩筆輸入相加結果顯示在最右邊兩個七段顯示器，並在最左邊兩個七段顯示器顯示對應的鏡像(如下圖)
![](https://i.imgur.com/wH3rm5K.jpg)
### 提示
在作業裡將 case 值直接+10，指定每隻 pin 角是否亮燈