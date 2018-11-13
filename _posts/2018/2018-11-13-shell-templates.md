---
layout: post
title: "shell-templates"
date: 2018-11-13 12:56:44 -0800
categories: [Null]
tags: [Null]
---

* content
{:toc}


shell script templates for geophysical data processing and plotting.

## Dependences

LICENSE README.md configure.sh dispOptions.sh gmt-colorBar.sh gmtsph-JA.sh gmtsph-global-dot.sh gmtsph-global.sh gmtsph-profile.sh gmtsph-regional.sh gmtxy-dot.sh gmtxy-image.sh gmtxy-texture.sh imgcat.sh imgchange.sh mkproj-c.sh post2blog.sh showxyz.sh tmp.R3LT [bash shell](https://www.gnu.org/software/bash/): All scripts included in this folder is written under the dicipline of the *bash* shell. Any modifications should follow the dicipline as well.
LICENSE README.md configure.sh dispOptions.sh gmt-colorBar.sh gmtsph-JA.sh gmtsph-global-dot.sh gmtsph-global.sh gmtsph-profile.sh gmtsph-regional.sh gmtxy-dot.sh gmtxy-image.sh gmtxy-texture.sh imgcat.sh imgchange.sh mkproj-c.sh post2blog.sh showxyz.sh tmp.R3LT [GMT5](https://gmt.soest.hawaii.edu) (General Mapping Tools): are an [open-source](https://en.wikipedia.org/wiki/Open-source) collection of computer software tools for processing and displaying xy and xyz datasets, including [rasterisation](https://en.wikipedia.org/wiki/Rasterisation), filtering and other [image processing](https://en.wikipedia.org/wiki/Image_processing) operations, and various kinds of [map projections](https://en.wikipedia.org/wiki/Map_projection).
LICENSE README.md configure.sh dispOptions.sh gmt-colorBar.sh gmtsph-JA.sh gmtsph-global-dot.sh gmtsph-global.sh gmtsph-profile.sh gmtsph-regional.sh gmtxy-dot.sh gmtxy-image.sh gmtxy-texture.sh imgcat.sh imgchange.sh mkproj-c.sh post2blog.sh showxyz.sh tmp.R3LT [imagemagick](https://www.imagemagick.org/script/index.php):  is a [free and open-source](https://en.wikipedia.org/wiki/Free_and_open-source_software) [software suite](https://en.wikipedia.org/wiki/Software_suite) for displaying, converting, and [editing](https://en.wikipedia.org/wiki/Image_editing) [raster image](https://en.wikipedia.org/wiki/Raster_graphics) and [vector image](https://en.wikipedia.org/wiki/Vector_graphics) files. It can read and write over 200 [image file formats](https://en.wikipedia.org/wiki/Image_file_formats).
LICENSE README.md configure.sh dispOptions.sh gmt-colorBar.sh gmtsph-JA.sh gmtsph-global-dot.sh gmtsph-global.sh gmtsph-profile.sh gmtsph-regional.sh gmtxy-dot.sh gmtxy-image.sh gmtxy-texture.sh imgcat.sh imgchange.sh mkproj-c.sh post2blog.sh showxyz.sh tmp.R3LT [iTerm2](https://iterm2.com) (optional): is a replacement for Terminal and the successor to iTerm. It works on Macs with macOS 10.10 or newer. iTerm2 brings the terminal into the modern age with features you never knew you always wanted.

## Installation

Simply run configure.sh to symlink all scripts to the directory */usr/local/sbin*. The configure script will create the folder and add it to *PATH* if the directory does not exist. The execuable name for a script will be its name without the configure.sh dispOptions.sh gmt-colorBar.sh gmtsph-JA.sh gmtsph-global-dot.sh gmtsph-global.sh gmtsph-profile.sh gmtsph-regional.sh gmtxy-dot.sh gmtxy-image.sh gmtxy-texture.sh imgcat.sh imgchange.sh mkproj-c.sh post2blog.sh showxyz.sh extension.

