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
[^1]筆者使用Cmake GUI的方式安裝，遇到很多錯誤，所以就改用 command line 的方式安裝。

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
## OpenPose Configuration
[^3]開啟 Cmake 的 GUI 後
- 在上方的 `Where is the source code` 欄位選擇 openpose 資料夾  
- 在 `Where to build the binaries` 欄位選擇 openpose 資料夾，並在後面加上 `/build`  
- 然後按下左下方的 `Configure` 按鈕
- 出現是否建立資料夾就選yes，其他照預設的選擇

等跑完後，出現 `Configuring done` 表示成功  然後按下 `Generate` 按鈕後就可以關掉 Cmake 的視窗了
## OpenPose Building
```shell
cd build/
make -j`nproc`
```
# 參考資料
[CMU-Perceptual-Computing-Lab/openpose: OpenPose: Real-time multi-person keypoint detection library for body, face, hands, and foot estimation](https://github.com/CMU-Perceptual-Computing-Lab/openpose)

[^1]: [openpose/prerequisites.md at master · CMU-Perceptual-Computing-Lab/openpose](https://github.com/CMU-Perceptual-Computing-Lab/openpose/blob/master/doc/prerequisites.md)
[^2]:[Ubuntu Cmake-gui error while getting default Caffe · Issue #423 · CMU-Perceptual-Computing-Lab/openpose](https://github.com/CMU-Perceptual-Computing-Lab/openpose/issues/423)
[^3]:[openpose/installation.md at master · CMU-Perceptual-Computing-Lab/openpose](https://github.com/CMU-Perceptual-Computing-Lab/openpose/blob/master/doc/installation.md)
*最後編輯時間:2018/5/10*
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIxMjEyNTA1NjcsMTM5NzM4NDYyOSwtOD
A5MzI3MTM1LDEyMDY5MDQ3MTksMTEyOTU5MzcyLC0xMTQ3MDM0
NzExLC0xMDc1MTUyNiwtMTg5MzEzNzA1Ml19
-->