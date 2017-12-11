# Linux 与生物信息

Linux 与生物信息学紧密相关，许多软件运行和数据分析都适合或必须运行在 Linux 操作系统中。关于 Linux 的教学网络上不计其数，这里只对在测序数据分析中可能涉及到的一些基本 Linux 操作做一个简单的介绍。

## 生信运行环境

生信软件的运行平台环境一般分为以下几种：

1. 基于web：可以在win/mac/linux/bsd等平台运行，只需系统有图形界面，并安装了现代化的主流浏览器如chrome/firefox等。
2. 纯windows环境：常见的商业软件往往只能在win环境下运行，如bionumerics等。
3. 多平台环境：许多生信软件是采用java开发，可以在多个平台下运行。一些C开发的程序也有win/mac/linux版本。
4. 纯linux环境：许多生信软件只能在linux/mac环境下运行，其中大部分又是基于命令行而不需要图形界面。

## 发行版

无论是在服务器上安装，或者是个人桌面使用Linux，都需要考虑一个问题，那就是使用哪一个发行版。服务器常用的Linux发行版有CentOS, Debian, Ubuntu等，桌面发行版非常多，主要有基于Ubuntu，基于Archlinux等发行版。不同的发行版相当于使用不同的包管理软件，以及系统控制方式等方面存在区别。

比如包管理和安装的差别：

```
# 以下分别是：CentOS, Debian/Ubuntu, Archlinux 安装 bwa 软件的方式
$ sudo yum
$ sudo apt-get install bwa
$ sudo pacman -S bwa
```
