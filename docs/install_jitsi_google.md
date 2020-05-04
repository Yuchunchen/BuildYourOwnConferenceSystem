# 如何將 Jitsi meet 安裝於 Google 雲端

- [如何將 Jitsi meet 安裝於 Google 雲端](#如何將-Jitsi-meet-安裝於-Google-雲端)
    - [1. Google 帳號](#step1-Google-帳號)
    - [2. 建立Google雲端虛擬主機](#step2-建立Google雲端虛擬主機)
    - [3. 建立主機的網域名稱](#step3-建立主機的網域名稱domain-name)
    - [4. 安裝 Jitsi meet 前置準備](#step4-安裝-Jitsi-meet-前置準備) 
    - [5. 安裝 Jitsi meet ](#step5-安裝-Jitsi-meet)
    - [6. 重要系統設定檔案](#step6.-重要系統設定檔案)

---

## step1. Google 帳號 
Jitsi meet對於硬體沒有特別要求，目前Google提供12個月[免費使用](https://cloud.google.com/free/?hl=zh-TW)，再加上額外美金300元試用金額，應該足以免費使用1年，是很好的開始。

## step2. 建立Google雲端虛擬主機
只需要6分鐘，就可以建立您的雲端虛擬主機。請跟著下面的影片操作，我們在Google雲端建立一台虛擬主機，所需費用正好在Google免費額度內，很適合預算有限的中小型機關學校。<br>

<a href="http://www.youtube.com/watch?feature=player_embedded&v=AE1kr1gs9OQ
" target="_blank"><img src="http://img.youtube.com/vi/AE1kr1gs9OQ/0.jpg" 
alt="Azure VM" width=80% border="10" /></a>

底下是過程中會需要用到的參數如下：

|參數名稱|設定值|說明|
|-------|-----|---|
|專案名稱|jitsi-demo||
|電腦名稱|my-jitsi-demo||
|位置|台灣|放在台灣反應速度最佳|
|開機磁碟|Ubuntu 18.04 LTS|作業系統|
|保留靜態位址:名稱| ip-my-jitsi-demo || 
|保留靜態位址:**外部位址**|xxx.xxx.xxx.xxx|您會獲得一組固定IP(影片中範例為:104.199.168.254)，請記下來|
|建立防火牆規則:名稱| port-jitsi||
|建立防火牆規則:來源IP範圍| 0.0.0.0/0 |不設限，您可以視需要設定|
|建立防火牆規則:指定的通訊協定和通訊埠|80,443,4443,5222,5347,10000-20000|tcp, udp都開啟以加快連線速度|

跟隨著影片步驟，您的主機應該看起來像下圖:
![虛擬主機](https://github.com/Yuchunchen/BuildYourOwnConferenceSystem/blob/master/docs/images/install_jitsi_google0020.png)

請記下下列資訊，

|參數名稱|設定值|說明|
|-------|-----|---|
|外部IP位址  |(影片中範例為:104.199.168.254)||


## step3. 建立主機的網域名稱domain name
您一定要設定網域名稱才能安裝jitsi系統。原因是jitsi meet會使用大量內部伺服器，數字型態IP位址無法使用。您必須跟學校/機關網路管理員申請，網路上有些免費網域服務伺服器可能可以試試看，有些學校有向Google購買G-suite服務，可能可以直接使用[G-suite名稱伺服器](https://support.google.com/a/answer/53929?hl=zh-Hant)，或者您可以花一點錢(每年約新台幣300-2000元)直接向Google[購買一個專屬您的網域名稱](https://www.wfublog.com/2019/04/google-domains-tw-purchase-transfer-godaddy-dns.html)，其他如[GoDaddy](https://tw.godaddy.com/domains/domain-name-search)、[Gandi](https://www.gandi.net/zh-Hant)..等都有提供便宜而且親善的中文介面。

無論您使用哪一家的網域名稱，重點在於您必須增加一筆 A紀錄 (A record)，A記錄又稱為「地址記錄」(或主機記錄)，可將網域連結至代管網域服務的主機實體 IP 位址。下面是我們使用網域伺服器使用畫面：

![DNS網域名稱設定](https://github.com/Yuchunchen/BuildYourOwnConferenceSystem/blob/master/docs/images/install_jitsi_dns_example.png)

**!! 注意 !!** 一般網域名稱設定後，大約需要幾個小時才會生效，請您務必利用確認您的網域名稱生效後，才能繼續安裝。  
您可以使用下列指令來確認網域名稱是否生效：  
###### Windows  
```nslookup 您的網域名稱```  (這裡以 sts.contoso.com 為例，截圖自微軟網頁)  
![Windows](https://github.com/Yuchunchen/BuildYourOwnConferenceSystem/blob/master/docs/images/install_jitsi_nslookup.png)

###### Mac, Linux  
```dig 您的網域名稱```  (這裡以陽明大學視訊系統 jitsiym.aigia.ai 為例)  
![Mac](https://github.com/Yuchunchen/BuildYourOwnConferenceSystem/blob/master/docs/images/install_jitsi_dig.png)



## step4 安裝 Jitsi meet 前置準備
1. Google雲端很貼心，不需要另外設定，您可以點擊畫面的SSH直接登入主機：   
![登入](https://github.com/Yuchunchen/BuildYourOwnConferenceSystem/blob/master/docs/images/install_jitsi_google0020.png)

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

## step5. 安裝 Jitsi meet 

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
|7.|Do you want to translate 'Participant' to your own language? Leave empty to use the default one (English):|請將'Participant' 翻譯成您的語言|Participant|不翻譯|
|8.|Do you want to translate 'me' to your own language?|將 me 翻譯成您的語言|me|不翻譯|
|9.|Do you want to disable the Welcome page: (yes or no)|是否關閉系統預設之首頁?|yes|我們將使用客製化首頁|
|10.|Do you want to enable static avatar?: (yes or no)|是否使用固定大頭貼?|yes|可自行選擇|
|11.|Do you want to enable local audio recording option?: (yes or no)|是否開放與會者自行側錄？|no|不允許側錄會議|
|12.|Do you want to enable secure rooms?: (yes or no)|是否開啟會議室帳號密碼管控？|yes||
|13.|Set username for secure room moderator:|設定管理者帳號|ymteacher|請自行設定|
|14.|Secure room moderator password:|管理者密碼|ym1234|請自行設定|
|15.|Do you want to setup Jibri Records Access via Nextcloud: (yes or no)|是否開放雲端側錄?|no|不允許側錄會議|
|16.|Do you want to setup Jigasi Transcription: (yes or no)|是否開啟自動語音辨識功能?|no|需要額外付費|

4. 再等待一下，系統將會自動重新啟動

5. 試試看使用Chrome 瀏覽器 瀏覽看看唷！


## step6. 重要系統設定檔案

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
|JIBRI錄影檔   |   /var/jbrecord |||
|JIBRI錄影上傳  |  /home/jibri/finalize_recording.sh |||
