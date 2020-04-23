# BuildYourOwnConferenceSystem
這個計畫目的在於提供「快速架站懶人包」，協助您快速架構自己專屬、免費、安全、易用的視訊會議系統。

## 動機
2020全世界面臨武漢肺炎(新型冠狀病毒, COVID-19)威脅，使用視訊會議可以兼顧團隊工作效率、減少感染風險，可惜目前常見的視訊軟體有[資安隱憂](https://3c.ltn.com.tw/news/40047 "自由時報")，或者設定過於複雜需要專門人員操作管理，更有些需要另外額外收取費用，反而影響參與視訊會議的使用體驗。<br>
我們依照台灣機關學校視訊會議使用情境重新撰寫視訊系統，以[教育部](https://depart.moe.edu.tw/ED2700/News_Content.aspx?n=727087A8A1328DEE&s=868B3A6EDF9BA52D)、「台灣天才IT大臣」[唐鳳](https://3c.ltn.com.tw/news/40055)推薦使用的開源軟體[Jitsi meet](https://https://meet.jit.si/)為基礎，重新打造一套快速入手適用於台灣的視訊會議平台。<br>

使用「快速架站懶人包」將有下列好處：
### 學校機關系統管理者 
免費軟體安裝不易，是管理者心中痛點。我們提供本機、雲端(Google cloud 與 Azure)多種安裝方式、您僅需要照著網頁操作，簡單修改原始碼就可以替單位架設一套免費、安全隱密的會議系統，還可以依照您的需求自行延伸加上傳送開會通知、會議錄影、錄音字幕等等功能。
### 視訊會議使用者
與會者一直遲遲無法加入會議，是視訊會議最常見的痛點，我們將常見的視訊會議流程簡化為4個步驟，會議管理者僅需要照著網頁提示即可開啟會議、自動產生開會通知。視訊會議參與者不需高檔配備，僅需用手機掃條碼便可即時參加會議，讓視訊會議流程最通暢。

## 系統操作畫面
我們將以「陽明大學視訊系統」流程為藍本。
![系統首頁](https://github.com/Yuchunchen/BuildYourOwnConferenceSystem/blob/master/docs/images/desktop_screen010.png "畫面1.系統首頁")
###### 畫面1.系統首頁

![視訊會議步驟1](https://github.com/Yuchunchen/BuildYourOwnConferenceSystem/blob/master/docs/images/desktop_screen020.png "畫面2.視訊會議步驟一：開啟虛擬會議室")
###### 畫面2.視訊會議步驟一：開啟虛擬會議室

![視訊會議步驟2](https://github.com/Yuchunchen/BuildYourOwnConferenceSystem/blob/master/docs/images/desktop_screen030.png "畫面3.視訊會議步驟二：管理虛擬會議室")
###### 畫面3.視訊會議步驟二：管理虛擬會議室

![視訊會議步驟-設定密碼、開會通知](https://github.com/Yuchunchen/BuildYourOwnConferenceSystem/blob/master/docs/images/desktop_screen031.png "畫面4.視訊會議步驟三：設定密碼、開會通知")
###### 畫面4.視訊會議步驟三：設定密碼、開會通知

![視訊會議與會](https://github.com/Yuchunchen/BuildYourOwnConferenceSystem/blob/master/docs/images/desktop_screen040.png)
###### 畫面5.簡單易懂參加會議說明

![視訊會議異地開會](https://github.com/Yuchunchen/BuildYourOwnConferenceSystem/blob/master/docs/images/desktop_screen041.png)
###### 畫面6.視訊會議實際畫面

![系統說明](https://github.com/Yuchunchen/BuildYourOwnConferenceSystem/blob/master/docs/images/desktop_screen050.png)
###### 畫面7.系統說明

![團隊](https://github.com/Yuchunchen/BuildYourOwnConferenceSystem/blob/master/docs/images/desktop_screen060.png)
###### 畫面8.開發團隊

## 安裝需求
* 您必須有台安裝好Ubuntu LTS主機(或者您可以申請Azure或Google雲端帳號，我們也有提供安裝指引可以安裝在 Azure雲端 與 Google雲端，管理更為方便), **必要**
* 您的網域名稱和DNS紀錄(Valid domain with DNS record), **必要**.

## 系統安裝說明
![系統架構說明](https://github.com/Yuchunchen/BuildYourOwnConferenceSystem/blob/master/docs/images/thesystem_architecture.png.png "系統架構說明")

1. 安裝設定Jitsi meet系統後端
   1. 使用 Google 雲端
   2. 使用 Azure 雲端
2. 安裝客製化視訊系統前台。

## 相關應用
1. [台北榮民總醫院視訊門診系統](https://www.vghtpe.gov.tw/News!one.action?nid=6396)