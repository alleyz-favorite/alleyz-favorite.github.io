# jhipster 实体类生成以及服务间调度

> 前面我们介绍了如何使用jhipster自动创建项目，项目框架搭建好之后，就要开始内容填充了，即开发功能。功能开发实体类是必不可少的，本文主要介绍，如何使用jhipster生成实体类。

> JHipster通过 entity sub-generator 自动创建前后端相应代码。
> JHipster entity sub-generator 根据项目类型，和选项，自动创建相应代码（gateway和Monolithic application 会创建前后端代码，uaa,microservice创建后端代码）

## 在综合应用中生成实体类
> 以综合应用为例，其他类型应用生成步骤都是相同的。

1. 进入项目目录
使用命令创建
```
# author 是实体类的名称
yo jhipster:entity author
```

2. 填写实体类信息 
然后会显示选项，是否需要添加字段，以及字段的一些信息。
```
D:\workspace\jhipsterExmple\exmplemysql>yo jhipster:entity author

The entity author is being created.


Generating field #1

? Do you want to add a field to your entity? Yes
? What is the name of your field? name
? What is the type of your field? String
? Do you want to add validation rules to your field? No

================= Author =================
Fields
name (String)


Generating field #2

? Do you want to add a field to your entity? Yes
? What is the name of your field? age
? What is the type of your field? Integer
? Do you want to add validation rules to your field? No

================= Author =================
Fields
name (String)
age (Integer)


Generating field #3

? Do you want to add a field to your entity? No

================= Author =================
Fields
name (String)
age (Integer)


Generating relationships to other entities

? Do you want to add a relationship to another entity? Yes
? What is the name of the other entity? book
? What is the name of the relationship? book
? What is the type of the relationship? one-to-many
? What is the name of this relationship in the other entity? author

================= Author =================
Fields
name (String)
age (Integer)

Relationships
book (Book) one-to-many


Generating relationships to other entities

? Do you want to add a relationship to another entity? No

================= Author =================
Fields
name (String)
age (Integer)

Relationships
book (Book) one-to-many



? Do you want to use separate service class for your business logic? No, the REST co
ntroller should use the repository directly
? Do you want pagination on your entity? Yes, with pagination links

Everything is configured, generating the entity...

   create .jhipster\Author.json
   create src\main\resources\config\liquibase\changelog\20180208021756_added_entity_Author.xml
   create src\main\java\com\hollycrm\domain\Author.java
   create src\main\java\com\hollycrm\repository\AuthorRepository.java
   create src\main\java\com\hollycrm\web\rest\AuthorResource.java
   create src\test\java\com\hollycrm\web\rest\AuthorResourceIntTest.java
 conflict src\main\resources\config\liquibase\master.xml
? Overwrite src\main\resources\config\liquibase\master.xml? (ynaxdH)
```

> 然后会出现是否重新配置文件和webbapp中的文件，这里全部都选择是。

>实体生成成功之后，会发现在com.hollycrm.domain下会生成。

