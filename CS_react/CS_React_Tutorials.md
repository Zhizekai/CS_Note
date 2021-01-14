# React 
> 配置react开发环境
## 创建项目
1.直接进入文件夹，打开powershell或者cmd运行这个命令：
```bash
npx create-react-app my-app
```
这条命令会自动下载所有的依赖包，如果没有安装react或create-react-app也会自动安装。
2.用webstorm打开那个文件夹，就可以看见项目。
## 配置webstorm的jsx模板
打开setting，找到添加模板
```javascript
import React, {Component} from 'react';

export default class ${NAME} extends Component {
    constructor(props) {
        super(props);
        this.state = {};
    }

    render() {
        return (
            <div ></div>
        )
    }
}
```

> 参考 ：https://www.jianshu.com/p/d906e183c83a
