# React 攻略

## 1.key在最外层，如下就不行
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210102163804723.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
必须要这样：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210102163829981.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
## 2.出现如下报错：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210104094653452.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
就是因为返回的是一个函数导致的，而没有调用这个函数。因为我写了这样一个函数：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210104094850811.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
这个只是一个函数，我没有用立即执行函数去执行它
## 3.在react中使用mockjs
先安装mockjs，然后在项目中写一个mock的js代码，其实代码写在哪都行，那就先举个如下的例子：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210104111732696.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)

```javascript
import Mock from 'mockjs';

const Random = Mock.Random;

// mock需要给三个参数,url(与axios请求是传的url一致,我这个是本地启动的项目就直接用本地域名了)
// 请求类型: get post...其他看文档
// 数据处理函数,函数需要return数据
Mock.mock('http://localhost:8081/test/city', 'get', () => {
    let citys = [];
    for (let i = 0; i < 10; i++) {
        let obj = {
            id: i + 1,
            city: Random.city(),
            color: Random.color()
        };
        citys.push(obj);
    }
    return {cityList: citys};
});
// post请求,带参数,参数会在data中返回,会返回url,type,body三个参数,可以把data打印出来看看
Mock.mock('http://localhost:8081/test/cityInfo', 'post', (data) => {
    // 请求传过来的参数在body中,传回的是json字符串,需要转义一下
    const info = JSON.parse(data.body);
    return {
        img: Random.image('200x100', '#4A7BF7', info.name)
    };
});
```
然后在入口文件里引用一下
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210104112103602.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
然后发送mock当中拦截的url发送请求，mock就会自动拦截请求返回对应的数据，发送请求如下所示：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210104112208810.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
## 4. 给axios添加请求头
第一种方法：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210104125754838.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
这种方法就直接添加，没有任何花里胡哨的东西。
第二种方法就是请求和响应拦截器的方式，需要给axios添加一个全局配置，定义请求拦截器和响应拦截器：

```javascript
import axios from 'axios';  // 该处引入axios模块

// 构建axios实例
const axiosInstance = axios.create({
    // baseURL: process.env.BASE_API,  // 该处url会根据开发环境进行变化（开发/发布）
    baseURL: '',
    timeout: 10000  // 设置请求超时连接时间
});
/*请求拦截器*/
axiosInstance.interceptors.request.use(
    config => {
        console.log(config);  // 该处可以将config打印出来看一下，该部分将发送给后端（server端）
        config.headers.token = 'token2222222';
        return config;  // 对config处理完后返回，下一步将向后端发送请求
    },
    error => {  // 当发生错误时，执行该部分代码
        console.log(error); //调试用
        return Promise.reject(error);
    }
);
/*响应拦截器*/
axiosInstance.interceptors.response.use(
    response => {  // 该处为后端返回整个内容
        const res = response.data;  // 该处可将后端数据取出，提前做一个处理
        if ('正常情况') {
            return response;  // 该处将结果返回，下一步可用于前端页面渲染用
        } else {
            alert('该处异常');
            return Promise.reject('error');
        }
    },
    error => {
        console.log(error);
        return Promise.reject(error);
    }
);
export default axiosInstance;

```
写在这个位置：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210104150538238.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
使用的时候如下调用即可：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210104150624447.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)

## 5.出现如下报错
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210104130744142.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
说明前端请求头里不能有中文
> 参考 https://www.cnblogs.com/arealy/p/13566884.html




## 7. react引入bootstrap

在项目更目录的public的文件夹中的index.html文件中引入：![在这里插入图片描述](https://img-blog.csdnimg.cn/20210105125204123.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
引入代码：

```html
<!-- 最新版本的 Bootstrap 核心 CSS 文件 -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@3.3.7/dist/css/bootstrap.min.css"
          integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous">

    <!-- 最新的 Bootstrap 核心 JavaScript 文件 -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@3.3.7/dist/js/bootstrap.min.js"
            integrity="sha384-Tc5IQib027qvyjSMfHjOMaLkfuWVxZxUPnCJA7l2mCWNIpG9mGCD8wGNIcPD7Txa" crossorigin="anonymous">
    </script>
```
这一部分的代码是采用CDN加速的，就是看到样式需要联网。
> 参考：bootstrap官网 ：https://v3.bootcss.com/getting-started/

## 8. 路由前缀导致样式丢失
在项目的public中的index下引入自定义的文件需要在之前写%PUBLIC_URL%，这个指向网站的根目录，根目录就是public文件夹
。

```html
<!--引用public下的文件时候必须前面加 %PUBLIC_URL%-->
<link rel="stylesheet" href="%PUBLIC_URL%/bootstrap.css"/> 
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210106084044100.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
2.或者可以把路由改成hashrouter，但一般都不该城hashrouter

## 9. 路由跳转不刷新的问题
前端这种代码：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210106093757417.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
问题是点击home时候它并不会高亮：
![问题代码](https://img-blog.csdnimg.cn/20210106094127245.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
并且我获取了当前页面的URL：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210106094229366.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)经过我的分析，其实这是因为NavLink路由跳转的时候并没有重新挂载并渲染页面，所以不会执行render函数，所以里面获取当前URL的js函数也就不会被执行。

其他导航可以高亮的原因是因为我再里面写了`this.setstate()`函数，导致了当前组件状态的改变，react组件状态改变了就必须重新挂载并且渲染，所以会执行render函数，所以会得到当前页面的path。

要想解决这个问题，可以让路径和组件状态绑定，也可以用NavLInk里active的属性，方法有很多，可以很笨的解决，顶多就多渲染几回。

其中最优的解决方案是：
1.把`router`套在最外层，就是`React.DOM`这个函数里面，挂载函数的那一层：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210106100531537.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
2.内层组件`<RouterMain/>`使用`withRouter`包裹：
![包裹](https://img-blog.csdnimg.cn/20210106100640864.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210106100706770.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
3.然后就能轻松在组件里取到react router给它传入的各种属性
![获取属性](https://img-blog.csdnimg.cn/20210106100950233.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
withRouter用在不是路由组件里，非路由组件如果想取得路由信息，就要用withRouter包裹。

## 10. redux-thunk
1.安装
2.在store里引入
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210107133939147.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
3.在actions里使用异步函数：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210107134008191.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
reducers自己会处理这个函数
4.在组件里使用：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210107134118412.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)








