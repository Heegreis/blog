紀錄在 windows 10 安裝 Keras 的過程
[readmore]
**目錄**
[TOC]
# 安裝backend

keras支援的backend，3種至少須選擇一種:

* TensorFlow * Theano * CNTK



請見 **Tensorflow**安裝筆記一文。

# 安裝Keras

## 安裝

在cmd中輸入:
```殼
> PIP3安裝keras -U -事先```若會發生PermissionError的錯誤，請改輸入[[1]]:```shell> pip3 install keras -U --pre --user```





## 驗證安裝成功

在shell裡(筆者使用cmd)進入python:
```殼
>蟒```


在python環境中，輸入以下程式碼:
```蟒蛇>> > 進口 keras ```


若沒有報錯，表示Keras成功安裝。

Keras中mnist數據集測試下載Keras開發包，在欲放置開發包的資料夾輸入以下git指令:
```bash的
 $ git的克隆https://github.com/fchollet/keras.git 
$ CD keras /例子/ 
$蟒蛇mnist_mlp.py ```

程式執行沒有錯誤，即成功。

# 參考資料

[1]: http://blog.csdn.net/stevenkwong/article/details/68489870  "windows下pip报PermissionError解决方案 - CSDN博客"

Keras文檔< https://keras.io/ >


Keras中文文檔< https://keras-cn.readthedocs.io/en/latest/ >


Keras安裝和配置指南(Windows) - Keras中文文檔< https://keras-cn.readthedocs.io/en/latest/for_beginners/keras_windows/ >


最後編輯時間: 2018/1/19
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoiZGF0ZTogJzIwMTgtMDEtMTknXG50YW
dzOiBLZXJhc1xuIiwiaGlzdG9yeSI6WzE1MDczOTMyOTgsLTEw
MTY1OTA1NjUsMTA5MTU0NzExNCwyMTAxNjk0NzUwXX0=
-->