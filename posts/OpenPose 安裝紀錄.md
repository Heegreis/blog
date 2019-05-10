本文紀錄安裝 OpenPose 的過程。OpenPose 是用來偵測出人體骨架的開源系統，為一種 姿態估計(pose estimation)的方法。  
筆者使用的作業系統是 ubuntu 16.04，GPU 版本是 1080 Ti
[readmore]
**目錄**  
[TOC]
# Clone 專案
```shell
git clone https://github.com/CMU-Perceptual-Computing-Lab/openpose
```
然後我們移動到 openpose資料夾底下，進行下面的指令操作
# Prerequisites
[^1]筆者曾經使用Cmake GUI的方式安裝，遇到很多錯誤，所以就改用 command line 的方式安裝。

**安裝 CUDA 8**
```shell
sudo ./scripts/ubuntu/install_cuda.sh
```

**安裝 cuDNN 5.1**
```shell
sudo ./scripts/ubuntu/install_cudnn.sh
```
在嘗試透過 Cmake GUI 安裝時，遇到錯誤有改 cuDNN 到 7.0.5版，但就沒在改回 cuDNN 5.1 版了，但使用 cuDNN 5.1 應該不會有錯。

**安裝 Caffe 的 prerequisites**
```shell
sudo bash ./scripts/ubuntu/install_deps.sh
```

**安裝 opencv**
```shell
sudo apt-get install libopencv-dev
```
**重新開機**
以便系統可以找到 CUDA
# 安裝
## OpenPose Configuration and Building
[^2]Configuration
```shell
mkdir build
cd build
cmake ..
```

Building
```shell
make -j`nproc`
```
# 測試 demo
回到OpenPose 專案的根目錄，執行demo
```shell
./build/examples/openpose/openpose.bin --video examples/media/video.avi
```
成功的話就會跑出範例影片抓取骨架的即時畫面
# 參考資料
[CMU-Perceptual-Computing-Lab/openpose: OpenPose: Real-time multi-person keypoint detection library for body, face, hands, and foot estimation](https://github.com/CMU-Perceptual-Computing-Lab/openpose)

[^1]: [openpose/prerequisites.md at master · CMU-Perceptual-Computing-Lab/openpose](https://github.com/CMU-Perceptual-Computing-Lab/openpose/blob/master/doc/prerequisites.md)
[^2]:[openpose/installation.md at master · CMU-Perceptual-Computing-Lab/openpose](https://github.com/CMU-Perceptual-Computing-Lab/openpose/blob/master/doc/installation.md)
*最後編輯時間:2019/5/10*

<!--stackedit_data:
eyJoaXN0b3J5IjpbMjA0NjA0ODIxNSw1MDk1MDk2MDldfQ==
-->