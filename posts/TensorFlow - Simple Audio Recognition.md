---
title: TensorFlow - Simple Audio Recognition
date: 2017/12/29
updated: 2017/12/29
abbrlink: bccd72eb
description:
第一次嘗試使用TensorFlow，紀錄官方教學的Simple Audio Recognition專案建置與使用過程。
---
第一次嘗試使用TensorFlow，紀錄官方教學的[Simple Audio Recognition](https://www.tensorflow.org/versions/master/tutorials/audio_recognition "Simple Audio Recognition  |  TensorFlow")專案建置與使用過程。
<!--more-->
筆者的使用環境為Win10，TensorFlow環境請參見[TensorFlow安裝筆記](https://heegreis.blogspot.tw/2017/12/tensorflow.html "Blogger內部連結")一文。

目前撰寫到訓練步驟，後續待補...

# 下載專案
因筆者透過非透過Sources安裝TensorFlow，安裝好的examples資料夾內無Simple Audio Recognition的範例專案。需先至GitHub下載: 
https://github.com/tensorflow/tensorflow/tree/master/tensorflow/examples/speech_commands

筆者是直接下載整個tensorflow的Sources。

# 執行專案

## 訓練模型
找到對應路徑後執行`train.py`檔
```bash
python tensorflow/examples/speech_commands/train.py
```
在**TensorFlow1.4**版應會報錯，如同此討論串: [[Windows] Speech commands tutorial does not work #14004](https://github.com/tensorflow/tensorflow/issues/14004 "[Windows] Speech commands tutorial does not work · Issue #14004 · tensorflow/tensorflow · GitHub")。
解決方法: 等待**TensorFlow1.5**出來，或安裝`tf-nightly`
```bash
pip3 install tf-nightly
```
或
```bash
pip3 install tf-nightly-gpu
```
筆者安裝版本為: **tf-nightly-gpu-1.5.0.dev20171228**

執行後，專案一開始會檢查是否已下載過[Speech Commands dataset](https://storage.cloud.google.com/download.tensorflow.org/data/speech_commands_v0.01.tar.gz)，若沒有則會自動開始下載**Speech Commands dataset**，筆者在下載期間出現下載失敗，但其實後來發現，在路徑`C:\tmp\speech_dataset`出現下載到一半的壓縮檔。
這時只要直接點選上述連結下載**Speech Commands dataset**壓縮檔，替換掉損毀的檔案即可再次執行`train.py`。
順利執行便會進入訓練。

最後編輯日期: 2017/12/29
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjAwNDczNDM4MV19
-->