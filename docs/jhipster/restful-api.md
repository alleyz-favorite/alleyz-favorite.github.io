## Restful API


### 1. 概念
Restful API就是符合Rest(Representational State Transfer)风格的API设计，是一种面向资源的设计。

### 2. 设计
#### 1. 版本号
设计Restfull API时最好是将API的版本号也放到URL中，这样比较直观，也可以将版本号放到请求头中。
```
https://api.example.com/v1/
```

#### 2. 路径
在Restfull API 设计中，每一个URI路径就代表了一种资源，所以在设计中URL中的资源表示应为名词，不要动词。
```
https://api.example.com/v1/zoos
```

#### 3. 动作
当我们需要对服务器上的资源进行操作时，也就是有所动作时，不要在URL上使用动词来体现，而是尽量通过HTTP请求的操作来表现操作类型。
```
GET: 从服务器获取资源
POST: 在服务器创建新的资源
PUT: 更新服务器上的资源(客户端提供所有信息)
PATCH: 更新资源(客户端只需提供更改字段的信息)
DELETE: 删除服务器上的资源
```

在设计API时，使用资源占位符的形式来表现资源。
```
# 获取特定ID的zoo
GET: /v1/zoos/ID
# 删除特定ID的zoo的某个动物
DELETE: /v1/zoos/ID/animals/ID
# 新增一个zoo
POST: /v1/zoos
# 修改特定ID的zoo的某个动物
PUT: /v1/zoos/ID/animals/ID
```

#### 4. 过滤信息
当我们请求的资源过多时，那么就需要我们对请求的资源进行过滤，无论是分页还是条件查询，都是过滤的一种。
```
?limit=10：指定返回记录的数量
?offset=10：指定返回记录的开始位置。
?page=2&per_page=100：指定第几页，以及每页的记录数。
?sortby=name&order=asc：指定返回结果按照哪个属性排序，以及排序顺序。
?animal_type_id=1：指定筛选条件
```

### 3. 为什么使用Rest
通过前面的介绍，对Restfull API 有了一定的了解，也可以看到这种设计风格，使得API的可读性非常强，便于理解，另外Restfull 强调了以资源为中心，规范了API设计的风格。

----------------------------------------------
参考资料：
1. [理解RESTful架构](http://www.ruanyifeng.com/blog/2011/09/restful.html)
2. [RESTful API 设计指南](http://www.ruanyifeng.com/blog/2014/05/restful_api.html)