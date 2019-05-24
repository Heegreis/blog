[readmore]
**目錄**  
[TOC]
# 創建環境
以下列出幾個常用的創見方式
最簡單的，只有指定虛擬環境的名稱
```shell
conda create -n envName
```

指定虛擬環境名稱，並預先安裝 python
```shell
conda create -n envName python=3.5
```

指定虛擬環境的安裝位置，以及 python 版本，因筆者在 windows 創建時，預設都會創建在
```shell
conda create --prefix=C:\ProgramData\Anaconda3\envs\envName python=3.5
```
## 標題二
連結說明: <https://developer.nvidia.com/cuda-80-ga2-download-archive>

`行內程式碼`

```shell
區塊程式碼
```

引用對照 [^1]。

# 參考資料
[Installing TensorFlow on Windows | TensorFlow](https://www.tensorflow.org/install/install_windows)

[^1]: [被引用連結說明:](http://tieba.baidu.com/p/4565248851)

*最後編輯時間:2018/5/10*

<!--tags:
-->
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjM0MDgyODU2XX0=
-->