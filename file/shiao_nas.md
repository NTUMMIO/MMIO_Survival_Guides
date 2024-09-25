MMIO 430小NAS 連線實戰手冊
===
2024.09.06 updated
---
# I. 網頁連線登入
>* 網頁搜尋 **"Synology QuickConnect"** 並進入網站 (<https://quickconnect.to/>)  
>* 輸入QuickConnect ID(實驗室共有) 並連線。  
>* 登入自己的NAS使用者帳號，進入NAS主畫面。  
---
# II. 使用網頁 上傳／下載 (GUI)
>* 進入 **File Station** 內 **home** 位置。
>* 可以執行建立資料夾、上傳檔案、下載等操作。
---
---
# III. 使用MobaXterm SFTP連線登入
>* command line 輸入指令。  
> 連線到使用者帳號，並輸入密碼。
>```bash
> sftp -P 100 <username>@<NAS IP>
> # e.g. sftp -P 100 MultiModal@257.257.257.257
>```
>* 進入NAS後，你會看到：  
>```bash
> sftp> 
>```
>* 可以使用 Linux Command 操作。例如：
>```bash
> ls  #查看當前路徑下的檔案
>
> cd home/  #移至當前路徑下的 home 資料夾
>```
>* 退出連線。  
>```bash
> quit
>```
---
# IV. 在MobaXterm SFTP連線 上傳／下載檔案 (commands)
>* 上傳 MobaXtterm 上的檔案 \<local_file_path\> 到 NAS 上的目標路徑 \<nas_destination\>。
>```bash
> put <local_file_path> <nas_destination>
>
> put <local_file_path>  #上傳檔案到NAS的當前路徑
>```
>* 從 NAS 下載檔案 \<nas_file_path\> 到 MobaXterm 上的目標路徑 \<local_destination\>。
>```bash
> get <nas_file_path> <local_destination>
>
> get <nas_file_path>  #下載檔案到MobaXterm的當前路徑
>```
