# BuildYourOwnConferenceSystem
這個計畫目的在於協助您快速架構自己專屬、免費、安全的視訊會議系統。<br>
我們依照台灣機關學校視訊會議使用情境重新撰寫視訊系統，

讓學校老師不需要多花心思設定，僅需要照著網頁操作就可以有兼顧安全隱密的會議系統
https://jitsiym.aigia.ai/meet_ym.html


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
