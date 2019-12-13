# Eclipse插件开发笔记

## Eclipse IDE环境篇

### 1.1.1    安装及使用eclipse IDE 

运行eclipse IDE前需要先安装Java运行环境（JRE）[jdkx6417.zip](https://pan.baidu.com/s/1zA4bai3tLlDNLPcTRzBwsA) 提取码: yxf6。在eclipse网站`http://www.eclipse.org/downloads/` 下载eclipse IDE[eclipse-jee-indigo-SR2-win32-x86_64.zip](https://pan.baidu.com/s/1pbRoywR2yS1H9OvVMt00OQ) 提取码:uf7h。

主界面样式

![](Eclipse插件开发笔记.assets/1.png)

### 1.1.2    eclipse IDE安装中文语言包

下载[语言包]( https://pan.baidu.com/s/1yjoSwztCHKcQZzdFrDRFBA) 提取码: 6a9g  ，在eclipse安装目录下创建`myplugins`目录。解压文件修改文件名为language。

![](Eclipse插件开发笔记.assets/f89cc94ffc0599e69eca2653fabdc6bb711292a7.png)

在eclipse安装目录下创建`links`目录，在`links`目录下创建`language.link`文件，在文件中写入插件目录`path=D://eclipse//myplugins//language`，重启eclipse。

> 恢复回英文环境只需要删除`links`目录下的`language.link`文件

### 1.2	eclipse 名词解释

- J2EE项目的（Web Tools Platform）
- 开发报表的BIRT（Business Intelligence and Reporting Tools）
- 富客户端平台（Rich Client Platform ，RCP）
- 嵌入式系统和设备项目开发。包括开发C/C++程序的CDT（C++ Development Toolkit）移动设备和J2ME项目的MTJ以及嵌入式设备的富客户端开发平台ERCP
- 富Internet应用程序（Rich Internet Application）。指利用ajax结合JavaScript开发具有丰富用户体验的Internet应用程序。 

### 1.3    SWT/JFace

#### 1.3.1	SWT

==SWT==（Standard Widget Toolkit，标准图形工具箱） 是一种Java开发的GUI程序的技术。与出自Sun的AWT（Abstract Widget Toolkit，抽象图形工具箱）和Swing不同，SWT是Eclipse的开发人员自行建造的。

==AWT==是Java最早的GUI技术，它采用了交集的办法来解决不同操作系统的图形平台不同显示风格的问题。

==Swing==是Sun提出的另外一种GUI解决方案，除了图形平台自己的一套标准的控件外，一般都会支持用户手绘界面的功能。但是完全脱离操作系统的支持，不能使用操作系统的消息处理机制而必须自己管理这些消息，影响了性能。

==SWT==技术吸取了AWT/Swing的优点。它同时采用了两者的一部分思想，吸取各个图形平台的经验决定自己的一个控件集合，然后针对某个目标平台进行判断，目标平台上有的控件直接使用，没有的控件采用Swing的方法进行绘制。

==JFace==是一套基于SWT的工具箱。它将一些常用的界面操作包装了起来，对界面设计进行了更高层次的抽象，使开发人员可以抽出更多精力关注程序的业务逻辑。JFface的设计目的是和SWT协同工作。