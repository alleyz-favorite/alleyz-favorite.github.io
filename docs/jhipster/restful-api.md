#  RESTful API 


## 1. 什么是REST
### 1. REST含义  
REST 的全称是Representational State Transfer，意思是“表现成状态转化”，"表现层"其实指的是"资源"（Resources）的"表现层"。如果客户端想要操作服务器，必须通过某种手段，让服务器端发生"状态转化"（State Transfer）。而这种转化是建立在表现层之上的，所以就是"表现层状态转化"。它是所有Web应用都应该遵守的架构设计指导原则。

面向资源是REST最明显的特征，对于同一个资源的一组不同的操作。资源是服务器上一个可命名的抽象概念，资源是以名词为核心来组织的，首先关注的是名词。REST要求，必须通过统一的接口来对资源执行各种操作。对于每个资源只能执行一组有限的操作。（7个HTTP方法：GET/POST/PUT/DELETE/PATCH/HEAD/OPTIONS）

### 2. HTTP四种基本操作
- GET ：获取资源
- POST：创建资源
- PUT： 更新资源
- DELETE： 删除资源


## 2. RESTful API
RESTful API是指符合REST的API。HTTP协议就是属于REST架构的设计模式。

### 1. API 路径规则
API网址中不能有动词，只能有名称，且都是对照数据库表名对应或者具体功能。

### 2. 过滤信息
如果记录数量很多，服务器不可能都将它们返回给用户。API应该提供参数，过滤返回结果。

常见的参数。
- ?limit=10：指定返回记录的数量
- ?offset=10：指定返回记录的开始位置。
- ?page=2&per_page=100：指定第几页，以及每页的记录数。
- ?sortby=name&order=asc：指定返回结果按照哪个属性排序，以及排序顺序。
- ?producy_type=1：指定筛选条件

### 3. API 版本
实际应用中，每个应用都是有版本的。API也是有版本的。
通常会将API的版本放到URL中，如https://api.example.com/v{n}/；另一种方式是在HTTP请求头信息的Accept字段中进行区分。

```
　Accept: vnd.example-com.foo+json; version=1.0

　Accept: vnd.example-com.foo+json; version=1.1

　Accept: vnd.example-com.foo+json; version=2.0
　　
```
### 4. API传入参数
传入参数有4中类型

- 地址栏参数
    - RESTful 地址栏：/api/v1/product/011 011是查询参数；
    - get方式的查询字符串
- 请求body数据
- cookie
- request header

cookie和header 一般都是用于OAuth认证的2种途径。

### 5. 返回数据格式 
数据返回结果使用JSON格式

```json
{
status:0, 
data:{}||[], 
msg:’’ 
}
```

status: 接口执行成功或者失败
data: 返回期望的数据
msg: 如果执行的结果是失败，返回失败信息


*********************************************************
参考文献

1. [理解RESTful架构](http://www.ruanyifeng.com/blog/2011/09/restful.html)
2. [API 接口开发规范](https://www.cnblogs.com/xiezhi/p/6434812.html)
