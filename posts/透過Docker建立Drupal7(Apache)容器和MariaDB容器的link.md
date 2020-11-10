---
title: 透過Docker建立Drupal7(Apache)容器和MariaDB容器的link
date: 2018/1/31
abbrlink: 613b126e
---
紀錄在Docker中建立Drupal7的container(容器)，以及MariaDB的container(容器)，並連接這兩個容器 ，讓Drupal實際可使用的兩種建立方式。

個別建立兩個容器

用 Docker Compose 一次建立2個容器與設定
<!--more-->
# 共同步驟

## Pull(下載)image(映像檔)

Pull Drupal:7.56 和 MariaDB:10.2.7
```bash
$ docker pull mariadb:10.2.7
$ docker pull drupal:7.56
```

# 個別建立2個容器

建立MariaDB容器
```bash
$ docker run --name  mariadbContainerName -e MYSQL_ROOT_PASSWORD=myPassword -d mariadb:10.2.7
```
其中，  `mariadbContainerName` 是所要建立的容器 name ； `myPassword` 是所要設定的 Root 密碼。

## 透過 MySQL command line client 連結到 MariaDB，並建立資料庫與使用者

連結資料庫，完成後即可輸入 MySQL 指令
```bash
$ docker run -it --link mariadbContainerName:mysql --rm mariadb:10.2.7 sh -c 'exec mysql -h"$MYSQL_PORT_3306_TCP_ADDR" -p"$MYSQL_PORT_3306_TCP_PORT" -uroot -p"$MYSQL_ENV_MYSQL_ROOT_PASSWORD"'
```
其中， `mariadb:10.2.7` 若沒有指定版本，會使用latest版。

建立給 Drupal 用的資料庫
```bash
> create database drupalDatabaseName;
```
其中， `drupalDatabaseName` 是資料庫的名稱。

建立使用者
```bash
> create user username@'%' identified by 'userPassword';
```
其中， `username` 是要建立的使用者名稱； `userPassword` 是使用者的密碼。

設定資料庫權限
```bash
> grant all privileges on drupalDatabaseName.* to username@'%';
```

離開MariaDB
```bash
> exit
```

## 建立Drupal容器，並且與MariaDB容器連接

建立Drupal容器
```bash
$ docker run --name drupalContainerName -p 80:80 --link  mariadbContainerName:mariadbNickname -d drupal:7.56
```
其中， `drupalContainerName ` 是所要建立的容器 name，並且將主機的 80port 指到這個容器的 80port；`mariadbNickname` 作為 MariaDB 的別名，讓我們在建立Drupal網站時，以此代表資料庫的IP 。

安裝Drupal
進到瀏覽器的drupal安裝畫面，在 Set up database 步驟裡的 ADVANCED OPTIONS 底下的 Database host 欄位輸入 `mariadbNickname` 。

# 用 Docker Compose 一次建立2個容器與設定

## 安裝 Docker Compose

安裝指令
```bash
$ curl -L "https://github.com/docker/compose/releases/download/1.10.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

安裝完畢之後給予 Docker Compose 一定的執行權限
```bash
$ chmod +x /usr/local/bin/docker-compose
```

可透過 `docker-compose --version` 檢查版本
```bash
$ docker-compose --version
docker-compose version 1.15.0, build e12f3b9
```

## 建立 Compose 檔案

建議先建立存放檔案的資料夾
```bash
$ mkdir my_drupal
$ cd mydrupal
```
檔案名稱自行設定。

在資料夾裡建立一個 `docker-compose.yml` 檔案，以包含 MariaDB 和 Drupal 兩個容器
內容如下:
```yaml
# Drupal with MariaDB

version: '2'

services:

  drupal8:
    image: drupal:8.3.6
    ports:
      - "80:80"
    volumes:
      - /var/www/html/modules
      - /var/www/html/profiles
      - /var/www/html/themes
      - /var/www/html/sites
    restart: always
    links:
      - mariadb

  mariadb_10_2_7:
    image: mariadb:10.2.7
    volumes:
      - /var/lib/mysql
    environment:
      MYSQL_ROOT_PASSWORD: eb202
      MYSQL_DATABASE: drupal
      MYSQL_USER: brian
      MYSQL_PASSWORD: eb202
    restart: always
```
**附註:** volumes 的部分可再調整周密

## 透過 Compose 啟動服務

在同個目錄下透過 docker-compose up -d 就能夠以剛才建立的設定檔啟動那兩個容器。
```bash
$ docker-compose up -d
```

## 建立透過 MySQL command line client 連結到 MariaDB (compose 版)

以 docker compose 建立容器時會為其創建一個默認網路 `containerName_defaul`，造成網路隔離。

查詢 docker network
```bash
$ docker network ls
```

mariadb 連接 mysql 的指令
```bash
$ docker run -it --net drupal8_default --link drupal8_mariadb_10_2_7_1:mysql --rm mariadb:10.2.7 sh -c 'exec mysql -h"$MYSQL_PORT_3306_TCP_ADDR" mariadb_10_2_7 -p"$MYSQL_PORT_3306_TCP_PORT" -uroot -p"$MYSQL_ENV_MYSQL_ROOT_PASSWORD"'
```
其中 `containerName_default` 為查詢到的 network name ； `mariadb_10_2_7` 為 compose 設定檔裡 MariaDB 的 container name。

# 參考資料

Docker —— 從入門到實踐
<https://philipzheng.gitbooks.io/docker_practice/content/container/enter.html>

今天開始Drupal環境就用Docker Container來建立
<https://blog.hellosanta.com.tw/網站設計/伺服器/今天開始drupal環境就用docker-container來建立>

MariaDB | Docker Documentation
<https://docs.docker.com/samples/mariadb>

Docker-Compose將Drupal網站跟環境設定一次搞定
<https://blog.hellosanta.com.tw/網站設計/伺服器/docker-compose將drupal網站跟環境設定一次搞定>

在 Ubuntu 安裝 Docker 和 Docker Compose
<https://yami.io/ubuntu-docker/>

Drupal | Docker Documentation
<https://docs.docker.com/samples/drupal/#-via-docker-compose>

Maxkit: Docker Compose 初步閱讀與學習記錄
<http://blog.maxkit.com.tw/2017/03/docker-compose.html>

MYSQL_DATABASE does not create database #68
<https://github.com/docker-library/mariadb/issues/68>
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExMjY3ODU0NjUsOTk1MDIwMDczLC0xND
EzNTE1ODM5XX0=
-->