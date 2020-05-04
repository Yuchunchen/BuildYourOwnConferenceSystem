# 如何安裝視訊系統前台

- [如何安裝視訊系統前台](#如何安裝視訊系統前台)
    - [1. 從 Github 下載前台程式 ](#step1-從-Github-下載前台程式 )
    - [2. 收工了](#step2-收工了)
    - [3. 如何修改](#step3-如何修改)
    - [4. 重要系統設定檔案](#step4-重要系統設定檔案)
    
---


## step1. 從 Github 下載前台程式 
```bash
sudo git clone https://github.com/Yuchunchen/BuildYourOwnConferenceSystem.git ./local2 &&
sudo cp -arv ~/local2/src_meet_ym/*.*    /usr/share/jitsi-meet/ &&
sudo cp -arv ~/local2/src_meet_ym/css    /usr/share/jitsi-meet/ &&
sudo cp -arv ~/local2/src_meet_ym/images /usr/share/jitsi-meet/ &&
sudo cp -arv ~/local2/src_meet_ym/libs   /usr/share/jitsi-meet/ 
```

## step2. 收工了
是的，這樣就完成囉，趕快來看看安裝成果！  
您可以先使用桌機或筆電，
* 如果您安裝於Azure雲端主機，  
  您可以使用瀏覽器移至 https://myjitsidemo.westus2.cloudapp.azure.com/meet_ym.html
* 如果您安裝於Google雲端，自己取了網域名稱(hosthname)，  
  您可以使用瀏覽器移至 https://hostname/meet_ym.html 

您也可以依照網頁說明下載APP，隨時隨地手機開會超方便！

## step3. 如何修改
根據這幾天回報，已經有許多朋友安裝成功，希望能夠更近一步修改為自己單位網頁，當然沒問題。   
您只需要打開 meet_ym.html，您就可以修改網頁文字：  
```bash
sudo nano /usr/share/jitsi-meet/meet_ym.html
```

更進階的修改，可以參考[進階客製化](./install_customization.md)，您也可以參考[「Jitsi 資源大全」](https://github.com/Yuchunchen/awesome-jitsi)並且留下您的使用心得唷！

希望大家使用愉快！

## step4. 重要系統設定檔案
Jitsi meet 還有很多神奇功能可以調整唷，底下是一些常用到的檔案位置，您一定要動手試試看!
依照您安裝的主機名稱(Azure:myjitsidemo.westus2.cloudapp.azure.com) ，檔名會有所不同，請注意替換唷！

|              |檔案    |說明|備註|
|--------------|-------|---|---|
|log           |/var/log/jitsi/jvb.log        |||
|log           |/var/log/jitsi/jicofo.log     |||
|log           |/var/log/prosody/prosody.log  |||  
|JITSI設定檔    |/etc/jitsi/meet/myjitsidemo.westus2.cloudapp.azure.com-config.js|!注意主機名稱||
|JITSI介面設定檔|/usr/share/jitsi-meet/interface_config.js  | ||
|nginx 設定    |/etc/nginx/sites-available/myjitsidemo.westus2.cloudapp.azure.com.conf|!注意主機名稱|重新啟動sudo systemctl restart nginx.service && sudo nano /etc/jitsi/meet/myjitsidemo.westus2.cloudapp.azure.com-config.js|
| Web Server Entry |/usr/share/jitsi-meet/| Jitsi meet home page|||
| 靜態大頭貼    |/usr/share/jitsi-meet/images/avatar2.png|||
|JIBRI錄影檔   |/var/jbrecord |||
|JIBRI錄影上傳  |/home/jibri/finalize_recording.sh |||
