# 如何將 Jitsi meet 安裝於 Azure 雲端

## 1. Azure 帳號 
Jitsi meet對於硬體沒有特別要求，目前Azure提供12個月[免費使用](https://azure.microsoft.com/zh-tw/free/)，再加上額外新台幣6100元試用金額，應該足以免費使用1年，是很好的開始。

## 2. 建立雲端虛擬主機
底下的影片我們將在Azure雲端建立一台虛擬主機(名稱為: myjitsidemo)，所需費用正好在Azure免費額度內，很適合預算有限的中小型機關學校。<br>

<a href="http://www.youtube.com/watch?feature=player_embedded&v=BMuAhTTeUYg
" target="_blank"><img src="http://img.youtube.com/vi/BMuAhTTeUYg/0.jpg" 
alt="Azure VM" width=80% border="10" /></a>

底下是過程中會需要用到的參數如下：

|參數名稱|設定值|說明|
|-------|-----|---|
|資源群組|jitsidemo||
|電腦名稱|myjitsidemo||
|位置|美國西部2|目前這個位置的主機比較便宜|
|登入帳號|jitsiadm||
|登入密碼| .....|請您自行設定一組12位密碼|
|DNS名稱標籤|myjitsidemo||
|目的地連接埠範圍|80,443,4443,5222,5347,10000-20000||

跟隨著影片步驟，您的主機應該看起來像下圖:
![虛擬主機](https://github.com/Yuchunchen/BuildYourOwnConferenceSystem/blob/master/docs/images/install_jitsi_azure_0010.png)

請記下下列資訊，接下來會常常使用到

|參數名稱|設定值|說明|
|-------|-----|---|
|登入帳號|jitsiadm||
|登入密碼| .....|您剛剛自行設定的12位密碼|
|DNS名稱|myjitsidemo.westus2.cloudapp.azure.com|
|SSH登入指令|`ssh jitsiadm@myjitsidemo.westus2.cloudapp.azure.com`|

## 3. 安裝 Jitsi meet 前置準備
1. 您可以由畫面上面的連結(SSH 登入) 或者 左下角(序列主控台登入)
![登入](https://github.com/Yuchunchen/BuildYourOwnConferenceSystem/blob/master/docs/images/install_jitsi_azure_0020.png)

2. 系統更新
   1. 更新 apt
```bash
sudo apt update && 
sudo apt upgrade && 
sudo apt-get update && 
sudo apt-get install sshfs
```

   2. 安裝 nano
```bash
sudo apt-get install nano
```

   3. 下載安裝標準 linux 核心
       * 下載  linux image
```bash
sudo apt-get -y install linux-image-generic &&
sudo update-grub
```

       * 開啟 /etc/default/grub 
```bash
sudo nano /etc/default/grub
```

       * 設定 linux image
      找到**GRUB_DEFAULT**，並修改為如下，Ctrl-X存檔
      GRUB_DEFAULT='1>2'

       * 重新開機
```bash
sudo reboot now
```

