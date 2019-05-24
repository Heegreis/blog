[readmore]
**目錄**  
[TOC]
# 創建環境
以下列出幾個常用的創見方式
**最簡單的，只有指定虛擬環境的名稱**
```shell
conda create -n envName
```

**指定虛擬環境名稱，並預先安裝 python**
```shell
conda create -n envName python=3.5
```

**指定虛擬環境的安裝位置，以及 python 版本**，因筆者在 windows 創建時，預設都會創建在 `C:\Users\XXX\AppData\Local\conda\conda\envs\` 底下，但筆者較習慣創建在以下的路徑
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
[[Day01]Anaconda環境安裝！ - iT 邦幫忙::一起幫忙解決難題，拯救 IT 人的一天]([https://ithelp.ithome.com.tw/articles/10192460](https://ithelp.ithome.com.tw/articles/10192460))



[^1]: [Python：Anaconda安装虚拟环境到指定路径 - learn_tech的博客 - CSDN博客]([https://blog.csdn.net/learn_tech/article/details/80748450](https://blog.csdn.net/learn_tech/article/details/80748450))

*最後編輯時間:2019/5/25*

<!--tags:
-->
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIxMDAwNzkwODQsLTgzNDEyNDg0MV19
-->