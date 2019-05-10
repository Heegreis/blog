本文的作業系統是 ubuntu 16.04，並且安裝的是 GPU 版本
[readmore]
**目錄**  
[TOC]
# Clone
```shell
git clone https://github.com/CMU-Perceptual-Computing-Lab/openpose
```
然後我們移動到 openpose資料夾底下，進行下面的指令操作
# Prerequisites
[^1]這邊採用Cmake GUI的方式安裝。筆者另外有建立OpenPose的docker版本則是使用 command line 的方式安裝。
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
先確認 OpenPose 專案下的 3rdparty/caffe 資料夾是不是空的，如果是空的則執行以下指令
```shell
git submodule init
git submodle update
```
開啟 Cmake

# 參考資料
[CMU-Perceptual-Computing-Lab/openpose: OpenPose: Real-time multi-person keypoint detection library for body, face, hands, and foot estimation](https://github.com/CMU-Perceptual-Computing-Lab/openpose)

[^1]: [openpose/prerequisites.md at master · CMU-Perceptual-Computing-Lab/openpose](https://github.com/CMU-Perceptual-Computing-Lab/openpose/blob/master/doc/prerequisites.md)

*最後編輯時間:2018/5/10*
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTIwNjkwNDcxOSwxMTI5NTkzNzIsLTExND
cwMzQ3MTEsLTEwNzUxNTI2LC0xODkzMTM3MDUyXX0=
-->