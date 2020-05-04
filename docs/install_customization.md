# 客製化Jitsi更符合您的需求

- [客製化Jitsi更符合您的需求](#客製化Jitsi更符合您的需求)
    - [修改「陽明視訊系統」](#修改「陽明視訊系統」)
    - [修改首頁 Welcome page 文字](#修改首頁-welcome-page-文字)
    - [如何修改將錄影檔案上傳至雲端](#如何修改將錄影檔案上傳至雲端)

---

## 修改「陽明視訊系統」
隨著上述步驟安裝，您應該可以直接以 https://您的jitsi名稱/meet_ym.html (如：https://jitsiym.aigia.ai/meet_ym.html ) 方式進入系統試用，當然，您可以直接利用下列指令進行任意修改：
```bash
sudo nano /usr/share/jitsi-meet/meet_ym.html
```

## 修改首頁 Welcome page 文字

有的朋友會希望可以修改官方的 welcome page，大概有兩種方法：  
1. 官方版，建議由 github ( https://github.com/jitsi/jitsi-meet ) 下載原始碼，修改後再重新 compile
2. 快速版：直接修改 ```app.bundle.min.js``` 檔案：  
```bash
sudo nano /usr/share/jitsi-meet/libs/app.bundle.min.js
```

## 如何修改將錄影檔案上傳至雲端
在完成錄影後，依照預設檔案會放置於 (/var/jbrecord) 目錄下，同時會執行 /home/jibri/finalize_recording.sh 命令，預設 finalize_recording.sh 不會進行任何動作，您可以自行修改此檔案。 (錄影與上傳相關設定檔案在 /etc/jitsi/jibri/config.json ）  

##### 1. 利用 rclone 上傳至 Google, One drive 等雲端空間
[rclone](https://rclone.org/docs/) 可以將檔案上傳至雲端空間(目前支援37種！)，常見的Google, OneDrive, ftp, sftp, webdav 都在支援之列。這篇文章 [How-to to get a WORKING setup of Google Drive, One Drive or other cloud services in Jibri](https://community.jitsi.org/t/how-to-to-get-a-working-setup-of-google-drive-one-drive-or-other-cloud-services-in-jibri-my-comprehensive-tutorial-for-the-beginner/42228)是很重要的參考。

##### 2. 上傳到NAS系統，再透過NAS介面下載
可以參考 [這篇文章](https://community.jitsi.org/t/how-do-you-use-finalize-recordings-sh/28034/2)，使用者[toni](https://community.jitsi.org/u/toni)分享了他的 finalize_recording.sh 如下:  

```bash
#!/bin/bash

RECORDINGS_DIR=$1

echo "$RECORDINGS_DIR" > /tmp/verzeichnis.out
#echo "This is a dummy finalize script" > /tmp/finalize.out
#echo "The script was invoked with recordings directory $RECORDINGS_DIR." >> /t$
#echo "You should put any finalize logic (renaming, uploading to a service" >> $
#echo "or storage provider, etc.) in this script" >> /tmp/finalize.out
# The script exctracts the filename to prepare it for moving it to an external place, i.e. NAS drive

pfad=$(cat /tmp/verzeichnis.out)"/*mp4"
echo "$pfad" > /tmp/pfad.out
ls -l $pfad > /tmp/filename.out
filename=$(cat /tmp/filename.out)
filenameneu=$(echo $filename | cut -c 47-)
echo "$filenameneu" > tmp/filenameneu.out
transfername=$(echo $filenameneu | cut -c 34-)
echo "$transfername" > tmp/transfername.out
# The syno.txt file contains the user password for the NAS drive
sshpass -f /home/username/syno.txt scp $filenameneu username@NASdrivedomain.com/path/to/storagefolder/$transfername
# Save a backup of the previous mp4 for safety reason
cp /home/username/kopie.mp4 /home/username/kopie.mp4.bak
# copy a backup of the actually moved mp4 to the local user folder
cp $filenameneu /home/toni/kopie.mp4
remove=$(cat /tmp/verzeichnis.out)

rm -r $remove
exit 0

```
