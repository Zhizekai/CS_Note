# react配置proxy代理
## 简易配置
在packag.json添加如下配置：
![在这里插入图片描述](https://img-blog.csdnimg.cn/2021010509415299.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
配置完之后一定要**重启`npm start`那种的重启**

&emsp;&emsp;proxy这里面填写的是目的服务器的URL，之后的axios请求一定要请求当前项目所在服务器自身的URL，就像是自己请求自己，然后proxy会自动转发到对应的URL上面。
&emsp;&emsp;如下我当前项目的端口在3000，我axios就请求3000端口：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210105094417371.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
## 正规配置
### 1. 创建代理配置文件
在src下创建配置文件：`setupProxy.js`。文件位置是src/setupProxy.js
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210109172720796.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)


### 2.编写setupProxy.js配置具体代理规则：


```javascript
  const proxy = require('http-proxy-middleware')
   
   module.exports = function(app) {
     app.use(
       proxy('/api1/**', {  //api1是需要转发的请求(所有带有/api1前缀的请求都会转发给5000)
         target: 'http://localhost:5000', //配置转发目标地址(能返回数据的服务器地址)
         changeOrigin: true, //控制服务器接收到的请求头中host字段的值
         /*
         	changeOrigin设置为true时，服务器收到的请求头中的host为：localhost:5000
         	changeOrigin设置为false时，服务器收到的请求头中的host为：localhost:3000
         	changeOrigin默认值为false，但我们一般将changeOrigin值设为true
         */
         pathRewrite: {'^/api1': ''} //去除请求前缀，保证交给后台服务器的是正常请求地址(必须配置)
       }),
       proxy('/api2', { 
         target: 'http://localhost:5001',
         changeOrigin: true,
         pathRewrite: {'^/api2': ''}
       })
     )
   }
```
上面设置了/api 前缀的转发规则，就是转发必须前缀要带上/api, 例如 /api1/search/users?q=1
### 3. 重启服务器
### 4. 直接引用

```javascript

    sendReqFindUser = () => {
        console.log("发送axios请求");
        //需要在package.json里配置代理请求 "proxy": "https://api.github.com"
        axios.get("/api1/search/users?q=1", {
            headers: {"auth": "123"}
        }).then((response) => {
            console.log(response);
        }).catch((error) => {
            console.log(error);
        });
    };
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210106193239944.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)

## 最新正规配置
起因是因为在用yarn安装antd之后，`http-proxy-middleware`这个包被莫名的更新成1.X.X版本，导致出现proxy is not function这个报错，最终把问题解决。
最新的配置为：

```javascript
const {createProxyMiddleware}  = require("http-proxy-middleware");

module.exports = function(app) {
    app.use(
        createProxyMiddleware ("/api1/**", {
            target: "https://api.github.com",//跨域地址，目标地址
            changeOrigin: true,  //让服务器知道从哪来的
            pathRewrite:{'^/api1':''} //把api1 替换成空字符串
        })
    );
};
```
