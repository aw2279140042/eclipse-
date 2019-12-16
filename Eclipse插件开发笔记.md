# Eclipse插件开发笔记

## 1	Eclipse IDE环境篇

### 1.1.1    安装及使用eclipse IDE

运行eclipse IDE前需要先安装Java运行环境（JRE）[jdkx6417.zip](https://pan.baidu.com/s/1zA4bai3tLlDNLPcTRzBwsA) 提取码: yxf6。在eclipse网站`http://www.eclipse.org/downloads/` 下载eclipse IDE[eclipse-jee-indigo-SR2-win32-x86_64.zip](https://pan.baidu.com/s/1pbRoywR2yS1H9OvVMt00OQ) 提取码:uf7h。

主界面样式

![1.png](Eclipse插件开发笔记.assets/1.png)

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

Eclipse RCP是帮助开发者创建和部署富客户端的平台。所谓服客户端，是指为用户提供了丰富功能体验的客户端程序。通常来说，一个富客户端程序应该有以下特征。

- 首先是桌面程序而不能是WEB应用程序；
- 可以暂时性的脱离网络运行，还可以对客服端的本地资源，如文件系统、打印机等进行操作。其次，界面美观，功能丰富，具有跨平台性并且可以和操作系统的图形平台紧密结合（支持拖拽操作，可以在系统托盘中显示），对用户的操作响应性好（在网络不畅时不能停止响应）
- 富客户端可以承担一定程度的数据缓存以及业务逻辑计算功能，如出现新版本时自动升级系统等。  

### 1.6	EMF技术

在编写面向对象的程序中，首先必须将实际生活中的例子抽象成Java对象来建立结构化的数据模型。==EMF==（Eclipse Modeling Framework，Eclipse建模框架）就是一项致力于简化建模工作的项目。用户只需要描述需要建立的模型，就可以通过EMF生成健壮的、易于使用的数据模型实现代码。EMF项目由一下三大部分组成。

- EMF核心框架

  EMF框架允许用户通过编写Java接口，从Rose导入UML类图等方法生成一个描述用户需要的数据模型的元模型（Meta Model）。在EMF项目中，这个元模型被称为Ecore。它描述着数据模型中包含哪些对象，对象中有哪些方法和属性，以及这些对象间关系。用户可以直接从这个元模型生成数据模型的实现代码，这些代码是基于EMF运行时框架的。

- EMF.Edit

  它提供的功能都和数据模型编辑相关。它为数据模型提供各种功能的适配器，使得生成的数据模型可以直接作为JFace的内容来源，也可以在Eclipse的属性师徒中展示出来病可编辑。这部分框架需要和CodeGen配合使用

- EMF.CodeGen

  这部分用于代码生成。生成的数据模型代码除包含了数据模型的接口和实现外，还包含了一个工厂类用于生成数据模型的实例，以及一个Package类型，其中包含了数据模型的元数据。同时，CodeGen也可以生成一个基于Eclipse RCP的编辑器，用于对数据模型的内容进行编辑。

EMF主要适用与模型驱动（Model Driven）的程序

### 1.7	GEF技术

图形化编辑可以直观的显示模型对象的属性和对象之间的关系，在很多情况下都很有用，如UML类图设计，工作流程图设计等。==GEF==（Graphical Editing Framework）是为了方便开发者开发基于RCP的，支持图形化编辑的程序界面设计的一套框架。

![image-20191214132653402](Eclipse插件开发笔记.assets\image-20191214132653402.png)

## 2	SWT/JFace概述

SWT技术是第一套基于Java的第三方图形工具库。它的设计思想是提供一套通用的API使得开发出的图形程序不仅可以不加修改的在平台间移植，而且外观和速度上与使用C/C++等语言在操作系统平台上开发出来的本地图形程序毫无区别，还可以只用鼠标拖放操作、系统托盘等高级的系统服务。

SWT程序与操作系统交互时，使用了JNI技术。简单来说是讲Java语言编写的接口与C语言编写的函数绑定，从而使得调用Java接口就等于调用C函数的技术。

### 2.1	SWT结构浅析

SWT的基本体系结构分为三层如图

![image-20191214160321223](Eclipse插件开发笔记.assets\image-20191214160321223.png)

- 第一层是SWT的API。外部开发者使用SWT时就是使用这些API编写SWT程序。这里包含了SWT的控件（文本框，按钮等）、时间处理（各种时间及监视器）、等和图形界面开发者关系最为密切的部分。同时也只有这一部分对外部开发者可见。
- 第二层时JNI相关的代码。每个操作系统提供的API都拥有自己定义的一系列独特的数据类型作为参数类型及返回值。这一层只在SWT内部可见。
- 第三层是使用C程序编写的操作系统本地动态链接库文件。这一层的代码在window平台上编译成DLL文件，而在linux上编译为so文件。

### 2.2	SWT API结构

SWT API的基本构成

![1576465923763](Eclipse插件开发笔记.assets/1576465923763.png)

#### 2.2.1	组件类	Widgets

组件是用户界面的组成部分。在一个SWT程序中，界面上的所有内容，如按钮、文本框等，包括窗口本身都是组件。整个图形界面是有组件构成的。

组件分为控件（Control）和项目（Item）。控件是界面的主体，项目依赖于控件并未他们提供附加功能。有些控件是专门用来容纳、分组其他控件的，它们被称为容器控件。窗口控件（Shell）就属于容器控件。

#### 2.2.2	布局类	Layout

它主要是由布局管理器（Layout Manager）组成。当一个布局管理器被安装到窗口上之后，它就负责着在窗口中安排控件位置和尺寸。当窗口尺寸变化时，布局管理器会根据一定的策略重新计算这些数据，并将控件安排在合适窗口新尺寸的位置上。不同的布局管理器，就代表了安防控件的一种不同策略。

#### 2.2.3	事件类	Events

事件类主要负责控件的消息传递。用户点击了界面上一个按钮，在文本框中输入了一段文字，或者仅仅是移动了一下鼠标，都会产生一个事件（Event）。事件是图形界面程序与用户交互的核心。SWT的事件处理机制采用了事件监听器（Event Listener）的结构，即使用Observer（观察者）的设计模式来处理时间。对某个对象上的某个事件感兴趣的话，就需要在对象上注册一个对应的事件的监听器。当事件发生时，所有在对象上注册过的此事件监听器都会收到通知。

监听器是一个接口，其中包含的每个方法都对应了某种事件的发生