# BuildYourOwnConferenceSystem
這個計畫目的在於提供「快速架站懶人包」，協助您快速架構自己專屬、免費、安全、易用的視訊會議系統。

# 動機
2020全世界面臨武漢肺炎(新型冠狀病毒, COVID-19)威脅，使用視訊會議可以兼顧團隊工作效率、減少感染風險，可惜目前常見的視訊軟體有[資安隱憂](https://3c.ltn.com.tw/news/40047 "自由時報")，或者需要專門人員操作管理帳號，或者需要額外收取費用，反而讓視訊會議操作不易，難以普及。<br>
我們依照台灣機關學校視訊會議使用情境重新撰寫視訊系統，以[教育部](https://depart.moe.edu.tw/ED2700/News_Content.aspx?n=727087A8A1328DEE&s=868B3A6EDF9BA52D)、[唐鳳](https://3c.ltn.com.tw/news/40055)w推薦使用的開源軟體[Jitsi meet](https://https://meet.jit.si/)為基礎，重新設計一套最適合台灣視訊會議的視訊平台。<br>
### 學校機關系統管理者 
您僅需要照著網頁操作，就可以替單位架設一套免費、安全隱密的會議系統
### 使用者
https://jitsiym.aigia.ai/meet_ym.html

# 系統操作畫面
docs/images/thesystem_architecture.png

將提供step-by-step逐步指引
只要跟著我們開發「陽明大學視訊系統」流程為藍本，再簡單修改即可輕鬆架設一套以Jitsi meet為基礎，開源安全的視訊系統。

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
