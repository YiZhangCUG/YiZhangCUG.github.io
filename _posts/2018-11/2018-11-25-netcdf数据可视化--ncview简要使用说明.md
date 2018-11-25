---
layout: post
title: "netcdf数据可视化--ncview简要使用说明"
date: 2018-11-25 14:11:47 -0800
author: Yi Zhang
category: program
tags: [ncview,visualization,tutorial]
header-img: "img/light.jpeg"
---

* content
{:toc}



## 简介与安装

[ncview](http://meteora.ucsd.edu/%7Epierce/ncview_home_page.html)是由Dr. David W. Pierce编写的一款[netcdf](https://www.unidata.ucar.edu/software/netcdf/)可视化工具。我们可以使用它来快速浏览netcdf格式的数据，切割获取剖面数据。ncview原生运行于类UNIX平台，运行依靠X11或者R4窗口平台。本文主要介绍如何在Mac OS和Ubuntu系统下如何安装ncview，以及基本的使用方法。

+ Mac OS系统下安装ncview最简单的方法是通过[Homebrew](https://brew.sh)进行安装，运行以下命令安装ncview：

```bash
brew cask install xquartz
brew install ncview
```
+ Ubuntu系统下一般已经预先安装X11环境。因此，我们只需要直接安装ncview就行了：

```bash
sudo apt-get ncview
```

## 界面与基本操作

安装完成以后，使用ncview浏览netcdf文件非常的简单。因为ncview运行于X11环境，因此我们需要从终端启动它。将netcdf文件的名称提供给ncview就可以开启软件，即`ncview <netcdf-file>`。以下是Mac OS下的终端截图，ncview将在终端显示当前的运行环境。

![ncview-open](/assets/2018-11/ncview-open.png)

以下是ncview的默认显示界面，包含一个控制面板和数据显示窗口。控制面板从上至下可以分为五个部分，最上方显示当前浏览数据的一些基本信息。包括数据名称，显示中数据的最大与最小值，鼠标指示位置的坐标与数值。**值得注意的两点**是数据名称不等同于netcdf文件的名称，因为一个netcdf文件可能包含多个数据体（我们可以通过控制面板下方Var选项卡选择想要浏览的数据），这里显示是当前数据窗口的数据信息。第二点是为了获取更好的显示效果，ncview默认不显示超出数据正态分布部分的数值。因此在默认窗口下显示的数据最大与最小值并非数据的真实范围。如果需要，我们需要右键单击Range选项来显示全部数据。如果要快速查看某个数据点的值，我们只需要将鼠标移动到数据显示窗口的对应位置即可。

数据信息窗口下是ncview的功能按键区域。其中，第一行动画显示控制（仅在netcdf文件中包含随时间变化数据的情况下有效）。第二行为数据显示控制按键，从左至右依次为切换色标文件、反转纵坐标、反转色标、缩放显示窗口、切换色标显示方式、切换数据显示范围、切换是否使用插值显示和打印。**注意**使用鼠标左右键点按这些按键时分别代表向前和向后选择。

按键区域下方分别是色标显示区域，以及数据选择区域。当有多个数据体可供选择时，我们可以通过它选择需要查看的数据。控制面板最下方显示坐标轴范围与对应的坐标轴名称，我们可以通过改变横纵坐标轴所对应的数据坐标轴对数据显示进行旋转。下面本文将就部分选项进行说明。

![ncview-default-view](/assets/2018-11/ncview-default-view.png)

### 更改色标文件

通过鼠标左右键点击色标切换按钮，我们可以向前和向后切换使用的色标文件（如下图所示），色标按键将显示当前使用的色标文件名称。色标使用的顺序可以在设置选项中进行调整。

![ncview-change-cpt](/assets/2018-11/ncview-change-cpt.png)

### 选项卡

点击Option按键打开选项卡（如下图所示）。主要包含三个部分：显示边界线（仅在坐标轴为经纬度时可用）、数据统计方法选择和色标文件选项。我们可以开启和关闭对应色标文件和对色标文件的使用顺序进行排列。

![ncview-option-view](/assets/2018-11/ncview-option-view.png)

### 数据编辑

点击Edit按键我们可以数据值进行人工设置，或者点击Dump Data将数据到出为文本格式。

![ncview-edit-data](/assets/2018-11/ncview-edit-data.png)

### 剖面显示

点击数据显示窗口的相应位置我们可以对数据剖面进行查看，单个窗口默认最多显示5条剖面。选择窗口中X Axis对应的数据坐标轴来控制剖面显示的横坐标轴。

![ncview-show-profile](/assets/2018-11/ncview-show-profile.png)

通过设置剖面显示窗口中X Range与Y Range值，ncview可以显示部分剖面数值。

![ncview-profile-range](/assets/2018-11/ncview-profile-range.png)

### 打印数据到文件

最后，通过Print功能，我们可以将数据打印到一个PS文件（如下图），图件包含数据的一些基本信息，我们可以通过其他工具（如[imagemagick](http://www.imagemagick.org/script/index.php)）将其转换为多种图片格式，方便使用。

![ncview-print](/assets/2018-11/ncview-print.png)
