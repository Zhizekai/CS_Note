@[toc]
# Nodejs环境安装配置
## Mac 安装Nodejs
推荐使用homebrew安装node
[参考](https://www.jianshu.com/p/da1e536fe475)

## Windows安装Nodejs
1.去nodejs官网下载LTS的安装包 [https://nodejs.org/en/](https://nodejs.org/en/) ，选择除C盘以外的其他目录进行安装即可
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201223143128252.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)

## npm配置
1.不推荐使用cnpm,cnpm安装包的路径有些奇怪，所以把cnpm的东西都删了

2.修改npm的镜像源，首先查看npm的源：
```bash
npm config get registry
```
这里npm的默认源是 `https://registry.npmjs.org/`，速度很慢，推荐使用国内镜像
npm更改淘宝镜像：
```bash
npm config set registry https://registry.npm.taobao.org
```
这里修改之后使用npx同样也会加速
3.查看npm的默认配置文件路径，直接从控制台输入：
```bash
npm config ls
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201223145711189.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
这里显示当前配置文件的路径为`C:\Users\asus\.npmrc`，可以从这个配置文件当中直接改变配置信息，比如之前设置的镜像源也会在那里显示

修改npm的默认下载路径
```bash
npm config set prefix "G:\Program\nodejs\node_global_modules"
npm config set cache "G:\Program\nodejs\node_cache"
```

4.查看npm 默认下载包路径
我们在执行`npm install -g XXXX`下载全局包时，这个包的默认存放路径位于`C:\Users\用户名\AppData\Roaming\npm\node_modules`下，可以通过CMD指令`npm root -g`查看。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201223150051212.png)
> 参考文档：https://www.jianshu.com/p/13f45e24b1de　

## 快速删除node_modules
###  使用windows强制删除命令
1.使用windwos上的强制删除，效果是以肉眼可见的速度删除文件夹，在需要删除的文件夹目录下按住shift + 鼠标右键。点击在当前位置打开powershell，输入命令：
```bash
rmdir /s/q .\node_modules\
```
完成删除
### 使用npm的一个包
用npm删除（不太推荐）
```bash
npm install -g rimraf
#cd到项目根目录
rimraf node_modules
```

6.启动npm热重载

```bash
npm start
```

7.查看npm全局安装的包

```bash
npm list -g --dept 0
```

8.npm 不同命令的含义
npm install moduleName 命令
1. 安装模块到项目node_modules目录下。
2. 不会将模块依赖写入devDependencies或dependencies 节点。
3. 运行 npm install 初始化项目时不会下载模块。

npm install -g moduleName 命令
1. 安装模块到全局，不会在项目node_modules目录中保存模块包。
2. 不会将模块依赖写入devDependencies或dependencies 节点。
3. 运行 npm install 初始化项目时不会下载模块。

npm install -save moduleName 命令
1. 安装模块到项目node_modules目录下。
2. 会将模块依赖写入dependencies 节点。
3. 运行 npm install 初始化项目时，会将模块下载到项目目录下。
4. 运行npm install --production或者注明NODE_ENV变量值为production时，会自动下载模块到node_modules目录中。

npm install -save-dev moduleName 命令
1. 安装模块到项目node_modules目录下。
2. 会将模块依赖写入devDependencies 节点。
3. 运行 npm install 初始化项目时，会将模块下载到项目目录下。
4. 运行npm install --production或者注明NODE_ENV变量值为production时，不会自动下载模块到node_modules目录中。

总结
devDependencies 节点下的模块是我们在开发时需要用的，比如项目中使用的 gulp ，压缩css、js的模块。这些模块在我们的项目部署后是不需要的，所以我们可以使用 -save-dev 的形式安装。像 express 这些模块是项目运行必备的，应该安装在 dependencies 节点下，所以我们应该使用 -save 的形式安装。

8.安装yarn

```bash
npm install -g yarn
```


## yarn配置

```bash
yarn config get registry
```
查看yarn的当前使用的镜像源

```bash
yarn config set  registry https://registry.npm.taobao.org/
```

全局修改yarn镜像
如果出现任何问题，重新安装包就可以

初始化项目

```bash
npm install -g vue-cli
vue init webpack gshop
cd gshop
npm install
npm run dev
```
打包项目

```bash
npm run build
npm install -g serve
serve dist
```

