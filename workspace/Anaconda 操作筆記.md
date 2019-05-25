Anaconda 可以用來分離 python 的環境，並且會預先安裝常用的科學運算套件。在做實驗或隔離專案環境時很方便。
[readmore]
**目錄**  
[TOC]
# 安裝 Anaconda
安裝直接到 [Home - Anaconda](https://www.anaconda.com/)，Anaconda 的官網，安裝還忙方便的
# 創建環境
以下列出幾個常用的創見方式
**最簡單的，只有指定虛擬環境的名稱 :**
```shell
conda create -n envName
```

**指定虛擬環境名稱，並預先安裝 python :**
```shell
conda create -n envName python=3.5
```

**指定虛擬環境的安裝位置，以及 python 版本**[^1]，因筆者在 windows 創建時，預設都會創建在 `C:\Users\XXX\AppData\Local\conda\conda\envs\` 底下，但筆者較習慣創建在以下的路徑
```shell
conda create --prefix=C:\ProgramData\Anaconda3\envs\envName python=3.5
```
該資料夾名稱便是虛擬環境名稱，所以就不用(也無法)加上 `-n` 的參數了。
# 參考資料
[[Day01]Anaconda環境安裝！ - iT 邦幫忙::一起幫忙解決難題，拯救 IT 人的一天]([https://ithelp.ithome.com.tw/articles/10192460](https://ithelp.ithome.com.tw/articles/10192460))


[^1]: [Python：Anaconda安装虚拟环境到指定路径 - learn_tech的博客 - CSDN博客]([https://blog.csdn.net/learn_tech/article/details/80748450](https://blog.csdn.net/learn_tech/article/details/80748450))

*最後編輯時間:2019/5/25*

<!--tags:
-->
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5Nzg1MjAxMjMsMTUxMDY2ODU5MiwxNz
AxNTY4MzUzLC0xODY2NDU2MTIxLC04MzQxMjQ4NDFdfQ==
-->