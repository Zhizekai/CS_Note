@[toc]

# 操作系统

>本文旨在总结windwos和MacOS的操作当中的各种技巧，使得后人可以更加快速的掌握MaxOS或者Liunx系统的操作。

## Windows

1.win+↑↓←→ 是分屏快捷键，win+Ctrl+D是新建虚拟桌面，都是win10系统可以正常使用的。

2.更改中英文输入法 `shift` + `alt`

3.搜索文件中带有特定字符串，在右上角的搜索中
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200608161127365.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
输入`System.FileName:”(1)”`，直接就能把重复图片删除同时也能实现图片降重的效果

4.快速删除有很多文件夹的文件，使用命令：
```bash
rmdir /s/q C:\abc
```
一般可以用于删除node_modules，非常快速
## 设置分屏
1.进入设置里的显示选项
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201129004947735.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
2. 对`多显示器设置`进行选择，可以复制当前屏幕，也可以扩展当前屏幕

### CMD
CMD的环境配置：
计算机右击-->属性-->高级系统设置-->高级选项卡-->环境变量-->系统变量：
添加环境变量
```bash
变量名:ComSpec 变量值:%SystemRoot%\system32\cmd.exe 
```
在path当中增加如下一条 

```bash
;%SystemRoot%\system32;%SystemRoot%%SystemRoot%\System32\Wbem;C:\Windows\SysWOW64;
```

## MacOS
### 快捷键

1.`command` + `shift` + `.`  隐藏文件夹/显示文件夹
2.`Shift` + `Command (⌘)`+ `5`  录屏
3.表情包首页 `control` + `command` + `space	` space就是空格键
4.剪切粘贴 `command` + `option` + `v`
5.切换搜狗输入法和系统输入法 `control` + `space`

### terminal
mac安装各种包最好先安装[HomeBrew](https://brew.sh/),有了它想安装什么包就安装什么包。安装过程不是很快,就铁等就完了。当然如果不想铁等就用如下命令,[参考](https://zhuanlan.zhihu.com/p/111014448)，会使用国内镜像加速安装

```bash
/bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"
```

### Download YouTube video

文件下载位置：`‎⁨Macintosh HD⁩ ▸ ⁨用户⁩ ▸ ⁨zhizekai⁩`
右键点击视频，copy视频url

默认下载

```bash
youtube-dl  <url>
```
获得指定链接中的视频格式

```bash
youtube-dl --list-formats <url>
```
查看格式列表

```bash
youtube-dl -F https://youtu.be/y7zgr6r5GxM
```


下载不同格式的音频和视频
```bash
youtube-dl -f <format code> <url>
```

> format code是格式编号，按照这个格式编号可以下载对应的视频或音频或视频
> 按format code下载指定的质量的视频

下面以一个例子来说明

下载对应格式

```bash
youtube-dl -f 137 https://youtu.be/y7zgr6r5GxM
```

下载对应音频

```bash
youtube-dl -f 140 https://youtu.be/y7zgr6r5GxM
```
记录一次解决的问题，在我很久不用这个包后再次使用这个工具，它显示了如下的问题
```powershell
ERROR: Signature extraction failed: Traceback (most recent call last):
  File "/Users/zhizekai/opt/anaconda3/lib/python3.7/site-packages/youtube_dl/extractor/youtube.py", line 1385, in _decrypt_signature
    video_id, player_url, s
  File "/Users/zhizekai/opt/anaconda3/lib/python3.7/site-packages/youtube_dl/extractor/youtube.py", line 1262, in _extract_signature_function
    raise ExtractorError('Cannot identify player %r' % player_url)
youtube_dl.utils.ExtractorError: Cannot identify player 'https://www.youtube.com/s/player/0acb4375/player_ias.vflset/en_US/base.js'; please report this issue on https://yt-dl.org/bug . Make sure you are using the latest version; see  https://yt-dl.org/update  on how to update. Be sure to call youtube-dl with the --verbose flag and include its complete output.
 (caused by ExtractorError("Cannot identify player 'https://www.youtube.com/s/player/0acb4375/player_ias.vflset/en_US/base.js'; please report this issue on https://yt-dl.org/bug . Make sure you are using the latest version; see  https://yt-dl.org/update  on how to update. Be sure to call youtube-dl with the --verbose flag and include its complete output.")); please report this issue on https://yt-dl.org/bug . Make sure you are using the latest version; see  https://yt-dl.org/update  on how to update. Be sure to call youtube-dl with the --verbose flag and include its complete output.
```
其实问题很简单就是需要更新了，输入更新命令就行，而且这还是在pip的管理之下

```powershell
pip install --upgrade youtube-dl
```
就好了


### mac下连接sftp服务器

　　mac上建议下载**filezilla**，直接连接，用户名和密码直接输入服务器的用户名和密码，端口号填22，22是sftp的默认端口号，使用sftp连接服务器省去了安装pure-ftpd和配置的问题
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201101155701141.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70#pic_center)

### 关闭仪表盘

设置，调度中心，仪表盘那项把单独空间改为关闭

## Liunx

### 安装redis
开启对外访问,绑定ip为0.0.0.0就行.修改完这些之后一定要重启redis
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200627180754993.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
### 安装GraphicsMagick
1.安装相关依赖

```bash
$ yum install -y gcc libpng libjpeg libpng-devel libjpeg-devel ghostscript libtiff libtiff-devel freetype freetype-devel
```

2.下载并解压到目录/usr/local/

```bash
$ wget ftp://ftp.graphicsmagick.org/pub/GraphicsMagick/1.3/GraphicsMagick-1.3.20.tar.gz
```
```bash
$ tar -zxvf GraphicsMagick-1.3.20.tar.gz -C /usr/local/
```
3.编译并安装：

```bash
$ cd /usr/local/GraphicsMagick-1.3.20
```

```bash
$ ./configure --prefix=/usr/local/GraphicsMagick-1.3.20 --enable-shared
```
```bash
$ make
```
4.配置环境变量

```bash
$ bashvi /etc/profile
```
在/etc/profile文件的最后添加如下配置：

```bash
export JAVA_HOME=/usr/java/java
PATH=$PATH:$JAVA_HOME/bin:$JAVA_HOME/jre/bin
CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$CLASSPATH
export JAVA_HOME PATH CLASSPATH

export GMAGICK_HOME="/usr/local/GraphicsMagick-1.3.20"
export PATH="$GMAGICK_HOME/bin:$PATH"
LD_LIBRARY_PATH=$GMAGICK_HOME/lib:$LD_LIBRARY_PATH
export LD_LIBRARY_PATH
```
>修改完后执行 `ldconfig` 让设置立即生效，并logout，然后重新登录。


5.验证：

```bash
gm version
```





