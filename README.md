# sublimetext2
sublime text2 build 2221中文支持

1、下载sublime text2压缩包，并解压
2、安装gtk2环境开发包，如果已经安装，直接跳过
3、复制 sublime_imfix.c 到sublime的lib目录里，编译动态链接库
	gcc -shared -o libsublime-imfix.so sublime_imfix.c `pkg-config --libs --cflags gtk+-2.0` -fPIC
4、自己制作启动脚本，并加入环境变量中
	#!/bin/bash
	SUB3_HOME=$HOME/Software/sublime_text_3
	CMD="LD_PRELOAD=./libsublime-imfix.so ./sublime_text"
	FILENAME=$1
	if [ -n "$1" ]
	then
	CMD=${CMD}" "`pwd`/$FILENAME
	fi
	cd "$SUB3_HOME"
	eval $CMD
5、完毕