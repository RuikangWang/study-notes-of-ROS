# 0. ROS系统学习笔记  
做毕业论文要用到ROS系统，所以这个项目主要记录自己学习使用ROS时遇到的问题和解决方法，有时会写一些心得。主要目的是在遇到相同问题供自己随时查找，省得再去网页搜索。
# 1. VMware虚拟机和Ubuntu 20.04(Focal Fossa)  
## 1.1 安装ubuntu 20.04失败  
安装ubuntu 20.04一直失败，总是提示找不到"Jammy" 这个release，换了多种镜像源一直无法解决。  
应该是这个"Jammy Jellyfish"版本有问题，找到历史版本20.04.4"focal Fossa" 重新安装，问题解决。  
## 1.2 改变界面图标和字体大小  
感觉图标和文字都太小，看着很累，想放大一点。    
使用下列命令安装Tweaks（安装后中文名称为“优化”）。  
```
sudo apt install gnome-tweaks
```
## 1.3 显示和关闭显示隐藏文件  
ctrl+H 显示隐藏文件，再次ctrl+H 关闭显示隐藏文件  
## 1.4 安装terminator  
比原生命令行工具更好用，功能更多。使用下面的命令安装  
```
sudo apt install terminator
```  
卸载使用下面的命令：
```
sudo apt remove terminator
```
## 1.5 安装VScode  
功能强大的IDE，从官网下载，选择.deb X64版本（在ubuntu中使用）在虚拟机中安装。  
然后安装扩展包，包括c++，python和ros。  

# 2. ROS
## 2.1 VScode 配置  
###2.1.1 创建ROS工作空间  
```
mkdir -p xxx_ws/src   //必须得有 src
cd xxx_ws             //进入 xxx_ws目录
catkin_make           // 创建工作空间并编译产生目标文件
```
###2.1.2 启动 vscode  
```
cd xxx_ws
code .        //注意"code"后面一定要有空格！！！
```
然后vscode会启动，然后在vscode 中编译ros  
快捷键 ctrl + shift + B 调用编译，选择:catkin_make:build 点击齿轮符号  
此时会弹出tasks.json文件，将文件内容替换为下列代码  
```
{
// 有关 tasks.json 格式的文档，请参见
    // https://go.microsoft.com/fwlink/?LinkId=733558
    "version": "2.0.0",
    "tasks": [
        {
            "label": "catkin_make:debug", //代表提示的描述性信息
            "type": "shell",  //可以选择shell或者process,如果是shell代码是在shell里面运行一个命令，如果是process代表作为一个进程来运行
            "command": "catkin_make",//这个是我们需要运行的命令
            "args": [],//如果需要在命令后面加一些后缀，可以写在这里，比如-DCATKIN_WHITELIST_PACKAGES=“pac1;pac2”
            "group": {"kind":"build","isDefault":true},
            "presentation": {
                "reveal": "always"//可选always或者silence，代表是否输出信息
            },
            "problemMatcher": "$msCompile"
        }
    ]
}
```
完成后可用ctrl + shift + B 编译看是否报错。  
### 2.1.3 创建 ROS 功能包  
选定 工作空间下的src 右击 ---> create catkin package  
输入自己命名的功能包名，回车，输入所需要的依赖包，比如roscpp rospy std_msgs,回车  
### 2.2.4 创建C++源文件  
然后右键功能包下的src（注意和上一个工作空间下的src区分！）选择新建文件，命名，比如hello_vcode_c。  
输入主要代码，比如想在控制台输出文字“hello”，那么代码为：  
```
#include "ros/ros.h"

int main(int argc, char *argv[])
{
    //执行节点初始化
    //argc：remapping参数的个数
    //argv：remapping参数的列表
    //name：节点名，必须是一个基本名称，不能包含命名空间,此处命名为hello_c
    ros::init(argc,argv,"hello_c");

    //输出日志
    ROS_INFO("hello");
    return 0;
}
```
### 2.1.5 配置 CMakeLists.txt  
打开功能包目录下的CMakeLists.txt文件（可以改成CMake文件格式更容易看）  
找到add_exectable和target_link_libraries开头的两个代码行  
去掉注释符号“#”，修改节点名称，一般和源文件同名即可。  
```
add_executable(节点名称
  src/C++源文件名.cpp
)
target_link_libraries(节点名称
  ${catkin_LIBRARIES}
)
```
可使用ctrl + shift + B 编译看是否报错。  
### 执行 c++文件  
在“终端”下新建窗口，启动ROS核心  
```
roscore
```
再新建终端：
```
source ./devel/setup.bash
```
然后输入：rosrun 功能包名 节点名
```
rosrun hello_vscode hello_vscode_c
```
