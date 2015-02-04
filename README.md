# sublimetext2
## sublime text2 build 2221中文支持

1. 下载sublime text2压缩包，并解压
2. 安装gtk2环境开发包，如果已经安装，直接跳过
3. 复制 sublime_imfix.c 到sublime的lib目录里，编译动态链接库
* gcc -shared -o libsublime-imfix.so sublime_imfix.c `pkg-config --libs --cflags gtk+-2.0` -fPIC
4. 自己制作启动脚本，并加入环境变量中
<pre><code>
> #!/bin/bash
> CMD="LD_PRELOAD=$HOME/Software/sublime_text_3/libsublime-imfix.so $HOME/Software/sublime_text_3/sublime_text"
> FILENAME=$1
> if [ -n "$1" ]
> then
>	CMD=${CMD}" "`pwd`/$FILENAME
> fi
> eval $CMD
</code></pre>


6. sublime package安装
	ctrl + ～ 调出控制台
<pre><code>
import urllib2,os; pf='Package Control.sublime-package'; ipp = sublime.installed_packages_path(); os.makedirs( ipp ) if not os.path.exists(ipp) else None; urllib2.install_opener( urllib2.build_opener( urllib2.ProxyHandler( ))); open( os.path.join( ipp, pf), 'wb' ).write( urllib2.urlopen( 'http://sublime.wbond.net/' +pf.replace( ' ','%20' )).read()); print( 'Please restart Sublime Text to finish installation')
</code></pre>
	