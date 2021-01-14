@[toc]
### Vue

本人学习Vue的时候有些js也有漏洞,于是连vue和js一起学一下,所谓less is more 和talk is cheap, show me the code,所以本文当中代码将占很多部分,文字叙述将很少.

```javascript
//解构赋值快速把对象中的变量提取出来
const aa = {a:12,b:23};
const {a:bb} = aa;
aa.a = 22222;
console.log(bb);
console.log(aa.a);
```
排序

```javascript
filterPersons() {
                //this.persons 是引用类型，直接赋值是传的地址，所有得先结构再赋值
                let afterFilterPersons = [...this.persons];
                if(this.orderType) {

                    //解构赋值快速把对象中的变量提取出来
                    const aa = {a:12,b:23};
                    const {a:bb} = aa;
                    aa.a = 22222;
                    console.log(bb);
                    console.log(aa.a);

                    console.log("开始排序");
                    // const dd = this.orderType
                    //回调函数必须是箭头函数，this指向本实例
                    afterFilterPersons.sort((p1,p2) => {
                        // console.log(this.orderType)
                        if(this.orderType===1) { // 降序
                            console.log("降序");
                            return p2.age-p1.age
                        } else { // 升序

                            console.log("升序");
                            return p1.age-p2.age
                        }

                    })
                }else {
                    console.log("没有进行排序")
                }

                return afterFilterPersons;
            }
```

### axios
为了解决跨域问题,代理请求
```javascript
dev: {

    // Paths
    assetsSubDirectory: 'static',
    assetsPublicPath: '/',
    proxyTable: {
      '/api': { // 匹配所有以 '/api'开头的请求路径
        target: 'http://localhost:4000', // 代理目标的基础路径，请求接口的地址，
        // secure: false,  // 如果是https接口，需要配置这个参数
        changeOrigin: true, // 支持跨域
        pathRewrite: {// 重写路径: 去掉路径中开头的'/api',
          '^/api': ''
        }
      }
    },
```
>  pathRewrite:  这个字段配置''^/api': ' '的意思在于后端接口实际上是http://localhost:4000/index_category，但是请求的时候要写成http://localhost:4000/api/index_category,他会把发起的/api字段替换成一个空字符串
### vuex
名字内容必须一致,一个也不能差![在这里插入图片描述](https://img-blog.csdnimg.cn/20200704161556293.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
