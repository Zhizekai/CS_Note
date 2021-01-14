@[TOC]
# $\LaTeX$
## mac下安装latex环境
1. 上[MacTEX的网站](http://www.tug.org/mactex/mactex-download.html)把mactex.pkg包下载下来，直接安装就完了，安装完之后会多处四个软件TexShop,LaTeXiT,Tex Live Utility,BibDesk。TexShop就是环境自带的编辑器，BibDesk是文献管理工具,

> 如果觉得太慢,我这有百度云的MacTEX的连接
> 链接:https://pan.baidu.com/s/1YHDPg8S5ZyXfy9NpJ17RXA  密码:dpwc

2. 然后下载[vscode](https://code.visualstudio.com/Download),在vscode的extensions里面安装下面三个软件![在这里插入图片描述](https://img-blog.csdnimg.cn/20200517101036450.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
3. 就差最后一步的配置工作,点击vcode左下脚的设置，搜索latex的json配置文件
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020051710132093.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)修改配置文件为了能支持中文.配置文件如下
```bash
{
    "latex-workshop.view.pdf.viewer": "tab",
     // Latex workshop
     "latex-workshop.latex.tools": [
        {
            "name": "xelatex",
            "command": "xelatex",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "-pdf",
                "%DOC%"
            ]
        },
        {
            "name": "latexmk",
            "command": "latexmk",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "-pdf",
                "%DOC%"
            ]
        },
        {
            "name": "pdflatex",
            "command": "pdflatex",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "%DOC%"
            ]
        },
        {
            "name": "bibtex",
            "command": "bibtex",
            "args": [
                "%DOCFILE%"
            ]
        }
    ],
    "latex-workshop.latex.recipes": [
        {
            "name": "xelatex",
            "tools": [
                "xelatex"
            ]
        },
        {
            "name": "pdflatex -> bibtex -> pdflatex*2",
            "tools": [
                "pdflatex",
                "bibtex",
                "pdflatex",
                "pdflatex"
            ]
        }
    ],
    "[latex]": {
    
    }

}
```
4. 然后就在网上随便找个模版编译运行吧

> 参考模版:
> [LaTeX 模版大全](https://www.latexstudio.net/articles/)
> [计算机青年报双排中文模版](https://www.latexstudio.net/archives/9189.html)
> [ICLR 2019](https://iclr.cc/Conferences/2019/CallForPapers)
> 北大毕业论文模版,中文的百度云链接:https://pan.baidu.com/s/1wSqcBmqUPzSAFh40SYTeqg  密码:n88n
## Windows下安装latex环境
1. 下载TexLive,[官方网站](http://tug.org/texlive/)和[清华大学镜像](https://mirrors.tuna.tsinghua.edu.cn/CTAN/systems/texlive/Images/)都可以用.
2. 然后安装就完了
3. 然后安装vscode和在mac上安装的东西一样.
> 
> 参考文章 
> [LaTeX学习：Texlive 2019和TeXstudio的安装及使用](https://blog.csdn.net/Mikchy/article/details/94448707)

## 参考文献的引用
文末写下参考文献
```bash
\begin{thebibliography}{99}  
\bibitem{ref1}Zheng L, Wang S, Tian L, et al., Query-adaptive late fusion for image search and person re-identification, Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition, 2015: 1741-1750.  
\bibitem{ref2}Arandjelović R, Zisserman A, Three things everyone should know to improve object retrieval, Computer Vision and Pattern Recognition (CVPR), 2012 IEEE Conference on, IEEE, 2012: 2911-2918.  
\bibitem{ref3}Lowe D G. Distinctive image features from scale-invariant keypoints, International journal of computer vision, 2004, 60(2): 91-110.  
\bibitem{ref4}Philbin J, Chum O, Isard M, et al. Lost in quantization: Improving particular object retrieval in large scale image databases, Computer Vision and Pattern Recognition, 2008. CVPR 2008, IEEE Conference on, IEEE, 2008: 1-8.  
\end{thebibliography}
```
文中引用参考文献

```bash
\cite{ref1}
\cite{ref1, ref5}
```

# Word/PPT
## 快捷键
格式刷 `command` + `shift` + `c` 和 `command` + `shift` + `v`     
删除回车符 按`fn` + `delete` 
快速上标 `shift` + `command` + `+`

## 关闭拼写检查
在左上角的偏好设置里面
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200705151955204.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020070515201549.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
## 显示/隐藏回车符
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507164828875.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
## 页码，页眉，页首
都在插入

## 布局里的分节符
MAC中删除分节符先得显示编辑标记![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507173818188.png)
再点中分节符，摁`fn` + `delete` 

## 目录
目录的位置在引用里面，在做好页码之后，加个分页符，注意不要选择手动目录，要选择下面的自动目录
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507175848496.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
## 行间距
调整标题的行间距
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507191610813.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
在段落里的段前，段后
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200507191710347.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
## 公式
在需要输入公式的地方 `control` + `=` 会出现公式框
就按照latex的语法输入每次输入完要按空格才会输入进去

## 给图片加题注
选中图片，在引用里，插入题注
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200508144829288.png)
## 文献引用
在文末写好文献，并标好序号，选择定义新的编号形式，
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020050819053066.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
在正文中需要插入的地方,点击那句话的末尾，然后选择插入下的交叉引用
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200508190736921.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
在交叉引用里面选择对应的文献编号,就会在那句话的末尾出现一个[1],然后把它变成上标

## MAC转成pdf目录无法跳转
注意要打开全局模式SSR才能转换成功
选择最适合电子分发
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200516220742891.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
