---
title: Ubuntu安裝PCL(Point Cloud Library)
date: 2018/9/10
abbrlink: c603fc0f
---
紀錄在Ubuntu 16.04環境下安裝PCL，因筆者目的是要實作點雲的機器學習，故實際操作環境選在Docker的[ufoym/deepo](https://hub.docker.com/r/ufoym/deepo/):all-py36，為DockerHub上的一個機器學習環境包。

並在最後執行官方的簡易程式，測試PCL是否安裝成功。
<!--more-->
# 安裝
## 方式1: 透過PPA安裝(快速安裝)[^1]
### Ubuntu 14
```bash
$ sudo add-apt-repository ppa:v-launchpad-jochen-sprickerhof-de/pcl
$ sudo apt-get update
$ sudo apt-get install libpcl-all
```
### Ubuntu 16 以上[^2]
```bash
$ sudo add-apt-repository ppa:v-launchpad-jochen-sprickerhof-de/pcl
$ sudo apt-get update
$ sudo apt-get install libpcl-dev
```
## 方式2:  自己從source編譯[^3]
### 安裝依賴庫
須先安裝依賴庫，才能成功進行後面的編譯。
在此紀錄2種安裝的方式，但筆者只有試過最後一種方式。
#### 自行安裝
所需依賴庫可參考[官方列表](http://www.pointclouds.org/documentation/tutorials/compiling_pcl_posix.php#id5)。

或是透過以下整理好的指令安裝[^4]
```bash
$ sudo apt-get update
$ sudo apt-get install git build-essential linux-libc-dev
$ sudo apt-get install cmake cmake-gui 
$ sudo apt-get install libusb-1.0-0-dev libusb-dev libudev-dev
$ sudo apt-get install mpi-default-dev openmpi-bin openmpi-common  
$ sudo apt-get install libflann1.8 libflann-dev
$ sudo apt-get install libeigen3-dev
$ sudo apt-get install libboost-all-dev
$ sudo apt-get install libvtk5.10-qt4 libvtk5.10 libvtk5-dev
$ sudo apt-get install libqhull* libgtest-dev
$ sudo apt-get install freeglut3-dev pkg-config
$ sudo apt-get install libxmu-dev libxi-dev 
$ sudo apt-get install mono-complete
$ sudo apt-get install qt-sdk openjdk-8-jdk openjdk-8-jre
```
#### 利用安裝方式1的PPA來獲取依賴庫[^2]
執行安裝方式1後，依賴庫就會安裝完成
但筆者遇到編譯PCL時，遇到錯誤，採用以下指令安裝缺少的套件:[^5]
```bash
$ sudo apt install libproj-dev
```
### 編譯source[^3]
下載pcl的原始碼:
```bash
$ git clone https://github.com/PointCloudLibrary/pcl.git
```

進行編譯流程:
```bash
$ cd pcl && mkdir build && cd build
$ cmake -DCMAKE_BUILD_TYPE=Release ..
$ make -j2
$ sudo make -j2 install
```
# 測試[^6] [^7]
在想要的路徑，例如`~/`建立測試專案資料夾，及其build資料夾:
```bash
~$ mkdir PCL_TUTORAIL
~$ cd PCL_TUTORAIL/
~/PCL_TUTORAIL$ mkdir build
```

新建`pcd_write.cpp`:
```bash
~/PCL_TUTORAIL$ vim pcd_write.cpp
```
在檔案中寫入範例程式碼:
```c++
#include <iostream>
#include <pcl/io/pcd_io.h>
#include <pcl/point_types.h>

int
  main (int argc, char** argv)
{
  pcl::PointCloud<pcl::PointXYZ> cloud;

  // Fill in the cloud data
  cloud.width    = 5;
  cloud.height   = 1;
  cloud.is_dense = false;
  cloud.points.resize (cloud.width * cloud.height);

  for (size_t i = 0; i < cloud.points.size (); ++i)
  {
    cloud.points[i].x = 1024 * rand () / (RAND_MAX + 1.0f);
    cloud.points[i].y = 1024 * rand () / (RAND_MAX + 1.0f);
    cloud.points[i].z = 1024 * rand () / (RAND_MAX + 1.0f);
  }

  pcl::io::savePCDFileASCII ("test_pcd.pcd", cloud);
  std::cerr << "Saved " << cloud.points.size () << " data points to test_pcd.pcd." << std::endl;

  for (size_t i = 0; i < cloud.points.size (); ++i)
    std::cerr << "    " << cloud.points[i].x << " " << cloud.points[i].y << " " << cloud.points[i].z << std::endl;

  return (0);
}
```

新建`CMakeLists.txt`:
```bashl
~/PCL_TUTORAIL$ vim CMakeLists.txt
```
在檔案中寫入範例程式碼:
```
cmake_minimum_required(VERSION 2.8 FATAL_ERROR)

project(pcd_write)

find_package(PCL 1.2 REQUIRED)

include_directories(${PCL_INCLUDE_DIRS})
link_directories(${PCL_LIBRARY_DIRS})
add_definitions(${PCL_DEFINITIONS})

add_executable (pcd_write pcd_write.cpp)
target_link_libraries (pcd_write ${PCL_LIBRARIES})
```

到`build`資料夾cmake出所需的檔案:
```bash
~/PCL_TUTORAIL$ cd build
~/PCL_TUTORAIL/build$ cmake ..
```
執行成功就會產出`CMakeCache.txt`、`CMakeFiles`、`cmake_install.cmake`、`Makefile` 檔案。

make出執行檔:
```bash
~/PCL_TUTORAIL/build$ make
```
若成功會產出`pcd_write`檔。

執行`pcd_write`，以測試是否安裝成功:
```bash
~/PCL_TUTORAIL/build$ ./pcd_write
```
若成功會顯示以下輸出:
```
Saved 5 data points to test_pcd.pcd.
  0.352222 -0.151883 -0.106395
  -0.397406 -0.473106 0.292602
  -0.731898 0.667105 0.441304
  -0.734766 0.854581 -0.0361733
  -0.4607 -0.277468 -0.916762
```
# 參考資料
[^1]:[Prebuilt binaries for Linux - Point Cloud Library (PCL)](http://pointclouds.org/downloads/linux.html)

[^2]:[ubuntu下的PCL安装过程 - CSDN博客:](https://blog.csdn.net/mush_room/article/details/78339578)

[^3]:[Compiling PCL from source on POSIX compliant systems — PCL 0.0 documentation](http://www.pointclouds.org/documentation/tutorials/compiling_pcl_posix.php)

[^4]:[PCL1.8+Ubuntu16.04安装详解 - CSDN博客](https://blog.csdn.net/dantengc/article/details/78446600)

[^5]:[c++ - Compiling PCL 1.7 on Ubuntu 16.04 , errors in CMake generated Makefile - Stack Overflow](https://stackoverflow.com/questions/37369369/compiling-pcl-1-7-on-ubuntu-16-04-errors-in-cmake-generated-makefile)

[^6]:[# Install and Use Point Cloud Libray in Linux for Beginners - YouTube](https://www.youtube.com/watch?v=5lU6RiS4pfE)

[^7]:[Using PCL in your own project - Documentation - Point Cloud Library (PCL)](http://pointclouds.org/documentation/tutorials/using_pcl_pcl_config.php)

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3OTA0MDk1NjUsMTgwNTY3MDk2MSwtNT
gzNjE0MTU5XX0=
-->