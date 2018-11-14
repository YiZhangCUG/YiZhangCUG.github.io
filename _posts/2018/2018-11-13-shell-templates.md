---
layout: post
title: "shell-templates"
date: 2018-11-13 19:44:15 -0800
categories: [Command Line Tools]
tags: [Shell]
---

* content
{:toc}


shell script templates for geophysical data processing and plotting.

## Dependences

* [bash shell](https://www.gnu.org/software/bash/):  All scripts included in this folder is written under the dicipline of the *bash* shell. Any modifications should follow the dicipline as well.
* [GMT5](https://gmt.soest.hawaii.edu) (General Mapping Tools): are an [open-source](https://en.wikipedia.org/wiki/Open-source) collection of computer software tools for processing and displaying xy and xyz datasets, including [rasterisation](https://en.wikipedia.org/wiki/Rasterisation), filtering and other [image processing](https://en.wikipedia.org/wiki/Image_processing) operations, and various kinds of [map projections](https://en.wikipedia.org/wiki/Map_projection).
* [imagemagick](https://www.imagemagick.org/script/index.php):  is a [free and open-source](https://en.wikipedia.org/wiki/Free_and_open-source_software) [software suite](https://en.wikipedia.org/wiki/Software_suite) for displaying, converting, and [editing](https://en.wikipedia.org/wiki/Image_editing) [raster image](https://en.wikipedia.org/wiki/Raster_graphics) and [vector image](https://en.wikipedia.org/wiki/Vector_graphics) files. It can read and write over 200 [image file formats](https://en.wikipedia.org/wiki/Image_file_formats).
* [iTerm2](http://iterm2.com) (optional): is a replacement for Terminal and the successor to iTerm. It works on Macs with macOS 10.10 or newer. iTerm2 brings the terminal into the modern age with features you never knew you always wanted. [test pdf1](/assets/2018-11/test-pdf1.pdf).
* Test image1 ![test image1](/assets/2018-11/test-image1.png). Here comes another picture ![test image2](/assets/2018-11/test-image2.png).
* Test image3 ![test image3](/assets/2018-11/test-image3.png).
* [test pdf2](/assets/2018-11/test-pdf2.pdf).

## Installation

Simply run **configure.sh** to symlink all scripts to the directory */usr/local/sbin*. The configure script will create the folder and add it to *PATH* if the directory does not exist. The execuable name for a script will be its name without the *.sh* extension.

