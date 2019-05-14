紀錄 Spatial Temporal Graph Convolutional Networks(ST-GCN) 的架設過程，ST-GCN是一種深度學習網路，將GCN應用到基於骨架的人體動作識別方法。

原論文: [Spatial Temporal Graph Convolutional Networks for Skeleton-Based Action Recognition](https://arxiv.org/abs/1801.07455)  
GitHub: [yysijie/st-gcn: Spatial Temporal Graph Convolutional Networks (ST-GCN) for Skeleton-Based Action Recognition in PyTorch](https://github.com/yysijie/st-gcn)

此紀錄尚未成功，若有進度會隨時更新本文，若有架設成功的案例歡迎分享，謝謝。
[readmore]
**目錄**
[TOC]
# Prerequisites
**PyTorch(0.4.0)**  
```shell
pip install torch==0.4.0 -f https://download.pytorch.org/whl/cu80/stable
```

**OpenPose**  
已安裝

**FFmpeg**  
```shell
sudo apt-get install ffmpeg
```

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
環境架設, 機器學習
-->
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGFnczogJ+eSsOWig+aetuiorSwg5q
mf5Zmo5a2457+SJ1xuIiwiaGlzdG9yeSI6WzExNzcxNDk0OTYs
Mjc0NjM0MzgzLC0yMTA0MjU3NjExLDE5NzgxMjUwOTgsNTM3Nj
MwNDc0LDI2NTc1ODYwMiwtMjk3OTU5ODEzLC02OTI4MzQxMzQs
MTY1NDEzNTAxOSwtOTUzMjM0ODQ1LDkyNjMxNTM3NywxNjk2OT
I0MDk4XX0=
-->