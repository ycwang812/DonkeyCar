# 20200501 萬能科大 Donkey Car 工作坊

## 《WIFI》
SSID: asus_1_5G
PWK: 1234567890

SSID: asus_3_5G
PWK: 1234567890

## 《hackmd》==>先連到這個頁面
http://bit.ly/2WfbVwS

## 《投影片下載》
Donkey Car簡介
http://bit.ly/34V7pH6

HSP 簡介
http://go.aws/3bRyAGp

組裝驢車(Donkey Car)
http://go.aws/2Ylvre6

Raspberry Pi安裝設定
http://go.aws/2yZVa16

快速測試 Donkey Car
http://go.aws/3aObEqg

快速訓練 Donkey Car
http://go.aws/2YidTiU

Donkey Car 小工具
http://go.aws/2Srk4gN

淺談車道資料與模型
https://docs.google.com/presentation/d/1LlgIDAaXwxvLBhVaLIInivFAH7Pns0lHyUl_vYUREaw/edit?usp=sharing

## 《補充教材》
medium.com/十百千實驗室/樹莓派學開車-1ea713c35e03

## 《驅動程式和軟體下載》
PL2303_for_Windows
http://bit.ly/2OOlH3k

PL2303_for_MacOSX
http://bit.ly/2OKpEpW

putty_32bit
http://raspberrypi-tw.s3.amazonaws.com/download/putty_32bit.exe

putty_64bit
http://raspberrypi-tw.s3.amazonaws.com/download/putty_64bit.exe

Xming_for_Windows
http://raspberrypi-tw.s3.amazonaws.com/download/Xming-6-9-0-31-setup.exe

Xming_for_MacOSX(xquartz)
http://bit.ly/2DFnqVi

WinSCP_for_Windows
http://raspberrypi-tw.s3.amazonaws.com/download/WinSCP-5.15.1-Setup.exe


## 快速測試Donkey Car
### 《快速測試Donkey Car》安裝必要軟體(已安裝), p8
```
sudo apt-get update
sudo apt-get install -y vim x11vnc network-manager
sudo apt-get install -y cmake unzip pkg-config libjpeg-dev libpng-dev libtiff-dev libswscale-dev libv4l-dev libxvidcore-dev libx264-dev libavcodec-dev libavformat-dev libswscale-dev libv4l-dev libxvidcore-dev libx264-dev libgtk-3-dev libatlas-base-dev gfortran
sudo apt-get install -y git ntp i2c-tools avahi-utils joystick 
```

### 《快速測試Donkey Car》安裝donkeycar, p14(已安裝) 
```
cd ~
wget https://www.piwheels.org/simple/tensorflow/tensorflow-1.13.1-cp37-none-linux_armv7l.whl
sudo pip3 install tensorflow-1.13.1-cp37-none-linux_armv7l.whl
git clone https://github.com/autorope/donkeycar
cd donkeycar
git checkout ec7ea7a9d
time pip3 install -e .[pi]
```

### 《快速測試Donkey Car》加入 Python3 環境變數(已加入), p16
```
python3 -m virtualenv -p python3 env --system-site-packages
echo "source env/bin/activate" >> ~/.bashrc
source ~/.bashrc
```


### 《快速測試Donkey Car》建立第一個donkeycar專案, p18
```
cd ~
python -c "import donkeycar as dk; print(dk.__version__)"
donkey createcar --path ~/mycar
cd ~/mycar
ls
```


### 《快速測試Donkey Car》測試相機>拍照指令RaspiStill, p21
```
raspistill -v -o test.jpg 
```

### 《快速測試Donkey Car》測試相機>確認PCA9685馬達控制板接線正確, p37
```
i2cdetect -y 1
```

### 《快速測試Donkey Car》測試油門前進(Throttle) (hackmd), p39
```
donkey calibrate --channel 0 --bus=1
```

### 《快速測試Donkey Car》測試轉向(Steering)向右 (hackmd), p47
```
donkey calibrate --channel 1 --bus=1
```

### 《快速測試Donkey Car》使用瀏覽器控制, p53
```
cd ~/mycar
python3 sample_manage.py drive 
```

### 《快速測試Donkey Car》測試搖桿(hackmd), p57
```
jstest /dev/input/js0
```


### 《快速測試Donkey Car》將sample_manage.py複製到~/mycar, p49
```
cp ~/donkeypart_ps3_controller/sample_manage.py ~/mycar
```

### 《快速測試Donkey Car》將myconfig.py複製到~/mycar, p50
```
cp ~/donkeypart_ps3_controller/myconfig.py ~/mycar
```


### 《快速測試Donkey Car》使用瀏覽器控制, p49
```
cd ~/mycar
python3 sample_manage.py drive 
```

### 《快速測試Donkey Car》使用搖桿或是瀏覽器操作(用I/J/K/L控制)==>建議使用搖桿
開啟瀏覽器http://x.x.x.x:8887
一邊訓練一邊自動紀錄影像和油門與方向(左右)
![](https://i.imgur.com/tLi9Z9b.jpg)


### 《快速測試Donkey Car》測試搖桿, p53
```
jstest /dev/input/js0
```

### 《快速測試Donkey Car》1.安裝搖桿控制程式(未安裝/hackmd), p61
```
cd ~
git clone https://github.com/raspberrypi-tw/donkeypart_ps3_controller
cd ~/donkeypart_ps3_controller
python3 setup.py install
```

### 《快速測試Donkey Car》2.使用搖桿控制 (hackmd), p62
```
cd ~/mycar
cp ~/donkeypart_ps3_controller/sample_manage.py .

python3 sample_manage.py drive --js
```


## 快速訓練Donkey Car
### 《快速訓練Donkey Car》使用搖桿控制, p18
```
cd ~/mycar
cp ~/donkeypart_ps3_controller/sample_manage.py .
python3 sample_manage.py drive --js
```

### 《快速訓練Donkey Car》設定git帳號, p24
```
cd ~/mycar
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```

### 《快速訓練Donkey Car》將資訊push到github, p25
```
cd ~/mycar
git init
git add .
git commit -m "喜歡的註解"
# git remote add origin https://github.com/<ID>/<REPO>
git push -u origin master
```

# Google Colab
## http://bit.ly/2ODIpNw

### 《快速訓練Donkey Car》執行自走功能, p33
```
cd ~/mycar
python3 sample_manage.py drive --model models/lin_1.h5
```

### 《快速訓練Donkey Car》執行 RNN 自走功能
```
cd ~/mycar
python3 sample_manage.py drive --model models/rnn_1.h5 --type rnn
```


### 使用訓練資料建立模型mypilot(在Google Colab)
```
python manage.py train --tub ./tub --model ./models/mypilot
```

### 訓練完成後自走(將Google Colab訓練好的模型放回Duckiebot上的Pi)
```
python3 sample_manage.py drive --model ~/mycar/models/mypilot
```
## 機器學習速成班(分類問題使用 Google Colab)
https://www.tensorflow.org/tutorials/customization/custom_training_walkthrough



## SD卡備份教學
[ Raspberry Pi ] Win32 Disk Imager 備份 SD 卡教學
http://bit.ly/2Qx7rjz

## 相機預覽(camera preview)
```
sudo pip3 install imutils
cd ~
wget http://raspberrypi-tw.s3.amazonaws.com/code/camera_preview.py
python3 camera_preview.py
```

###### tags: `workshop`, `vnu`, `donkey car`, `donkeycar`



