# Node.js基础操作

### npm安装淘宝镜像

`npm install cnpm -g --registry=https://registry.npm.taobao.org`

### 怎么快速删除node_modules
`cnpm install rimraf -g ``rimraf node_modules`

### 启动npm热重载

`nom start`

安装yarn

`npm install -g yarn`

### yarn配置

查看yarn的当前使用的镜像源
`yarn config get registry`

全局修改yarn镜像
`yarn config set registry https://registry.npm.taobao.org/`

如果出现任何问题，重新安装包就可以
