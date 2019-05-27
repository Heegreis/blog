紀錄 Spatial Temporal Graph Convolutional Networks(ST-GCN) 的架設過程，ST-GCN是一種深度學習網路，將GCN應用到基於骨架的人體動作識別方法。

原論文: [Spatial Temporal Graph Convolutional Networks for Skeleton-Based Action Recognition](https://arxiv.org/abs/1801.07455)  
GitHub: [yysijie/st-gcn: Spatial Temporal Graph Convolutional Networks (ST-GCN) for Skeleton-Based Action Recognition in PyTorch](https://github.com/yysijie/st-gcn)

st-gcn 是用 python 3 運行，雖然原作者的指令都是用 `python` ，但筆者的 python 預設為 2，所以以下皆會替換成 `python3` 的指令。
[readmore]
**目錄**
[TOC]
# Clone
在想要的目錄下，clone該專案
```shell
git clone https://github.com/yysijie/st-gcn.git
```
# Prerequisites
## PyTorch(0.4.0)
```shell
pip3 install torch==0.4.0 -f https://download.pytorch.org/whl/cu80/stable
```

**也要安裝 torchvision**
```shell
pip3 install torchvision -f https://download.pytorch.org/whl/cu80/stable
```

## OpenPose
請參考 [OpenPose 安裝紀錄](https://heegreis.blogspot.com/2019/05/openpose.html) ([github](https://github.com/Heegreis/blogger/blob/master/posts/OpenPose%20%E5%AE%89%E8%A3%9D%E7%B4%80%E9%8C%84.md))

## FFmpeg
**失敗的安裝方式**
```shell
sudo apt-get install ffmpeg
```
以此方法安裝的 FFmpeg ，在測試 demo 時會有以下錯誤:  
```
ValueError: No way to determine width or height from video. Need `-s` in `inputdict`. Consult documentation on I/O.
```
**可行的安裝方式**
改為從 source code 編譯的方式安裝 FFmpeg[^1] :
以下的安裝FFmpeg的部分，筆者會另外開一個資料夾，在裡面進行編譯與安裝的步驟，因為會下載蠻多東西的。如 `~/ffmpeg_sources/`

先移除已存在的 packages
```shell
sudo apt -y  remove ffmpeg x264 libav-tools libvpx-dev libx264-dev
```

安裝依賴庫
```shell
sudo apt-get update
sudo apt-get -y install build-essential checkinstall git libfaac-dev libgpac-dev \
  libjack-jackd2-dev libmp3lame-dev libopencore-amrnb-dev libopencore-amrwb-dev \
  librtmp-dev libsdl1.2-dev libtheora-dev libva-dev libvdpau-dev libvorbis-dev \
  libx11-dev libxfixes-dev pkg-config texi2html yasm zlib1g-dev
```

Install Yasm
```shell
cd ~/ffmpeg_sources
wget http://www.tortall.net/projects/yasm/releases/yasm-1.3.0.tar.gz
tar xzvf yasm-1.3.0.tar.gz
cd yasm-1.3.0
./configure --prefix="$HOME/ffmpeg_build" --bindir="$HOME/bin"
make
make install
```

Install nasm
```shell
cd ~/ffmpeg_sources
wget http://www.nasm.us/pub/nasm/releasebuilds/2.13.01/nasm-2.13.01.tar.bz2
tar xjvf nasm-2.13.01.tar.bz2
cd nasm-2.13.01
./autogen.sh
PATH="$HOME/bin:$PATH" ./configure --prefix="$HOME/ffmpeg_build" --bindir="$HOME/bin"
PATH="$HOME/bin:$PATH" make
make install
```

libx264
```shell
sudo apt-get install libx264-dev
```

libx265
```shell
sudo apt-get install libx265-dev
```

libfdk-aac
```shell
sudo apt-get install libfdk-aac-dev
```

libmp3lame
```shell
sudo apt-get install libmp3lame-dev
```

libopus
```shell
sudo apt-get install libopus-dev
```

libvpx
```shell
sudo apt-get install libvpx-dev
```

筆者在執行稍候的FFmpeg指令時，會出現以下錯誤:  
```
ERROR: libass not found using pkg-config
```

所以需要安裝 libass[^3] [^4] :  
[FreeType-2.10.0](https://downloads.sourceforge.net/freetype/freetype-2.10.0.tar.bz2) 下載並解壓縮後，進到解壓縮後的資料夾，執行以下指令
```shell
./configure --prefix=/usr --enable-freetype-config --disable-static && make
```
[FriBidi-1.0.5](https://github.com/fribidi/fribidi/releases/download/v1.0.5/fribidi-1.0.5.tar.bz2) 下載並解壓縮後，進到解壓縮後的資料夾，執行以下指令
```shell
./configure --prefix=/usr --disable-docs && make
```
[Fontconfig-2.13.1](https://www.freedesktop.org/software/fontconfig/release/fontconfig-2.13.1.tar.bz2) 下載並解壓縮後，進到解壓縮後的資料夾，執行以下指令
```shell
./configure --prefix=/usr -disable-docs && make && sudo make install
```
安裝 libass
```shell
git clone https://github.com/libass/libass.git
cd libass
sh autogen.sh
./configure --prefix=/usr --disable-static && make
sudo make install
```
設定環境變數
```shell
export PKG_CONFIG_PATH=/usr/local/ass/lib/pkgconfig:$PKG_CONFIG_PATH
```

安裝 FFmpeg[^1] [^2]
```shell
cd ~/ffmpeg_sources
git clone --depth 1 https://git.ffmpeg.org/ffmpeg.git
cd ffmpeg
PATH="$HOME/bin:$PATH" PKG_CONFIG_PATH="$HOME/ffmpeg_build/lib/pkgconfig" ./configure \
  --prefix="$HOME/ffmpeg_build" \
  --pkg-config-flags="--static" \
  --extra-cflags="-I$HOME/ffmpeg_build/include" \
  --extra-ldflags="-L$HOME/ffmpeg_build/lib" \
  --bindir="$HOME/bin" \
  --enable-gpl \
  --enable-libass \
  --enable-libfdk-aac \
  --enable-libfreetype \
  --enable-libmp3lame \
  --enable-libopencore-amrnb \
  --enable-libopencore-amrwb \
  --enable-librtmp \
  --enable-libopus \
  --enable-libtheora \
  --enable-libvorbis \
  --enable-libvpx \
  --enable-libx264 \
  --enable-libx265 \
  --enable-nonfree \
  --enable-version3 \
  --enable-libxcb
PATH="$HOME/bin:$PATH" make
make install
hash -r
```
## 其他 Python liberties
```
cd st-gcn
pip3 install -r requirements.txt
```
# 安裝

不知道為什麼 ``python setup.py install`` 會有權限問題，各位在安裝時可以試試看不加 ``sudo`` 能不能安裝
```shell
cd torchlight; sudo python3 setup.py install; cd ..
```
# 下載預訓練模型權重
```shell
bash tools/get_models.sh
```
# 測試demo
```shell
python3 main.py demo --openpose <path to openpose build directory> [--video <path to your video> --device <gpu0> <gpu1>]
```
範例:  
```shell
python3 main.py demo --openpose /data/paperProjects/openpose/build --video /data/paperProjects/st-gcn/resource/media/ta_chi.mp4 --device 0
```

# 參考資料
[动作识别初体验 - 知乎](https://zhuanlan.zhihu.com/p/40574587)

[ST-GCN網絡安裝過程中遇到的問題 - 台部落](https://www.twblogs.net/a/5c76c74dbd9eee33991817c9)

[^1]:[Compile FFmpeg on Ubuntu 16.04](https://gist.github.com/teocci/f7a438013a0197a91446ee86de41faee)

[^2]:[image - Unknown option "--enable-x11grab" when installing ffmpeg on centos (6.8) - Stack Overflow](https://stackoverflow.com/questions/43364400/unknown-option-enable-x11grab-when-installing-ffmpeg-on-centos-6-8)

[^3]:[FFmpeg编译记-依懒库安装-广东IDC网](http://aliyun.gdidc.com.cn/forum/8713/)

[^4]:[ffmpeg在PC上编译问题全解决_张志辉kom_新浪博客](http://blog.sina.com.cn/s/blog_61bc01360102w815.html)

*最後編輯時間:2019/5/28*
<!--tags:
環境架設, 機器學習, 動作識別
-->
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGFnczogJ+eSsOWig+aetuiorSwg5q
mf5Zmo5a2457+SJ1xuIiwiaGlzdG9yeSI6Wy03Nzk0NzAwNDgs
NjIzNzg0OTQzLC0xNzU2NzU4NTYyLC0xODg2NjAwODM5LC0xMz
EwNzIxMTUyLC0yMDAyOTE5OTk1LDEyMDQ1NDQ2MTcsMTg1MTI0
MjkwNCwzMjg0MjMzMDMsMTU3MDEwODEwMCwtNjg1NjA0OTE3LC
03NTY0NDUwNTAsNjgxOTU4Njg3LDk0ODU1OTA5OSwxNjE3NDE5
MjgzLDI3NDYzNDM4MywtMjEwNDI1NzYxMSwxOTc4MTI1MDk4LD
UzNzYzMDQ3NCwyNjU3NTg2MDJdfQ==
-->