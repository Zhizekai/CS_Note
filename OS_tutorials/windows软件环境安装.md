# windows各种开发环境的安装指南
>写这个的原因就是为了给自己梳理一下未来需要做的东西


## 1.安装java环境
下载安装就行
## 2.安装python环境
1.安装python环境要直接下载anaconda，用它的虚拟环境进行安装
2.调试anaconda环境

修改jupyter lab的默认工作目录
　　1.打开anaconda prompt 输入`jupyter lab --generate-config`
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020122311443577.png)
　　2.找到配置文件目录，我的配置文件目录在`C:\Users\asus\.jupyter`，打开配置文件，找到
```
# The directory to use for notebooks and kernels.
#  c.NotebookApp.notebook_dir = ''
```
把它改成
```
## The directory to use for notebooks and kernels.
#  Default: ''
c.NotebookApp.notebook_dir = 'G:/'
```
保存退出就可以

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201223114919798.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
注意：此方法修改完之后只有通过anaconda进入jupyter lab才可以生效，桌面快捷方式进入不起作用

## 3.安装node.js环境
1.去nodejs官网下载LTS的安装包https://nodejs.org/en/ ，选择除C盘以外的其他目录进行安装即可
2.


https://www.jianshu.com/p/13f45e24b1de
