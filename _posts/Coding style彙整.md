---
title: Coding style彙整
date: 2018/6/2
updated: 2018/6/2
tags:
  - tag1
  - tag2
abbrlink: 
description: 整理各語言與編輯器，筆者所使用的Coding style工具
---
整理各語言與編輯器，筆者所使用的Coding style工具
<!--more-->
# Visual Studio Code

## Python
安裝Python擴充功能(ms-python.python)
預設是開啟Pylint，若無效，可能是沒有安裝Pylint，可使用`pip3`進行安裝。
(筆者的電腦不知道是哪裡裝來Pylint的)

在Python上，除了Pylint(較厚重，但檢查較詳細)，還有flake8，只做單檔檢查，速度非常快。[^1]
(筆者只有使用過預設的Pylint)

# Visual Studio 2017
從2017版預設包含了Coding style(程式碼規範)的工具，甚至可以自動提供程式碼建議。[^2]
VS支援的語言眾多，以下列出筆者有在VS 2017使用的語言。

## C#

# Google 開源專案風格指南
這並非是工具，只是規則文件，目前筆者未細看。
官方版:[GitHub - google/styleguide: Style guides for Google-originated open-source projects](https://github.com/google/styleguide)
簡中翻譯版:[GitHub - zh-google-styleguide/zh-google-styleguide: Google 开源项目风格指南 (中文版)](https://github.com/zh-google-styleguide/zh-google-styleguide)
繁中翻譯版:[GitHub - welkineins/tw-google-styleguide: Google 開源專案風格指南 (繁體中文版)](https://github.com/welkineins/tw-google-styleguide)

## 包含的程式語言
- C++
- Objective-C Style Guide
- Java
- Python
- R
- Shell
- HTML/CSS
- JavaScript
- AngularJS
- Common Lisp
- Vimscript

# 參考資料
[^1]:[Python coding style 1: 基本概念 & linter – ianlini](https://ianliniblog.wordpress.com/2017/05/03/python-coding-style-1-%E5%9F%BA%E6%9C%AC%E6%A6%82%E5%BF%B5-linter/)
[^2]:[Visual Studio 2017 第一眼的改變 - demo小鋪](https://demo.tc/post/834)]