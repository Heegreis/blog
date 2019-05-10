本文的作業系統是 ubuntu 16.04，並且安裝的是 GPU 版本
[readmore]
**目錄**  
[TOC]
# Clone
```shell
git clone https://github.com/CMU-Perceptual-Computing-Lab/openpose
```

然後我們移動到 openpose資料夾底下，進行下面的指令操作。
# Prerequisites
這邊採用Cmake GUI的方式安裝。筆者另外有建立OpenPose的docker版本則是使用 command line 的方式安裝。
**安裝 Cmake GUI**
```shell
sudo apt-get install cmake-qt-gui
```

**安裝 CUDA 8**
```shell
sudo ./scripts/ubuntu/install_cuda.sh
```

**安裝 cuDNN 5.1**
```shell
sudo ./scripts/ubuntu/install_cudnn.sh
```

**安裝 Caffe 的 prerequisites**
```shell
sudo bash ./scripts/ubuntu/install_deps.sh
```

**安裝 opencv**
```shell
sudo apt-get install libopencv-dev
```
# 安裝
先確認 OpenPose 專案下的 3rdparty/caffe 資料夾是不是空的，如果是空的擇執行以下指令
```shell
git submodule init
git submodle update
```
開啟 Cmake

# 參考資料
[Installing TensorFlow on Windows | TensorFlow](https://www.tensorflow.org/install/install_windows)

[^1]: [被引用連結說明:](http://tieba.baidu.com/p/4565248851)

*最後編輯時間:2018/5/10*
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTUyMDE2MDc4NiwtMTE0NzAzNDcxMSwtMT
A3NTE1MjYsLTE4OTMxMzcwNTJdfQ==
-->