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

### 1.4	插件技术和OSGI

Eclipse平台包含有很多功能模块，如JDT（Java Development Toolkit）等模块的历史几乎和Eclipse一样悠久，以至于人们认为它们是Eclipse平台不可或缺的组成部分，事实上Eclipse平台不包含任何专用的模块，它的设计遵循微内核理念，即提供最基本的运行时环境，简单的系统和模块之间交互的渠道，而各模块则使用这些服务运行并相互交流。

为了处理模块之间的依赖关系，Eclipse提出了扩展（Extension）和扩展点（Extension Point）的概念。每一个希望被别的程序模块扩展的模块，都必须声明一系列的扩展点。而希望在这个模块上扩展功能的程序模块，就需要按照扩展点声明来编写扩展。扩展点提供服务功能，而扩展使用这些服务。凡遵循这套扩展规则的模块，都可以方便的往体系中添加或删除，即==可插拔==的，因而被称为==插件==（Plug-in）。

插件技术使得系统的结构简练，可维护性与可扩展性大增。但是一切都是插件，使得插件的数量同样大增。因为用户不可能同时使用所有的插件，Eclipse采用了延迟加载（Lazy Loading）的技术，只有一个插件被其他插件调用的时候才将它装载到内存中。

延迟加载体系中，扩展和扩展点的声明，都通过遵循特定规范的XML文件完成的。这些文件被称为==清单==（Manifest），在这些清单中指明了具体实现扩展功能的Java代码。

```xml
<!--扩展点声明 -->
<extension-point id="views"							
                 name="org.eclipse.ui.views //扩展点名称"		 	
                 schema="schema/views.exsd //Eclipse专用的manifest格式描述文件。对扩展点的xml格式进行定义"/>         
<!--扩展声明 -->
<extension point="org.eclipse.ui.views //扩展点名称">
	<view allowMultiple="false" class="org.harper.ecocenter.client.ManageView //扩展功能具体实现类" id="org.harper.ecocenter.client.ManageView" name="Manage"
</extension>
```

==OSGi==（Open Services Gateway initiative ，开放式服务网关协议）是一套基于Java的开放式接口协议。它的思想与Eclipse插件的思想有些类似，然而OSGi的框架体系实现了在运行时对模块动态添加和删除功能的支持。

### 1.5	RCP技术

