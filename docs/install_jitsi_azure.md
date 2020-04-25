# 如何將 Jitsi meet 安裝於 Azure 雲端

## 1. Azure 帳號 
Jitsi meet對於硬體沒有特別要求，目前Azure提供12個月[免費使用](https://azure.microsoft.com/zh-tw/free/)，再加上額外新台幣6100元試用金額，應該足以免費使用1年，是很好的開始。

## 2. 建立雲端虛擬主機
底下的影片我們將在Azure雲端建立一台虛擬主機(名稱為: myjitsidemo)，所需費用正好在Azure免費額度內，很適合預算有限的中小型機關學校。<br>

<a href="http://www.youtube.com/watch?feature=player_embedded&v=--0RYO_zlOo
" target="_blank"><img src="http://img.youtube.com/vi/--0RYO_zlOo/2.jpg" 
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
* 更新 apt
```bash
sudo apt update && 
sudo apt upgrade && 
sudo apt-get update && 
sudo apt-get install sshfs
```
   * 安裝 nano
```bash
sudo apt-get install nano
```
   * 下載安裝標準 linux 核心: 下載  linux image
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
      `GRUB_DEFAULT='1>2'`
   * 重新開機
```bash
sudo reboot now
```

## 4. 安裝 Jitsi meet 

1. 下載 Jitsi 安裝程式
雖然官方網站已提供安裝說明，但是仍有許多地方需要手工設定，經過測試，[SwITNet](https://github.com/switnet-ltd/quick-jibri-installer)所提供的快速安裝程序，可以省下不少設定帶來的挫折。
```bash
wget https://raw.githubusercontent.com/switnet-ltd/quick-jibri-installer/master/jigasi.sh &&
wget https://raw.githubusercontent.com/switnet-ltd/quick-jibri-installer/master/jitsi-updater.sh &&
wget https://raw.githubusercontent.com/switnet-ltd/quick-jibri-installer/master/jm-bm.sh &&
wget https://raw.githubusercontent.com/switnet-ltd/quick-jibri-installer/master/jra_nextcloud.sh &&
wget https://raw.githubusercontent.com/switnet-ltd/quick-jibri-installer/master/quick_jibri_installer.sh &&
chmod +x  jigasi.sh &&
chmod +x jitsi-updater.sh &&
chmod +x jm-bm.sh &&
chmod +x jra_nextcloud.sh &&
chmod +x quick_jibri_installer.sh 
```

2. 執行 quick_jibri_installer.sh
```bash
sudo ./quick_jibri_installer.sh
```

3. 經過一小段時間下載更新後，接著我們要進行基本設定:

|   |提示|說明|建議回答|備註|
|---|---|---|-------|---|
|1.|Please set your language (Press enter to default to 'en')|選擇預設語系|zhTW|選擇中文，注意大小寫需一致)|
|2.|Set sysadmin email|管理者電子郵件||此為必須欄位|
|3.|Do you want to drop support for unsecure protocols TLSv1.0/1.1 now: (yes or no)|是否要停止支援不安全的http協定?|yes|我們希望系統僅能透過https加密連線|
|4.|Do you want to setup LetsEncrypt with your domain: (yes or no)|是否需要SSL加密？|yes||
|5.|Do you want to setup the Dropbox feature now: (yes or no)|是否需要「錄影上傳dropbox」功能？|no|防止未經允許側錄會議|
|6.|Do you want to install customized "brandless mode"?: (yes or no)|是否將Jitsi logo刪除？|no|建議保留jitsi logo|
|7.|Do you want to translate 'Participant' to your own language? Leave empty to use the default one (English):|請將'Participant'翻譯成您的語言|Participant|不翻譯|
|8.|Do you want to translate 'me' to your own language?|將 me 翻譯成您的語言|me|不翻譯|
|9.|Do you want to disable the Welcome page: (yes or no)|是否關閉系統預設之首頁?|yes|我們將使用客製化首頁|
|10.|Do you want to enable static avatar?: (yes or no)|是否使用固定大頭貼?|yes|可自行選擇|
|11.|Do you want to enable local audio recording option?: (yes or no)|是否開放與會者自行側錄？|no|不允許側錄會議|
|12.|Do you want to enable secure rooms?: (yes or no)|是否開啟會議室帳號密碼管控？|yes||
|13.|Set username for secure room moderator:|設定管理者帳號|ymteacher|請自行設定|
|14.|Secure room moderator password:|管理者密碼|ym1234|請自行設定|
|15.|Do you want to setup Jibri Records Access via Nextcloud: (yes or no)|是否開放雲端側錄?|no|不允許側錄會議|
|16.|Do you want to setup Jigasi Transcription: (yes or no)|是否開啟自動語音辨識功能?|no|需要額外付費|

4. 再等待一下，系統將會自動重新啟動

5. 試試看使用Chrome 瀏覽器 瀏覽網址 https://myjitsidemo.westus2.cloudapp.azure.com 


## 5. 恭喜 :)
您現在應該已經有專屬於您的視訊平台囉，接著我們將[安裝視訊系統前台](./docs/install_conferencesystem.md)，加上前端介面，讓系統更好用。

## 6. 重要系統設定檔案
Jitsi meet 還有很多神奇功能可以調整唷，底下是一些常用到的檔案位置，您一定要動手試試看!

|              |檔案    |說明|備註|
|--------------|-------|---|---|
|log           |/var/log/jitsi/jvb.log        |||
|log           |/var/log/jitsi/jicofo.log     |||
|log           |/var/log/prosody/prosody.log  |||  
|JITSI設定檔    |/etc/jitsi/meet/myjitsidemo.westus2.cloudapp.azure.com-config.js| ||
|JITSI介面設定檔|/usr/share/jitsi-meet/interface_config.js  | ||
|nginx 設定    |/etc/nginx/sites-available/myjitsidemo.westus2.cloudapp.azure.com.conf||重新啟動sudo systemctl restart nginx.service && sudo nano /etc/jitsi/meet/myjitsidemo.westus2.cloudapp.azure.com-config.js|
| Web Server Entry |/usr/share/jitsi-meet/| Jitsi meet home page|||
| 靜態大頭貼    |/usr/share/jitsi-meet/images/avatar2.png|||
|JIBRI錄影檔   |/var/jbrecord |||
|JIBRI錄影上傳  |/home/jibri/finalize_recording.sh |||
