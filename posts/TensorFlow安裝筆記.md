紀錄在 windows 10 安裝 TensorFlow GPU 版本的過程
[readmore]
**目錄**
[TOC]

# 安裝

## 安裝TensorFlow

此筆記紀錄支援GPU的安裝版本，安裝環境GPU為GeForce GTX 750 Ti 繪圖卡。

### 安裝CUDA 8.0

#### 下載、安裝

CUDA 8 下載網址: <https://developer.nvidia.com/cuda-80-ga2-download-archive>
此筆記選擇local版本安裝。

選擇所要的版本下載完成後，打開安裝程式，照著指示安裝。此筆記安裝選項選擇: 快速(建議)。
並安裝Patch 2 (Released Jun 26, 2017)做補丁更新。

#### 檢查配置是否正確
檢查CUDA Toolkit的版本: 在**命令提示字元**中輸入 `nvcc -V` 。

驗證硬體與軟體的正確配置，官方文件強烈建議在**預設路徑** `C:\ProgramData\NVIDIA Corporation\CUDA Samples\v8.0\bin\win64\Release` 中執行 `DEVICEQUERY`
筆者結果如下:
```shell
C:\ProgramData\NVIDIA Corporation\CUDA Samples\v8.0\bin\win64\Release>DEVICEQUERY
DEVICEQUERY Starting...

 CUDA Device Query (Runtime API) version (CUDART static linking)

Detected 1 CUDA Capable device(s)

Device 0: "GeForce GTX 750 Ti"
  CUDA Driver Version / Runtime Version          8.0 / 8.0
  CUDA Capability Major/Minor version number:    5.0
  Total amount of global memory:                 2048 MBytes (2147483648 bytes)
  ( 5) Multiprocessors, (128) CUDA Cores/MP:     640 CUDA Cores
  GPU Max Clock rate:                            1137 MHz (1.14 GHz)
  Memory Clock rate:                             2700 Mhz
  Memory Bus Width:                              128-bit
  L2 Cache Size:                                 2097152 bytes
  Maximum Texture Dimension Size (x,y,z)         1D=(65536), 2D=(65536, 65536), 3D=(4096, 4096, 4096)
  Maximum Layered 1D Texture Size, (num) layers  1D=(16384), 2048 layers
  Maximum Layered 2D Texture Size, (num) layers  2D=(16384, 16384), 2048 layers
  Total amount of constant memory:               65536 bytes
  Total amount of shared memory per block:       49152 bytes
  Total number of registers available per block: 65536
  Warp size:                                     32
  Maximum number of threads per multiprocessor:  2048
  Maximum number of threads per block:           1024
  Max dimension size of a thread block (x,y,z): (1024, 1024, 64)
  Max dimension size of a grid size    (x,y,z): (2147483647, 65535, 65535)
  Maximum memory pitch:                          2147483647 bytes
  Texture alignment:                             512 bytes
  Concurrent copy and kernel execution:          Yes with 1 copy engine(s)
  Run time limit on kernels:                     Yes
  Integrated GPU sharing Host Memory:            No
  Support host page-locked memory mapping:       Yes
  Alignment requirement for Surfaces:            Yes
  Device has ECC support:                        Disabled
  CUDA Device Driver Mode (TCC or WDDM):         WDDM (Windows Display Driver Model)
  Device supports Unified Addressing (UVA):      Yes
  Device PCI Domain ID / Bus ID / location ID:   0 / 1 / 0
  Compute Mode:
     < Default (multiple host threads can use ::cudaSetDevice() with device simultaneously) >

deviceQuery, CUDA Driver = CUDART, CUDA Driver Version = 8.0, CUDA Runtime Version = 8.0, NumDevs = 1, Device0 = GeForce GTX 750 Ti
Result = PASS
```
主要確保有偵測到與系統所安裝符合的設備，筆者即為**GeForce GTX 750 Ti** 。

若cmd找不到 `DEVICEQUERY` ，則到**預設路徑** `C:\ProgramData\NVIDIA Corporation\CUDA Samples\v8.0\1_Utilities\deviceQuery` 找到與系統對應的VS版本.sln檔進行編譯，如筆者為**VS2013版**，包括Debug與Release皆進行編譯 [[1]]。編譯後即可回去執行 `DEVICEQUERY` 。

(另有 `bandwidthTest` 部分，cmd找不到，筆者未能理解，暫為保留)
(設定 `$path` 尚待理解，現確認有未新專案增加路徑與現存專案增加路徑2種)

### 安裝cuDNN 6.0

cuDNN下載網址: <https://developer.nvidia.com/rdp/cudnn-download>
需註冊nVIDIA developer帳號才能下載。

選擇符合的作業系統版本安裝，下載後為一個壓縮檔，將**CUDA** 資料夾裡面的3個資料夾: **bin**、**include**、**lib**，解壓縮至 `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v8.0` 中 [[2]]。此筆記使用**cuDNN v6.0 (April 27, 2017), for CUDA 8.0**。

### 原生pip安裝TensorFlow

#### 安裝

此筆記選擇GPU版本TensorFlow，使用以下指令:
```shell
C:\> pip3 install --upgrade tensorflow-gpu
```
此指令會下載最新的版本，筆者此時的版本為1.4
#### 驗證安裝成功

在**shell**裡啟動**python**(筆者使用cmd):
```shell
$ python
```

並在裡面輸入以下python程式碼:
```python
>>> import tensorflow as tf
>>> hello = tf.constant('Hello, TensorFlow!')
>>> sess = tf.Session()
>>> print(sess.run(hello))
```
若輸出為`Hello, TensorFlow!` 表示成功可執行。

# 參考資料

Installing TensorFlow on Windows | TensorFlow
<https://www.tensorflow.org/install/install_windows>

Installation Guide Windows :: CUDA Toolkit Documentation
<https://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/>

问一下大神deviceQuery.exe怎没有呢【cuda吧】_百度贴吧 \[1]
[1]: http://tieba.baidu.com/p/4565248851
<http://tieba.baidu.com/p/4565248851>

閱讀記事: 於Win10環境下配置CUDA與cuDNN \[2]
[2]: https://rreadmorebooks.blogspot.tw/2017/04/win10cudacudnn.html
<https://rreadmorebooks.blogspot.tw/2017/04/win10cudacudnn.html>

最後編輯日期: 2017/12/29
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGFnczogVGVuc29yRmxvd1xuZGF0ZT
ogJzIwMTctMTItMjUnXG4iLCJoaXN0b3J5IjpbLTk0ODE1Njcx
MywzODk2MDYwOTddfQ==
-->