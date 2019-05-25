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

```
projectRoot
├---src
└---docs
```
筆者將原始碼統一放在 `src/` 資料夾下

在 `doc/` 資料夾下執行
```shell
sphinx-quickstart
```
會產生所需檔案與 `conf.py` ，將該檔案內的
```python
# import os
# import sys
# sys.path.insert(0, os.path.abspath('.'))
```
取消註解，並修改為
```python
import os
import sys
sys.path.insert(0, os.path.abspath('../src/'))
```
然後在
```python
extensions = [
]
```
加入 `'sphinx.ext.autodoc'` ，如下所示
```python
extensions = ['sphinx.ext.autodoc']
```
## 引用程式內說明
以 `./src/main.py` 範例
```rst
Crawler Python API
==================

crawler.main
.. automodule:: crawler.main
	:members:
```

# 參考資料


*最後編輯時間:2019/5/24*

<!--tags:
-->
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY0MTg5NjEyMCwtNjc5NDE2Nzk1LDE1OT
ExMjY5NTQsNzU4MDI4OTM1LC0xOTY3NTE2OTgsLTY4MzExNDM3
MiwxNTQxNjMyNTEyLC0yMTE4OTkzMzUxLC02ODA1OTk4MTQsLT
E4MjMwMzkwMTddfQ==
-->