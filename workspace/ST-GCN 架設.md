紀錄 Spatial Temporal Graph Convolutional Networks(ST-GCN) 的架設過程，ST-GCN是一種深度學習網路，將GCN應用到基於骨架的人體動作識別方法。

原論文: [Spatial Temporal Graph Convolutional Networks for Skeleton-Based Action Recognition](https://arxiv.org/abs/1801.07455)  
GitHub: [yysijie/st-gcn: Spatial Temporal Graph Convolutional Networks (ST-GCN) for Skeleton-Based Action Recognition in PyTorch](https://github.com/yysijie/st-gcn)

此紀錄尚未成功，若有進度會隨時更新本文，若有架設成功的案例歡迎分享，謝謝。

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
**PyTorch(0.4.0)**  
```shell
pip3 install torch==0.4.0 -f https://download.pytorch.org/whl/cu80/stable
```

**也要安裝 torchvision**
```shell
pip3 install torchvision -f https://download.pytorch.org/whl/cu80/stable
```

**OpenPose**  
請參考

**FFmpeg**  
```shell
sudo apt-get install ffmpeg
```
以此方法安裝的 FFmpeg ，在測試 demo 時會有以下錯誤
```
ValueError: No way to determine width or height from video. Need `-s` in `inputdict`. Consult documentation on I/O.
```
改以從 source code 編譯的方式安裝

**其他 Python liberties**
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

```shell
python3 main.py demo --openpose /home/brian/Desktop/paperProject/openpose/ [--video <path to your video> --device <gpu0> <gpu1>]
```
# 重新訓練模型
下載 Kinetics-skeleton 資料，並解壓縮。然後執行以下指令
```shell
python tools/kinetics_gendata.py --data_path <path to kinetics-skeleton>
```



# 參考資料
[动作识别初体验 - 知乎](https://zhuanlan.zhihu.com/p/40574587)

*最後編輯時間:2019/5/9*
<!--tags:
環境架設, 機器學習, 動作識別
-->
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGFnczogJ+eSsOWig+aetuiorSwg5q
mf5Zmo5a2457+SJ1xuIiwiaGlzdG9yeSI6WzIwODI5NDg2MDks
LTY4NTYwNDkxNywtNzU2NDQ1MDUwLDY4MTk1ODY4NywxNjE3ND
E5MjgzLDI3NDYzNDM4MywtMjEwNDI1NzYxMSwxOTc4MTI1MDk4
LDUzNzYzMDQ3NCwyNjU3NTg2MDIsLTI5Nzk1OTgxMywtNjkyOD
M0MTM0LDE2NTQxMzUwMTksLTk1MzIzNDg0NSw5MjYzMTUzNzcs
MTY5NjkyNDA5OF19
-->