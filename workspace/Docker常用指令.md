簡單紀錄一些docker的指令
[readmore]
**目錄**
[TOC]
# 本機映像檔
以下指令中 `the_image` 代表所要操作的映像檔，請自行替換。

下載映像檔 `docker pull`，不加tag會下載最新版
```shell
$ sudo docker pull the_image
```
加上tag，以下指令的`the_tag`代表tag名稱，請自行替換。
```shell
$ sudo docker pull the_image:the_tag
```
查看本機已有的映像檔 `docker images`
```shell
$ sudo docker images
```

# 容器
以下指令中 `the_container` 代表所要操作的容器，請自行替換。

新建執行中的容器 `docker run`:
```shell
$ sudo docker run --name the_container -it the_image
```

查看執行中的容器 `docker ps`:
```shell
$ sudo docker ps
```

查看全部的容器 `docker ps -a:`
```shell
$ sudo docker ps -a
```

終止容器 `docker stop`:
```shell
$ sudo docker stop the_container
```

啟動終止狀態的容器 `docker start`:
```shell
$ sudo docker start the_container
```

刪除容器 `docker rm`:
```shell
$ sudo docker rm the_container
```

進入容器 `docker exec`:
```shell
$ sudo docker exec -it the_container bash
```

按下 `ctrl` + `P` 然後 `ctrl` + `Q` 跳離容器，讓它繼續在背景執行。

在容器與本機之間傳送檔案 `docker cp`:
容器ID加上":"後面接檔案位置，前面路徑的檔案複製到後面路徑
```shell
$ sudo docker cp d8f7c83ba660:/data/file /data/file
$ sudo docker cp /data/file d8f7c83ba660:/data/file
```
# Volume
清除未被使用的volume[^1]
``` shell
$ sudo docker volume prune
```

# Docker Compose
啟動
```shell
$ sudo docker-compose up -d
```
停止
```shell
$ sudo docker-compose stop
```
停止加上移除容器
```shell
$ sudo docker-compose down
```

# 參考資料
[前言 · 《Docker —— 從入門到實踐­》正體中文版](https://philipzheng.gitbooks.io/docker_practice/content/)
[Docker容器和主机如何互相拷贝传输文件 – 峰云就她了](http://xiaorui.cc/2015/04/12/docker容器和主机如何互相拷贝传输文件/)
[^1]:[清理Docker的container，image与volume · 零壹軒·笔记](http://note.qidong.name/2017/06/26/docker-clean/)

*最後修改時間:2019/1/25*
<!--stackedit_data:
eyJwcm9wZXJ0aWVzIjoiZGF0ZTogJzIwMTktMDEtMjUnXG50YW
dzOiBEb2NrZXJcbiIsImhpc3RvcnkiOlsxMTE5NTI2MjA2XX0=

-->