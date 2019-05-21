Sphinx 是個用來幫忙在 python 程式中所寫的說明中，自動生成文件的工具。
[readmore]
**目錄**  
[TOC]
# 初始設定
[Getting Started: Overview & Installing Initial Project — Sphinx Tutorial 1.0 documentation](https://sphinx-tutorial.readthedocs.io/start/)

**安裝 Sphinx**
```shell
pip install sphinx
```

可以另外安裝 theme
```shell
pip install sphinx-rtd-theme
```

**設定資料夾結構**
待補
筆者將原始碼統一放在 `src/` 資料夾下

在 `doc/` 資料夾下執行
```shell
sphinx-quickstart
```
會產生所需檔案與 `conf.py` ，將該檔案內的
```python
# import sys
# sys.path.insert(0, os.path.abspath('.'))
```
取消註解，並修改為
```
# import sys
# sys.path.insert(0, os.path.abspath('../src/'))
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
eyJoaXN0b3J5IjpbLTY0ODQ4MzQ2OCwxNTQxNjMyNTEyLC0yMT
E4OTkzMzUxLC02ODA1OTk4MTQsLTE4MjMwMzkwMTddfQ==
-->