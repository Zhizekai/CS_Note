@[toc]
## 参考文档
[spring boot 2.x](https://www.kancloud.cn/hanxt/springboot2/1492077)
[Spring Security-JWT-OAuth2一本通(基于SpringBoot2.0)](https://www.kancloud.cn/hanxt/springsecurity)
## 名词解释
[(PO,VO,TO,BO,DAO,POJO)分别是指什么](https://blog.csdn.net/weixin_42323802/article/details/82669637)
控制层(controller-action)，业务层/服务层( bo-manager )，实体层(po-entity)，dao(dao)，

**PO（bean、entity等命名）**： 
&emsp;&emsp;Persistant Object持久对象，数据库表中的记录在java对象中的显示状态，最形象的理解就是一个PO就是数据库中的一条记录。好处是可以把一条记录作为一个对象处理，可以方便的转为其它对象。

**POJO（POJO是一种概念或者接口，身份及作用随环境变化而变化）** ：
&emsp;&emsp;POJO有一些Private的参数作为对象的属性。然后针对每个参数定义了get和set方法作为访问的接口，Plain Ordinary Java Object简单Java对象，即POJO是一个简单的普通的Java对象，它不包含业务逻辑或持久逻辑等，但不是JavaBean、EntityBean等，不具有任何特殊角色和不继承或不实现任何其它Java框架的类或接口。POJO对象有时也被称为Data对象，大量应用于表现现实中的对象。 一个POJO持久化以后就是PO。直接用它传递、传递过程中就是DTO
&emsp;&emsp;直接用来对应表示层就是VO 

**DAO（Data Access Object数据访问对象**）：
&emsp;&emsp;这个大家最熟悉，和上面几个O区别最大，基本没有互相转化的可能性和必要.
主要用来封装对数据库的访问。通过它可以把POJO持久化为PO，用PO组装出来VO、DTO，
就是用DAO来对数据库进行操作

**Impl** ：
&emsp;&emsp;定义的接口

## 部署到服务器
1. 本地打成war包
2. 放到服务器的`/www/server/tomcat/webapps` 目录下,文件位置为`/www/server/tomcat/webapps/boot-launch.war` 
3. 运行tomcat
4. 访问tomcat的接口,默认是8080,springboot当中yml配置文件的`port` 项不起作用


## maven
阿里镜像配置

```xml
 <mirror>
    <id>nexus-aliyun</id>
	<mirrorOf>central</mirrorOf>
	<name>Nexus aliyun</name>
	<url>http://maven.aliyun.com/nexus/content/groups/public</url>
  </mirror>
```

## Postman 

想看console就点左下角那个
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200611112347895.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)


&emsp;&emsp;从cookie和响应中获取值,然后存到环境变量里面,在别的接口的地方直接用.
&emsp;&emsp;从cookie和响应中获取值,然后存到环境变量里面如下
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200611173101875.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
```javascript
pm.test("jwt", function () {
    var jsonData = pm.response.json();
    console.log(jsonData);
    pm.environment.set("jwttoken",jsonData.data);
    
    //下面两种方式都能从cookie中获取到值,推荐使用第二个,因为那是最新的
    var Cookies = postman.getResponseCookie('XSRF-TOKEN').value;
    var Cookie = pm.cookies.get('XSRF-TOKEN');
    
    console.log(Cookie);
    console.log(co);
    pm.environment.set("CSRF-TOKEN",Cookies);
});
```
在同一个环境下可以直接使用
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200611173648466.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
### idea
application context配置的问题看[这里](https://blog.csdn.net/qq_36666651/article/details/78509393)
#### 方法注释配置
自定义javadoc 输出：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201121141049140.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70#pic_center)

在groups 里新建一个live templates，如下图所示
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201121141128157.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70#pic_center)
将新建的templates起名为`*`，没错就得叫 `*`，这样才能起作用，

templates text里填这个

```java
*
 * 
 * $params$
 * @return $returns$
 * @author zhizekai
 * @describe Talk is cheap,show me the code
 * @date $date$ $time$
 */
```
然后点edit variables，设置这几个variables的expression，returns ，data，time照着填就完了。最上面的params看下面
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201121141430455.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70#pic_center)
params中的expression填这个

```groovy
groovyScript("
	def result='';  
	def params=\"${_1}\".replaceAll('[\\\\[|\\\\]|\\\\s]', '').split(',').toList();   
	for(i = 0; i < params.size(); i++) {   	
		if(i!=0)result+= ' * ';    	
		result+='@param ' + params[i] + ' ' + params[i] + ((i < (params.size() - 1)) ? '\\n' + '\\t' : '');   
	};    
	return result", methodParameters())
```


然后保存，点下面这个，将它的作用范围设定为everywhere。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201121141259434.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70#pic_center)

如果上面的设置不起作用的话，别忘了查看这个默认输入的按钮
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210110172216586.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)

其中有些javadoc tags是个人自定义的，不是sun公司默认的，idea会提示让你加进新的tags里，当然想删除也是可以的。
删除定义javadoc tags
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201121140944694.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70#pic_center)

> 参考文档 
> [IDEA Wrong tag describe add  to custom tags 移除自定义的javadoc tags](https://blog.csdn.net/coder_knight/article/details/83827994)
> [idea自动生成方法注释（含参数及返回值）](https://blog.csdn.net/yuruixin_china/article/details/80933835)
> https://www.cnblogs.com/mylocalhost/p/9697402.html

#### 颜色
如果文件名的颜色变得乱七八糟,mac下就把
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020060613063014.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
这里面的colors文件夹删了就行了

为了让代码里的变量名的颜色都不一样,做如下设置,这样看起来更舒服
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200617170019152.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)

#### 快捷键
1.快速字符串大小转换 `command` + `shift` + `U`
2.快速折叠代码 `command` + `-`,减号
3.返回上一步,也就是函数按`command` 跳转之后返回到上一个函数
4.`command` + `option` + `<-` 方向键左键

设置shortcut,直接使用`command` + `,` 调出设置界面,然后直接搜索comment
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200607144558541.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
把这个comment with block comment 的short cut 设置成 `option` + ` command ` + `/`

快速给返回值生成变量
Mac：`option` + `command` + `v`
windows：`ctrl` + `alt` + `v`
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020062809420929.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
快速重写父类方法 `control` + `o`
### 小问题和配置
springboot热部署
pom.xml
```xml
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-devtools</artifactId>
   <scope>runtime</scope>
   <optional>true</optional>
</dependency>
```
application.yml
```yaml
spring:
  # 热启动的设置
  devtools:
    restart:
      # 设置热部署生效
      enabled: true
      # 设置重启的目录
      additional-paths: src/main/java
```

在项目配置完之后还需要在idea里配置才能生效,具体来说是如果这个没配置,它还是会热重启但就是代码没有改动
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200628114414178.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)

---
发行版本错误
如果出现不支持发行版本5,就把下面这几样都弄成一样的,点File->project structure
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200611200608758.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200611200622365.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020061120064541.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)

idea配置tomcat
application server就是配置外部tomcat的根目录,下图的URL在下面需要注意
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200616104838773.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
根目录如下
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200616105020546.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
这个application context要和上面的URL要一致,最好直接根目录
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200616105140350.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
### Spring Security
如果出现登陆了还是403的话就是权限没设置好,在配置里设置如下,下面是静态资源的访问,就是不需要登陆就能访问
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200603091119377.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)

