

## 动手前的准备

- 准备一个至少16G容量的U盘
- 获取虚拟机（MWare Workstation）
- 获取Windows 7 镜像(MSDN I tell you)
- 获取PE(微pe)
- 获取系统补丁（IT天空）
- 获取运行库（3DM游戏运行库）
- 获取美化工具（软媒魔方）
- 获取常用软件（7-Zip\WPS\手心输入法）
- 获取激活工具（Windows Loader）
- 获取封装工具和驱动程序（sysceo）





## 配置虚拟机并给虚拟机装系统

1. 虚拟机配置如下

![image-20200705201107300](D:\myBlogs\docs\Windows\image-20200705201107300.png)

2. 进入BIOS

![image-20200705201219720](D:\myBlogs\docs\Windows\image-20200705201219720.png)

3. 调整为光驱启动

![image-20200705201355810](D:\myBlogs\docs\Windows\image-20200705201355810.png)

4. 光驱启动，分配31G的C盘和29G的D盘，C盘安装操作系统

![image-20200705201910644](D:\myBlogs\docs\Windows\image-20200705201910644.png)

5. 重启后进入如下OOBE模式

![image-20200705202303067](D:\myBlogs\docs\Windows\image-20200705202303067.png)

6. Ctrl+Shift+F3，重启，跳过OOBE模式，使用Administrator进入sysprep系统准备模式

![image-20200705202604163](D:\myBlogs\docs\Windows\image-20200705202604163.png)

## 调整系统设置

- 调整桌面图标

增加计算机图标

![image-20200705202948401](D:\myBlogs\docs\Windows\image-20200705202948401.png)

- 调整视觉效果

个性化中开启Windows 特效

![image-20200705203204308](D:\myBlogs\docs\Windows\image-20200705203204308.png)

高级设置中开启特效

![image-20200705203330267](D:\myBlogs\docs\Windows\image-20200705203330267.png)

- 关闭自动播放

在组策略中管别自动播放

![image-20200705204431989](D:\myBlogs\docs\Windows\image-20200705204431989.png)

- 关闭操作中心

控制面板中关闭操作中心通知

![image-20200705203602115](D:\myBlogs\docs\Windows\image-20200705203602115.png)

同时关闭通知区域图标

![image-20200705203759420](D:\myBlogs\docs\Windows\image-20200705203759420.png)

- 关闭Windows Update

![image-20200705203958021](D:\myBlogs\docs\Windows\image-20200705203958021.png)

其他组策略的操作需要在这儿处理

## 封装前的部署

1. 将需要的软件放进虚拟机

使用仅主机专用网络共享实现文件传递。

2. 安装系统补丁

#### 利用360安装补丁

- 克隆操作系统镜像
- 链接internet 网络
- 安装360安全卫士
- 调整补丁部署位置，并且不清除补丁

![image-20200710115246884](D:\myBlogs\docs\Windows\image-20200710115246884.png)

- 进行补丁扫描和下载.NET Framework的相关漏洞

![image-20200710115612899](D:\myBlogs\docs\Windows\image-20200710115612899.png)

- 拷贝补丁库文件至离线操作系统环境
- 管理员命令行执行如下命令：

```powershell
@echo off 
rem for %%i in (*.exe) do %%i /passive /norestart /nobackup
for %%i in (*.cab) do dism /online /NoRestart /add-package /packagepath:%%i
```



3. 安装运行库

安装了所有的VC++运行库和所有的.net framework 版本

![image-20200705220537689](D:\myBlogs\docs\Windows\image-20200705220537689.png)

![image-20200705220740330](D:\myBlogs\docs\Windows\image-20200705220740330.png)

Microsoft Vistual C++ 安装至2019版本

.NET Framework 安装至4.5.2版本

4. 安装常用软件

WPS

- 关闭自带浏览器

![image-20200710113610523](D:\myBlogs\docs\Windows\image-20200710113610523.png)

- 关闭自动升级

![image-20200710113339951](D:\myBlogs\docs\Windows\image-20200710113339951.png)

- 关闭信息推送

![image-20200710113437128](D:\myBlogs\docs\Windows\image-20200710113437128.png)

- 清理wps网盘入口

右键清理WPS网盘图标——》启动办公助手——》开启“在我的电脑显示WPS网盘入口”，然后关闭，即可去掉图标



edge

- 设置从上次关闭处打开

![image-20200710114341497](D:\myBlogs\docs\Windows\image-20200710114341497.png)

手心输入法

7-Zip

## 优化设置

