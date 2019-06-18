# Install Nvidia Driver on Ubuntu (14.04/16.04)
* 安裝方式分成兩種
  1. 使用官網的 .run 安裝 (強烈建議)
  2. 使用 apt-get 安裝

## 使用官網的 .run 安裝 (強烈建議)
### 1. 禁止整合的nouveau驅動
* ubuntu 系統整合的顯示卡驅動程式是 nouveau，它是第三方為 NVIDIA 開發的開源驅動，我們需要先將其遮蔽才能安裝 NVIDIA 官方驅動。[1]
* 將驅動新增到黑名單 blacklist.conf 中，但是由於該檔案的屬性不允許修改。所以需要先修改檔案屬性。
```
sudo nano /etc/modprobe.d/blacklist.conf
```
* 在該檔案後新增一下幾行：
```
blacklist vga16fb
blacklist nouveau
blacklist rivafb
blacklist nvidiafb
blacklist rivatv
```
* 接著 reload kernel 並重啟電腦：
```
sudo update-initramfs -u
sudo reboot
```
* 重開機後可用下列指令確定是否屏蔽成功：
```
lsmod | grep nouveau
```
### 2. 解除舊版本(如果有)並關閉圖形介面
```
sudo apt-get purge nvidia-*
sudo service lightdm stop
```
### 3. 從官網選取對應的顯卡型號下載 .run 檔
* (https://www.nvidia.com.tw/Download/index.aspx?lang=tw)
* 修改檔案權限
```
wget http://us.download.nvidia.com/XFree86/Linux-x86_64/430.26/NVIDIA-Linux-x86_64-430.26.run
sudo chmod 755 NVIDIA-Linux-x86_64-430.26.run
```
### 4. 開始安裝
```
sudo ./NVIDIA-Linux-x86_64-430.26.run
```
* 可能遇到的訊息
   1. The distribution-provided pre-install script failed! Are you sure you want to continue? 選擇 yes 繼續。
   2. Would you like to register the kernel module souces with DKMS? This will allow DKMS to automatically build a new module, if you install a different kernel later?  選擇 No 繼續。
   3. Nvidia's 32-bit compatibility libraries? 選擇 No 繼續。
   4. Would you like to run the nvidia-xconfigutility to automatically update your x configuration so that the NVIDIA x driver will be used when you restart x? Any pre-existing x confile will be backed up.  選擇 Yes 繼續。
### 5. 檢查安裝是否成功
* 觀察顯卡狀態，可能要 sudo reboot 才能執行，但正常應該是可以直接執行
```
nvidia-smi
```
* 觀察 nvidia 程序，確認是否包含 nvidia_uvm、nvidia_drm、nvidia_modeset
```
lsmod | grep nvidia
```
## 使用 apt-get 安裝
* 與 .run 檔相同，需要先禁止整合 nouveau 驅動
* 刪除舊版 nvidia driver
* 關閉圖形介面 (sudo service lightdm stop)
### 1. 更新來源
```
sudo add-apt-repository ppa:graphics-drivers/ppa
```
### 2. 安裝並重啟
```
sudo apt-get install nvidia-430
sudo reboot
```
* 檢查則可以參考第一種的方法的第 5 點

## 參考資料 : 
1. Unable to load the kernel module 'nvidia.ko' : https://stackoverflow.com/questions/24734986/unable-to-load-the-kernel-module-nvidia-ko
2. 大部分步驟參考 : https://www.itread01.com/content/1549538125.html