```java
 /**
     * 静态资源不需要权限
     * @param web web
     */
    @Override
    public void configure(WebSecurity web) {
        //将项目中静态资源路径开放出来
        web.ignoring()
           .antMatchers( "/css/**", "/fonts/**", "/img/**", "/js/**",
                   "/**/*.css",
                   "/**/*.js",
                   "/swagger-ui.html",
                   "/rest/*",  //开放restful接口，如果没有这个即使登陆了也访问不了接口
                   "/web","/webjars/**",
                   "/swagger-resources/**",
                   "/v2/**",
                   "/favicon.ico");
    }
```
如果资源需要登陆访问,就用如下方法

cookie的安全性,设置了httponly的cookie从js脚本就完全取不到值了,提升了安全性
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200603191825991.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70)
### redis-shiro

整合这两个东西先引入依赖,这东西应该是shiro和redis的合体

```xml
<!--shiro-->
<dependency>
    <groupId>org.crazycake</groupId>
    <artifactId>shiro-redis-spring-boot-starter</artifactId>
    <version>3.2.1</version>
</dependency>
```
然后配置redis数据源,shiro-redis顶头写,前面没有空格,在里面填入相应的redis端口和密码,redis设定对外访问的时候强制要有密码.具体配置看[这个依赖的配置说明](https://github.com/alexxiyang/shiro-redis/tree/master/docs)

```yaml
shiro-redis:
  enabled: true
  redis-manager:
    host: 106.15.95.26:6379
    password: zzkceo
```
然后就看[这篇文章](https://juejin.im/post/5ecfca676fb9a04793456fb8#heading-2)写shiro的配置把


