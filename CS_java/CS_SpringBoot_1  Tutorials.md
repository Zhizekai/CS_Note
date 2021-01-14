> 给自己提个醒

### 常用注解
`@RequestParam(value = "name") String string` 和 `@RequestParam String name`是一样的，`value`标注了接受的key值，如果不标注就自动使用变量的名称
```java
@Slf4j
@RestController
@RequestMapping("/t-booking")
public class TBookingController {

    @Autowired
    TBookingService tBookingService;

    // 所有预约记录
    @GetMapping(value = "/bookingList")
    public AjaxResponse bookingList(@RequestParam(value = "name") String string) {
        log.info("article:" + string);
        return AjaxResponse.success(string);

    }

}
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201102154923575.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70#pic_center)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20201102154439852.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201102154500383.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70#pic_center)


@RequestBody
使用这个必须要用post格式，要创建一个vo，vo里面必须要有@Data注解
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201102162609420.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70#pic_center)
使用的时候是这个样子，要使用PostMapping，对象的属性对应着
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201102162750860.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20201102162904232.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzMTY1Njg0,size_16,color_FFFFFF,t_70#pic_center)



mybatis-plus 
```xml
		<!--模版引擎-->
      	<dependency>
           <groupId>org.springframework.boot</groupId>
           <artifactId>spring-boot-starter-freemarker</artifactId>
       </dependency>


       <dependency>
           <groupId>mysql</groupId>
           <artifactId>mysql-connector-java</artifactId>
           <scope>runtime</scope>
       </dependency>

       <!--lombok工具类-->
       <dependency>
           <groupId>org.projectlombok</groupId>
           <artifactId>lombok</artifactId>
           <optional>true</optional>
       </dependency>

       <!--springboot测试类-->
       <dependency>
           <groupId>org.springframework.boot</groupId>
           <artifactId>spring-boot-starter-test</artifactId>
           <scope>test</scope>
           <exclusions>
               <exclusion>
                   <groupId>org.junit.vintage</groupId>
                   <artifactId>junit-vintage-engine</artifactId>
               </exclusion>
           </exclusions>
       </dependency>


       <!--解决jdk版本过高-->
       <dependency>
           <groupId>javax.xml.bind</groupId>
           <artifactId>jaxb-api</artifactId>
           <version>2.3.0</version>
       </dependency>
       <dependency>
           <groupId>com.sun.xml.bind</groupId>
           <artifactId>jaxb-impl</artifactId>
           <version>2.3.0</version>
       </dependency>
       <dependency>
           <groupId>com.sun.xml.bind</groupId>
           <artifactId>jaxb-core</artifactId>
           <version>2.3.0</version>
       </dependency>
       <dependency>
           <groupId>javax.activation</groupId>
           <artifactId>activation</artifactId>
           <version>1.1.1</version>
       </dependency>

       <!-- hutool工具类-->
       <dependency>
           <groupId>cn.hutool</groupId>
           <artifactId>hutool-all</artifactId>
           <version>5.3.3</version>
       </dependency>


       <!--mybatis plus -->
       <dependency>
           <groupId>com.baomidou</groupId>
           <artifactId>mybatis-plus-boot-starter</artifactId>
           <version>3.2.0</version>
       </dependency>
       <dependency>
           <groupId>com.baomidou</groupId>
           <artifactId>mybatis-plus-generator</artifactId>
           <version>3.2.0</version>
       </dependency>

       <!--mp代码生成器-->
       <dependency>
           <groupId>com.baomidou</groupId>
           <artifactId>mybatis-plus-generator</artifactId>
           <version>3.2.0</version>
       </dependency>
```

