---
title: 如何在免費主機上架設私人VPN?
date: 2022-06-14 23:34:26
tags: tech
---
# 前言
其實一開始是為了要看國外的netflix，(我超想看The Office)，不過做完了之後結果被Netflix擋下來，要知道netflix有很多防範VPN的措施，而我不想要花錢買sharkvpn之類的東西，而且自己做一個比較好玩，雖然netflix不能用，不過其他大部分的國外網站還是能用，所以大家還是可以動手做做看，而且還是免費的~
![](math.jpg)

---
<h2><font size="5" color=#58a548>申請Amazon AWS帳號</font></h2>
進入Amazon AWS註冊頁面並填入email等資料，之後會要求你輸入信用卡資料，因為AWS服務並非所有都是免費的，但基本上不用太擔心會被亂收錢。

![](register.png)

<h2><font size="5" color=#58a548>啟用虛擬主機服務</font></h2>
在控制台點擊EC2，進入之後在左側選單，點擊"執行個體"，然後在右上角點擊"啟動新執行個體"。

![](EC2.png)

名稱就隨便取，映像檔就選ubuntu 20.04。

![](ubuntu_image.png)

執行個體選t2.mirco，因為這個是免費方案裡面最好的，但也足以應付vpn。

![](t2micro.png)

再來就是選金鑰對，aws比較注重安全性所以只能用他給你的私鑰登入主機，不過有點麻煩就是了。金鑰對類型選RSA，私有金鑰檔案格式選.ppk。這時會下載一個檔案，請把它存好。

![](key_generate.png)

最後在網路設定加入新規則，類型選UDP，來源類型選隨處。

![](rules.png)

到這裡，虛擬主機的設定就完成了，點選啟動執行個體。

<h2><font size="5" color=#58a548>進入虛擬主機</font></h2>

請先下載putty，putty是一款強大的軟體，若是要用私鑰登入，putty非常適合。
[下載處](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)

安裝後，先回到AWS的頁面查看剛剛所創建的虛擬主機IP地址複製起來並貼到putty的ip位置欄。

![](ipv4.png)

點開putty左側選單的SSH再點選AUTH，點開private key的按鈕並開啟剛剛獲得的.ppk檔。

此時會出現一個終端機，請以ubuntu為名稱登入。

恭喜你成功進入你的主機!但不覺得如果每次登入都要有私鑰會非常麻煩嗎?因此我們可以修改root密碼。

輸入``` sudo passwd root ```。
輸入你要的密碼之後就可以以root身分登入了。
輸入``` su - ```。之後輸入剛剛設定的密碼就可以以root身分登入了。

由於主機中的套件不一定是最新的，因此我們要先更新。輸入```sudo apt-get update && sudo apt-get upgrade```。

之後載入vpn腳本。
輸入 ```curl -O https://raw.githubusercontent.com/angristan/openvpn-install/master/openvpn-install.sh```。
輸入```chmod +x openvpn-install.sh```。
輸入```./openvpn-install.sh```。
之後會出現一連串的configuration，基本上照預設的就ok了，就一直enter直到出現client name。
client name 輸入你想取的名稱就可以了。
這時輸入ls若有出現 使用者名稱.ovpn 
輸入```cp owenowenserver.ovpn /home/ubuntu```。
最後，開啟任意ftp軟體把ovpn檔存到自己的電腦，下載open vpn connect 並把ovpn檔導入就可以使用了!
![](vpn.png)

不過亞馬遜有每月100gb的限制小心不要超過，不然會被收費。