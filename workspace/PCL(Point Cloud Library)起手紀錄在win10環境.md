紀錄在win10環境中安裝PCL，並記錄一些常用PCL功能程式碼。
[readmore]
**目錄**
[TOC]
# 安裝
## cmake
官方下載連結:
[Download | CMake](https://cmake.org/download/)
筆者選擇[cmake-3.11.3-win64-x64.msi](https://cmake.org/files/v3.11/cmake-3.11.3-win64-x64.msi)進行快速安裝
過程中選擇加入Path[^1]
## PCL
**PCL-AllInOne**下載: 
[Releases · PointCloudLibrary/pcl · GitHub](https://github.com/PointCloudLibrary/pcl/releases)
筆者下載的是: [**PCL-1.8.1-AllInOne-msvc2017-win64.exe**](https://github.com/PointCloudLibrary/pcl/releases/download/pcl-1.8.1/PCL-1.8.1-AllInOne-msvc2017-win64.exe)
因筆者使用的是Visual Studio 2017。
安裝過程中，筆者有選擇安裝第三方插件。

安裝完成後在環境變數的系統變數中加入以下變數[^2]
|變數名稱|變數|
|--|--|
|PCL_ROOT|C:\Program Files\PCL 1.8.1|
|Path|;%PCL_ROOT%\bin;%PCL_ROOT%\3rdParty\VTK\bin|
PCL_ROOT 請改為自己的安裝路徑。

修改完環境變數後，請重新開機，以套用變更。
否則之後在建置方案時，可能會跳出找不到.dll檔。[^3]
有時，設定完一次，還有可能還是會出現一樣狀況。
則確認環境變數後，再次重開機即可。
# 建立專案檔
## 建立必要檔案
新增一個資料夾，裡面需包含CMakeLists.txt、main.cpp[^4]
CMakeLists.txt的內容如下:
```
cmake_minimum_required( VERSION 2.8 )
 
# Create Project
project( solution )
add_executable( project main.cpp )
set_property( DIRECTORY PROPERTY VS_STARTUP_PROJECT "project" )
 
# Find Packages
find_package( PCL 1.8 REQUIRED )
 
if( PCL_FOUND )
  # Additional Include Directories
  # [C/C++]>[General]>[Additional Include Directories]
  include_directories( ${PCL_INCLUDE_DIRS} )
 
  # Preprocessor Definitions
  # [C/C++]>[Preprocessor]>[Preprocessor Definitions]
  add_definitions( ${PCL_DEFINITIONS} )
  #add_definitions( -DPCL_NO_PRECOMPILE )
 
  # Additional Library Directories
  # [Linker]>[General]>[Additional Library Directories]
  link_directories( ${PCL_LIBRARY_DIRS} )
 
  # Additional Dependencies
  # [Linker]>[Input]>[Additional Dependencies]
  target_link_libraries( project ${PCL_LIBRARIES} )
endif()
```
其中`solution`，為方案名稱；`project`，為專案名稱，可替換為所需的名稱。

main.cpp的內容如下:[^5]
```c++
#include <iostream>
int main( int argc, char* argv[] )
{
	return 0;
}
```
## CMake出專案檔
開啟CMake，sourse code資料夾即為剛剛所建立的資料夾。build資料夾，則選擇要生成的位置。
設定完資料夾後即可按下Configure按鈕，顯示Configuring done完成後按下Generate按鈕。[^6]
![設定完資料夾後即可按下Configure按鈕，完成後按下Generate按鈕](https://lh3.googleusercontent.com/G2Vcr1GL0N8pwssrF2wEdmR1XcVcjP_4EplJrRnOzkbaPjR5TLO2vPnOhc-l1Mtfc7eXCo84PLgC)
建立完專案檔後，即可在build的資料夾找到.sln檔，開啟後即可開始使用PCL囉。
# 基本操作範例程式
## 將點雲資料寫入pcd檔
範例程式:[^7]
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
此程式碼會在專案資料夾中生成名為test_pcd.pcd的點雲資料檔，包含一些點雲資料。
可使用[CloudCompare](http://www.danielgm.net/cc/)開啟此類.pcd檔案。
## 將pcd檔轉為ply檔
[MeshLab](http://www.meshlab.net/)是常用的觀看3D格式檔案的軟體，但此軟體卻無法開啟pcd檔，故以下介紹轉換的程式碼:[^8]
```c++
#include <pcl/io/pcd_io.h>
#include <pcl/io/ply_io.h>
#include<pcl/PCLPointCloud2.h>
#include<iostream>
#include<string>

using namespace pcl;
using namespace pcl::io;
using namespace std;

int PCDtoPLYconvertor(string & input_filename, string& output_filename)
{
	pcl::PCLPointCloud2 cloud;
	if (loadPCDFile(input_filename, cloud) < 0)
	{
		cout << "Error: cannot load the PCD file!!!" << endl;
		return -1;
	}
	PLYWriter writer;
	writer.write(output_filename, cloud, Eigen::Vector4f::Zero(), Eigen::Quaternionf::Identity(), true, true);
	return 0;

}

int main()
{
	string input_filename = "test_pcd.pcd";
	string output_filename = ".//result//cloud_ply.ply";
	PCDtoPLYconvertor(input_filename, output_filename);
	return 0;
}
```
資料路徑部分，生成檔案的資料夾位置，必須先行自行新增。

筆者在第一次執行時遇上以下錯誤:
錯誤 C1041 無法開啟程式資料庫 'XXX\build\project.dir\Debug\vc141.pdb'; 如果要將多個 CL.EXE 寫到同一個 .PDB 檔案，請使用 /FS project c:\users\brianliu\desktop\files\plcfile\test\main.cpp.cpp 1

**處理方式**:[^9]
對方案總管中的專案名稱點擊右鍵，點選**屬性**
1. C/C++ > 一般 > 偵錯資訊格式: 改為 C7 相容(/Z7)
2. C/C++ > 程式碼產生 > 啟用字串共用: 改為 是 (/GF)
## 透過PCL可視化點雲資料
透過官方文件的介紹，可視化pcd檔的點雲資料:[^10]
```c++
#include <pcl/visualization/cloud_viewer.h>
#include <iostream>
#include <pcl/io/io.h>
#include <pcl/io/pcd_io.h>
    
int user_data;
    
void 
viewerOneOff (pcl::visualization::PCLVisualizer& viewer)
{
    viewer.setBackgroundColor (1.0, 0.5, 1.0);
    pcl::PointXYZ o;
    o.x = 1.0;
    o.y = 0;
    o.z = 0;
    viewer.addSphere (o, 0.25, "sphere", 0);
    std::cout << "i only run once" << std::endl;
    
}
    
void 
viewerPsycho (pcl::visualization::PCLVisualizer& viewer)
{
    static unsigned count = 0;
    std::stringstream ss;
    ss << "Once per viewer loop: " << count++;
    viewer.removeShape ("text", 0);
    viewer.addText (ss.str(), 200, 300, "text", 0);
    
    //FIXME: possible race condition here:
    user_data++;
}
    
int 
main ()
{
    pcl::PointCloud<pcl::PointXYZRGBA>::Ptr cloud (new pcl::PointCloud<pcl::PointXYZRGBA>);
    pcl::io::loadPCDFile ("my_point_cloud.pcd", *cloud);
    
    pcl::visualization::CloudViewer viewer("Cloud Viewer");
    
    //blocks until the cloud is actually rendered
    viewer.showCloud(cloud);
    
    //use the following functions to get access to the underlying more advanced/powerful
    //PCLVisualizer
    
    //This will only get called once
    viewer.runOnVisualizationThreadOnce (viewerOneOff);
    
    //This will get called once per visualization iteration
    viewer.runOnVisualizationThread (viewerPsycho);
    while (!viewer.wasStopped ())
    {
    //you can also do cool processing here
    //FIXME: Note that this is running in a separate thread from viewerPsycho
    //and you should guard against race conditions yourself...
    user_data++;
    }
    return 0;
}
```
以上的程式碼是用來讀取RGBA資料的點雲，若是其他格式，請更改此行程式碼:[^11]
`pcl::PointCloud<pcl::PointXYZRGBA>::Ptr cloud(new pcl::PointCloud<pcl::PointXYZRGBA>);`
讀取RGB:
`pcl::PointCloud<pcl::PointXYZRGB>::Ptr cloud(new pcl::PointCloud<pcl::PointXYZRGB>);`
讀取單純XYZ:
`pcl::PointCloud<pcl::PointXYZ>::Ptr cloud(new pcl::PointCloud<pcl::PointXYZ>);`
# **參考資料**
[Documentation - Point Cloud Library (PCL)](http://pointclouds.org/documentation/tutorials/using_pcl_pcl_config.php)

[^1]: [Windows上使用CMake | gclxry](http://gclxry.com/use-cmake-on-windows/)
[^2]:[PCL 1.7.2 All-in-one Installer MSVC2012 x64 - CSDN博客](https://blog.csdn.net/bizer_csdn/article/details/51707710)
[^3]:[计算机中丢失pcl_common_debug.dll - CSDN博客](https://blog.csdn.net/xueyuediana/article/details/39637775)
[^4]:[Point Cloud Library 1.8.0 has been released – Summary?Blog](http://unanancyowen.com/en/pcl18/)
[^5]:[Basic CMakeLists for PCL · GitHub](https://gist.github.com/UnaNancyOwen/f4dcd74ab870a0fc9e7a)
[^6]:[Windows上使用CMake | gclxry](http://gclxry.com/use-cmake-on-windows/)
[^7]:[Writing Point Cloud data to PCD files — PCL 0.0 documentation](http://pointclouds.org/documentation/tutorials/writing_pcd.php#writing-pcd)
[^8]:[点云pcd格式转换成ply格式 - CSDN博客](https://blog.csdn.net/xs1997/article/details/78022651)
[^9]:[error C1041: 无法打开程序数据库“xxx\vc140.pdb”；如果要将多个 CL.EXE 写入同一个 .PDB 文件，请使用 - CSDN博客](https://blog.csdn.net/m0_37876745/article/details/78172846)
[^10]:[The CloudViewer — PCL 0.0 documentation](http://pointclouds.org/documentation/tutorials/cloud_viewer.php#cloud-viewer)
[^11]:[Point Cloud Library (PCL) Users mailing list - Failed to find a field named: 'rgba'. Cannot convert message to PCL type.](http://www.pcl-users.org/Failed-to-find-a-field-named-rgba-Cannot-convert-message-to-PCL-type-td3914066.html)

*最後編輯時間:2018/6/23*
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExNjAzOTk4N119
-->