1. 美化你的系统
   - 设置壁纸
   
   使用软媒美化大师visualmaster进行编辑，开启为桌面和资源管理器建立不懂的进程
   
   ![image-20200706104752605](D:\myBlogs\docs\Windows\image-20200706104752605.png)
   
   - 添加“运行”到开始菜单
   
   ![image-20200706105000271](D:\myBlogs\docs\Windows\image-20200706105000271.png)
   
   - 修改开机提示文字
   
   开机动画——》修改开机文字
   
   ![image-20200706105227585](D:\myBlogs\docs\Windows\image-20200706105227585.png)
   
   - 设置登录界面壁纸
   
   ![image-20200706110244227](D:\myBlogs\docs\Windows\image-20200706110244227.png)
   
   - 设置OEM信息
   
   ![image-20200706112559849](D:\myBlogs\docs\Windows\image-20200706112559849.png)
   
2. 系统设置优化

资源管理器自动刷新

在资源管理器中显示菜单栏

![image-20200706113015100](D:\myBlogs\docs\Windows\image-20200706113015100.png)

禁用错误报告

![image-20200706113158515](D:\myBlogs\docs\Windows\image-20200706113158515.png)

关机设置

![image-20200706113303890](D:\myBlogs\docs\Windows\image-20200706113303890.png)



![image-20200710140457733](D:\myBlogs\docs\Windows\image-20200710140457733.png)



![image-20200710140354161](D:\myBlogs\docs\Windows\image-20200710140354161.png)



![image-20200710140430391](D:\myBlogs\docs\Windows\image-20200710140430391.png)



![image-20200710140558164](D:\myBlogs\docs\Windows\image-20200710140558164.png)

![image-20200710140733575](D:\myBlogs\docs\Windows\image-20200710140733575.png)

![image-20200710140818799](D:\myBlogs\docs\Windows\image-20200710140818799.png)

1. 清理垃圾并减少系统体积

使用cleanmaster，清理垃圾

![image-20200706114853881](D:\myBlogs\docs\Windows\image-20200706114853881.png)

关闭操作系统

使用PE引导进入

![image-20200706115813425](D:\myBlogs\docs\Windows\image-20200706115813425.png)

1. 在开始封装前先备份你的系统

使用CGI备份还原工具，本分系统分区

![image-20200706133911698](D:\myBlogs\docs\Windows\image-20200706133911698.png)

## 正式封装

准备：在C盘创建文件家sysprep，将驱动程序、激活工具放置在该文件夹内

建立压缩包关联关系

拷贝aida64至Windows文件夹下

拷贝驱动至sysprep下

拷贝Windows Loader至sysprep下







1. 使用sysceo封装系统

启动sysceo工具设置目标系统

![image-20200706135829303](D:\myBlogs\docs\Windows\image-20200706135829303.png)

设置部署过程

![image-20200706140635068](D:\myBlogs\docs\Windows\image-20200706140635068.png)

1. 部署驱动的自动安装

计划任务中添加——》部署中——》添加驱动程序安装

![image-20200706142156637](D:\myBlogs\docs\Windows\image-20200706142156637.png)



1. 激活工具的使用方式
2. 打包你的系统

系统封装

![image-20200706142536490](D:\myBlogs\docs\Windows\image-20200706142536490.png)

启用PE进入桌面，打包分区





## 安装系统到另一台电脑





##  问题

1. 有蓝牙的驱动信息
2. 有U盘信息

不使用USB，仅使用主机模式连接虚拟机，参考资料：https://jingyan.baidu.com/article/0aa223759c5793c9cd0d6472.html

共享主机文件夹至虚拟机，出现问题，参考资料：**https://jingyan.baidu.com/article/08b6a59191875f14a809228a.html**

1. 制造商图片尺寸（120x120大小的bmp图片）
2. 安装图片（）
3. 关机图片（1920*1080）
4. 正在启动华中光电专属Windows，需要确认
5. WPS有网盘图标

使用WPS助手进行清除



李家伟

- 需要获取硬盘序列号
- 设置IP地址192.168.20.111-120
- 删除IE64位版本的链接

- 睡眠模式从不



范收平

- 尽快进行安全产品适配性测试



初始化操作

- 进去后对edge，再进行一波操作。
- 7z建立关联关系
- aida64拷贝

张珂相

- 锁屏界面设计——陈璇



将默认浏览器换成chrome 49版本

压缩软件关联zip、rar格式

恢复默认锁屏界面





###  使用Windows 7 x64test为基础进行测试





1. 卸载edge，安装chrome 49
2. 删除所有程序中不用的快捷方式

![image-20200716183851395](D:\myBlogs\docs\layui\image-20200716183851395.png)

3. 关联7z的rar格式
4. 精简开始菜单

![image-20200716184221166](D:\myBlogs\docs\layui\image-20200716184221166.png)

5. 修改登录画面和系统属性
6. 