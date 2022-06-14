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
## 1.3 安装terminator  
比原生命令行工具更好用，功能更多。使用下面的命令安装  
```
sudo apt install terminator
```  
卸载使用下面的命令：
```
sudo apt remove terminator
```
## 1.4 安装VScode  
功能强大的IDE，从官网下载，选择.deb X64版本（在ubuntu中使用）在虚拟机中安装。  
然后安装扩展包，包括c++，python和ros。  

# 2. ROS
## 2.1 配置 