![image](http://note.youdao.com/favicon.ico)

> 然后生成实体类book，步骤以上面的相同。

**注意：由于author和book创建了关联关系，所以book实体必须生成，否则会报错**

如果生成的实体类有问题或者添加新字段，可以重新生成。

```
D:\workspace\jhipsterExmple\exmplemysql>yo jhipster:entity book

Found the .jhipster/Book.json configuration file, entity can be automatically generated!


The entity book is being updated.

? Do you want to update the entity? This will replace the existing files for this entity, all your custom code will be overwr
itten (Use arrow keys)
> Yes, re generate the entity // 重新生成实体
  Yes, add more fields and relationships // 添加新字段和关联关系
  Yes, remove fields and relationships
  No, exit // 删除字段和关系


```

> 然后，启动项目，访问首页可以看到，数据功能中添加了两个实体：

![image](http://note.youdao.com/favicon.ico)

选择一个实体类可以对他进行增删改查的操作。

![image](http://note.youdao.com/favicon.ico)

3. 过程中遇到的问题

> 在创建boot实体类时，author字段与关系实体类的名称重复，导致生成的author的实体类报错，类型不一致。

![image](http://note.youdao.com/favicon.ico)

![image](http://note.youdao.com/favicon.ico)

解决办法，通过添加新的字段和关系，重新修改即可。
```
yo jhipster:entity book

Found the .jhipster/Book.json configuration file, entity can be automatically generated!


The entity book is being updated.

? Do you want to update the entity? This will replace the existing files for this entity, all your custom code will be overwr
itten Yes, add more fields and relationships

================= Book =================
Fields
name (String)
author (String)
pubDate (LocalDate)


Generating field #4

? Do you want to add a field to your entity? No

================= Book =================
Fields
name (String)
author (String)
pubDate (LocalDate)


Generating relationships to other entities

? Do you want to add a relationship to another entity? Yes
? What is the name of the other entity? author
? What is the name of the relationship? au
? What is the type of the relationship? many-to-one
? When you display this relationship with Angular, which field from 'author' do you want to use? This field will be displayed
 as a String, so it cannot be a Blob id
? Do you want to add any validation rules to this relationship? No

================= Book =================
Fields
name (String)
author (String)
pubDate (LocalDate)

Relationships
au (Author) many-to-one

```

> 所以在字段命名和关联关系的处理上需要慎重考虑，尽量避免字段名称和关联的关系的实体类重名。
按照关系来说，book中的author字段可以不创建的。所以在创建实体的时候还是要看好看看学习一下实体关系。


## 微服务间相互调用
> jhipster 生成的微服务使用的是spring cloud，那什么是spring cloud呢？Spring Cloud是一系列框架的有序集合。它利用Spring Boot的开发便利性巧妙地简化了分布式系统基础设施的开发，如服务发现注册、配置中心、消息总线、负载均衡、断路器、数据监控等，都可以用Spring Boot的开发风格做到一键启动和部署。简单的说是分布式系统开发工具包。

下面通过一个简单的小例子，实现服务调用。
1. 准备服务
> 前面的笔记[window环境使用jhipster创建项目](./docs/jhipster/create_jhipster.md)中已经介绍了如何生成应用，这里不再做介绍
 - 注册中心
 - uaa 身份认证中心
 - 网关服务
 - 2个微服务应用
 - 总和应用服务
 启动注册中心、uaa、网关服务。

2. 如何将服务注册到注册中心

> 在创建的微服务项目的启动类中,我们可以看到@EnableDiscoveryClient注解，它的作用就是向服务中心注册。当启动项目时，在注册中心会看到启动的服务名称等信息。

![image](http://note.youdao.com/favicon.ico)

2. 通过网关调用服务

> ribbon是一个负载均衡客户端，可以很好的控制htt和tcp的一些行为。spring cloud 中使用ribbon来做负载均衡的。

> 这里我们创建名为msapp1（启动两次，端口分别为：8081、8084）、msapp2的微服务，也就是服务的提供者。

> 在微服务中创建一个controller,返回应用名称和端口信息。

```
@RestController
@RequestMapping("/app")
public class AppExmple {
    @Value("${server.port}")
    String port;
    @RequestMapping("/hi")
    public String home(@RequestParam String name) {
        return "hi "+name+",i am from port:" +port;
    }
}
```
> 然后启动微服务msapp1 和msapp2,注意msapp1 需要启动两次(使用idea用两个窗口打开，启动即可)，两次分别端口不同，用来模拟一个服务多个部署，测试负载匀衡。

> 启动成功后，会发现注册中心的app类别如下：
![image](http://note.youdao.com/favicon.ico)

> 访问网关页面http://localhost:8087/，可以看到如下信息，这里可以看到服务的实际ip地址以及端口号
![image](http://note.youdao.com/favicon.ico)

> 然后可以在地址然输入：http://localhost:8087/msapp1/app/hi?name=msapp1； 会发现页面会打印如下信息,如果一致刷新会发现端口号会发生改变，且是每次刷新端口都会发生改变。

```
# 首次访问结果
hi msapp1,i am from port:8081
# 刷新后结果
hi msapp1,i am from port:8084
```
> 网关通过ribbon实现了负载均衡，对msapp1服务轮流调用。

如何实现各应用之间的调度呢？下篇文章我们在继续讨论吧~~

*****
参考文章
1. [jhipster创建实体](https://jh.jiankangsn.com/ch1/entity.html)
2. [spring clound参考资料](http://blog.csdn.net/forezp/article/details/70148833)
