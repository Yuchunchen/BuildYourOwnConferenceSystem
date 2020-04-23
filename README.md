# BuildYourOwnConferenceSystem
這個計畫目的在於提供「快速架站懶人包」，協助您快速架構自己專屬、免費、安全、易用的視訊會議系統。

# 動機
2020全世界面臨武漢肺炎(新型冠狀病毒, COVID-19)威脅，使用視訊會議可以兼顧團隊工作效率、減少感染風險，可惜目前常見的視訊軟體有[資安隱憂](https://3c.ltn.com.tw/news/40047 "自由時報")，或者需要專門人員操作管理帳號，或者需要額外收取費用，反而影響參與視訊會議的使用體驗。<br>
我們依照台灣機關學校視訊會議使用情境重新撰寫視訊系統，以[教育部](https://depart.moe.edu.tw/ED2700/News_Content.aspx?n=727087A8A1328DEE&s=868B3A6EDF9BA52D)、「台灣天才IT大臣」[唐鳳](https://3c.ltn.com.tw/news/40055)推薦使用的開源軟體[Jitsi meet](https://https://meet.jit.si/)為基礎，重新打造一套快速入手適用於台灣的視訊會議平台。<br>

使用「快速架站懶人包」將有下列好處：
### 學校機關系統管理者 
免費軟體安裝不易，是管理者心中痛點。我們提供本機、雲端(Google cloud 與 Azure)多種安裝方式、您僅需要照著網頁操作，簡單修改原始碼就可以替單位架設一套免費、安全隱密的會議系統，還可以依照您的需求自行延伸加上會議錄影、錄音字幕等等功能。
### 視訊會議使用者
與會者一直遲遲無法加入會議，是視訊會議最常見的痛點，我們將常見的視訊會議流程簡化為4個步驟，會議管理者僅需要照著網頁提示即可開啟會議。視訊會議參與者不需高檔配備，僅需用手機掃條碼便可即時參加會議，讓視訊會議流程最通暢。

# 系統操作畫面
我們將以「陽明大學視訊系統」流程為藍本。
！[](https://github.com/Yuchunchen/BuildYourOwnConferenceSystem/blob/master/docs/images/desktop_screen010.png)

！[](https://github.com/Yuchunchen/BuildYourOwnConferenceSystem/blob/master/docs/images/desktop_screen020.png)

！[](https://github.com/Yuchunchen/BuildYourOwnConferenceSystem/blob/master/docs/images/desktop_screen030.png)

！[](https://github.com/Yuchunchen/BuildYourOwnConferenceSystem/blob/master/docs/images/desktop_screen040.png)

！[](https://github.com/Yuchunchen/BuildYourOwnConferenceSystem/blob/master/docs/images/desktop_screen041.png)

！[](https://github.com/Yuchunchen/BuildYourOwnConferenceSystem/blob/master/docs/images/desktop_screen050.png)

！[](https://github.com/Yuchunchen/BuildYourOwnConferenceSystem/blob/master/docs/images/desktop_screen060.png)


！[](https://github.com/Yuchunchen/BuildYourOwnConferenceSystem/blob/master/docs/images/thesystem_architecture.png.png)



## Requirements
* 您必須有台Ubuntu LTS主機(或者您可以申請Azure或Google雲端帳號，我們也有提供安裝指引可以安裝在 Azure雲端 與 Google雲端，管理更為方便), **必要**
* 您的網域名稱和DNS紀錄(Valid domain with DNS record), **必要**.

## Features
* 客製化流程，針對台灣召開視訊會議場景特別設計，
* Enabled Jitsi Electron app detection server side.
* Standalone SSL Certbot/LE implementation
* Jigasi Transcript - Speech to Text powered by Google API
* (New) JRA (Jibri Recordings Access) via Nextcloud
* (New) Customized brandless mode
* (New) Improved recurring updater

### Jigasi Transcript
* SIP account
* Google Cloud Account with Billing setup.

### Jibri Recodings Access via Nextcloud
* Valid domain with DNS record for Nextcloud SSL.

## Optional custom changes
* Optional default language
* Option to enable Secure Rooms
* Option to enable Welcome Page
* Option to enable Local audio recording using flac.
* Option to use Rodentia static avatar (icon credit: sixsixfive).
