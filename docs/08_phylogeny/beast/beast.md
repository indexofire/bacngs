# BEAST 入门教程

## Linux 服务器中安装

1. 安装 beagle

```bash
$ sudo apt-get install build-essential autoconf automake libtool subversion pkg-config openjdk-8-jdk
$ git clone --depth=1 https://github.com/beagle-dev/beagle-lib
$ cd beagle-lib
$ ./autogen.sh
$ ./configure --prfix=/usr/local
$ make
$ sudo make install
$ export LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH
$ make check
```

## 运行

beauti 设置好 xml 文件后，用 beast 运行

```bash
$ beast run_1.xml
```

如果没有安装 beagle

```bash
$ beast -beagle_off -threads 40 run_1.xml
```
