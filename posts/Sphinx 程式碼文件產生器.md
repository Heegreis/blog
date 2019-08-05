Sphinx 是個用來幫忙在 python 程式中所寫的說明中，自動生成文件的工具。
[readmore]
**目錄**  
[TOC]
# 初始設定
**安裝 Sphinx**
```shell
pip install sphinx
```

可以另外安裝 theme
```shell
pip install sphinx-rtd-theme
```

**設定資料夾結構**
其實也可以不設定，這邊是要分離文件跟原始碼所做的處理
```txt
projectRoot
├---src
└---docs
```
筆者將原始碼統一放在 `src/` 資料夾下

在 `doc/` 資料夾下執行
```shell
sphinx-quickstart
```
然後會有一連串的設定選項要選，但筆者也還沒很了解這些設定，以後有機會再補充。  
就會產生所需檔案與 `conf.py` ，將該檔案內的
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
# autodoc
這個功能可以引用程式內的註解說明(docstring)，但 Sphinx 有指定的格式[^1]。  
若是像筆者習慣使用 vscode ，可以使用 autoDocstring 這個擴充功能，並設定為 Sphinx 的格式。就可以快速插入 docstring 了。

以 `src/subFunc/main.py` 為例，在 `docs/` 的任一 `.rst` 檔加入以下語法，就會引用該程式碼裡所寫的說明
```rst
.. automodule:: subFunc.main
	:members:
```
# 檢視結果
可以使用 SimpleHTTPServer 建立簡易的網頁伺服器[^2]  
在要
```shell
python -m SimpleHTTPServer
```
# 參考資料
[Getting Started: Overview & Installing Initial Project — Sphinx Tutorial 1.0 documentation](https://sphinx-tutorial.readthedocs.io/start/)

[^1]:[飘逸的python - 代码即文档docstring - mattkang - CSDN博客](https://blog.csdn.net/handsomekang/article/details/46830083)

[^2]:[用 Python 的 SimpleHTTPServer 模組快速建立一個臨時網頁伺服器（Web Server） - G. T. Wang](https://blog.gtwang.org/web-development/python-simplehttpserver-web-server/)

*最後編輯時間:2019/5/25*

<!--tags:
docstring, python, Sphinx
-->
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoidGFnczogJ2RvY3N0cmluZywgcHl0aG
9uLCBTcGhpbngnXG4iLCJoaXN0b3J5IjpbLTEyNTMzOTY4MTAs
OTA0NzUxOTA3LC04ODIzMDExNyw1NDk4MDczNjgsLTY3OTQxNj
c5NSwxNTkxMTI2OTU0LDc1ODAyODkzNSwtMTk2NzUxNjk4LC02
ODMxMTQzNzJdfQ==
-->