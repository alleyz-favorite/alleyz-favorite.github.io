# jhipster项目生成

## jhipster生成应用类型介绍
> 安装jhipster之后就可以使用jhipster生成应用了，jhipster可以生成四种类型的应用

- Monolithic application (recommended for simple projects) 总和应用
- Microservice application 微服务应用
- Microservice gateway 微服务网管
- JHipster UAA server (for microservice OAuth2 authentication) jhipster身份验证中心(uaa)服务

> ==jhipster使用的数据这里我们使用mysql数据库。所以如果没有mysql数据库，再生成文件之前请先安装mysql数据库。==  
==注意：本文所述都是在window环境下创建的项目==

## 创建应用

### 1.综合应用
> 打开dos窗口，进入存放项目的文件目录，如果没有可以创建（这里可以用命令创建，也可以创建好之后直接进入目录下。）

```
# 创建目录
mkdir exmple
cd exmple

```
1. 执行命令，选择需要的配置

```
yo jhipster
```
> 执行上面的命令后，如下图选择应用类型，这里我们选择综合应用类型  

![image](./docs/images/create-project-1.png)

> 选择国际化时可以选择两种语言，这里选择中文和英文

![image](https://github.com/hollycrm-td/hollycrm-td.github.io/blob/docs/images/create-project-2.png)


![image](https://github.com/hollycrm-td/hollycrm-td.github.io/blob/qianxm/docs/images/create-project-3.png)

> 然后选择测试选择，这里选择gatling（压力测试）

![image](https://github.com/hollycrm-td/hollycrm-td.github.io/blob/qianxm/docs/images/create-project-4.png)


> 然后继续选择，如下图，已经选择完所有的选项，正在生成项目

![image](https://github.com/hollycrm-td/hollycrm-td.github.io/blob/qianxm/docs/images/create-project-5.png)

> 项目生成成功之后，会显示如下如，生成成功的标识，并说明如何启动项目。

 ![image](https://github.com/hollycrm-td/hollycrm-td.github.io/blob/qianxm/docs/images/create-project-6.png)
 
> 修改配置文件中关于mysql数据库的配置，修改成自己的配置，如果没有数据库可以创建新的数据库
  ![image](https://github.com/hollycrm-td/hollycrm-td.github.io/blob/qianxm/docs/images/create-project-7.png)

> 修改完配置文件之后，执行命令启动服务

```
mvn spring-boot:run
```
> 启动成功后访问，http://localost:8080/
登录用户名和密码均为admin

![image](https://github.com/hollycrm-td/hollycrm-td.github.io/blob/qianxm/docs/images/create-project-8.png)
 
### 2. 微服务
> 创建微服务需要使用jhipster的注册中心，否则应用无法使用。刚开始创建项目时，没有注意到这一点，导致创建的任务，启动时报错。

#### 1.注册中心
> jhipster已经提供可注册中心的服务，直接去[github下载](https://github.com/jhipster/jhipster-registry.git)到本地，编译使用即可。

> 使用idea打开项目，执行以下命令，在本地启动registry

```
mvn.cmd -Pdev,webpack; // mvn.cmd 默认使用的是.m2的配置文件
# 如果在idea中打开项目，可以使用如下命令
mvn -Pdev,webpack;
yarn && yarn start;

```

> **注意：编译过程中遇到的问题，如果直接运行
mvn -Pdev,webpack 时会出现空白页问题，可以先执行yarn && yarn start命令，再执行mvn -Pdev,webpack即可解决。之后再启动项目时，直接运行mvn -Pdev,webpack命令即可。**

> 启动成功后，访问http://localhost:8761,默认的登录密码和用户都是admin，登录成功后可以看到如下界面，因为没有应用启动，所以app那里是空的。

![image](https://github.com/hollycrm-td/hollycrm-td.github.io/blob/qianxm/docs/images/create-project-9.png)

#### 2. 微服务身份验证中心（UAA）
> 使用jhipster创建uaa应用步骤
和创建综合项目类似，创建目录，然后执行命令选择需要的选项生成即可。
```
 yo jhipster
```
> 选择Uaa服务
![image](https://github.com/hollycrm-td/hollycrm-td.github.io/blob/qianxm/docs/images/create-project-10.png)
> 然后继续选择其他的选项，如下图

![image](https://github.com/hollycrm-td/hollycrm-td.github.io/blob/qianxm/docs/images/create-project-11.png)

> 等待项目生成，生成成功后，如下图
![image](https://github.com/hollycrm-td/hollycrm-td.github.io/blob/qianxm/docs/images/create-project-12.png)

> 修改mysql配置
![image](https://github.com/hollycrm-td/hollycrm-td.github.io/blob/qianxm/docs/images/create-project-13.png)

> 然后执行命令启动应用
```
mvn spring-boot:run
```
**注意：一定要先启动注册中心，否则会报错**
启动成功后可以在注册中心中看到，uaa应用。
![image](https://github.com/hollycrm-td/hollycrm-td.github.io/blob/qianxm/docs/images/create-project-14.png)

#### 3. 微服务网关
```
yo jhipster
```
> 与之前的项目生成步骤类似，选择网管服务
![image](https://github.com/hollycrm-td/hollycrm-td.github.io/blob/qianxm/docs/images/create-project-15.png)

> 然后选择相应的选择
![image](https://github.com/hollycrm-td/hollycrm-td.github.io/blob/qianxm/docs/images/create-project-16.png)

> 生成成功后，修改mysql配置
![image](https://github.com/hollycrm-td/hollycrm-td.github.io/blob/qianxm/docs/images/create-project-13.png)
> 启动服务
```
mvn spring-boot:run
```
> 启动成功后，在注册中心中也可以看到启动成功的网关应用。
![image](https://github.com/hollycrm-td/hollycrm-td.github.io/blob/qianxm/docs/images/create-project-17.png)

> 可以访问http://localhost:8080,这里的端口号是在选择选项过程中可配置
![image](https://github.com/hollycrm-td/hollycrm-td.github.io/blob/qianxm/docs/images/create-project-18.png)

#### 4. 微服务应用
> 微服务应用的创建和网管服务的创建步骤基本一致
执行命令：
```
yo jhipster
```
> 选择微服务应用
![image](https://github.com/hollycrm-td/hollycrm-td.github.io/blob/qianxm/docs/images/create-project-19.png)
> 然后选择相应的选择
![image](https://github.com/hollycrm-td/hollycrm-td.github.io/blob/qianxm/docs/images/create-project-21.png)

![image](https://github.com/hollycrm-td/hollycrm-td.github.io/blob/qianxm/docs/images/create-project-20.png)

> 生成成功后，修改mysql配置
![image](https://github.com/hollycrm-td/hollycrm-td.github.io/blob/qianxm/docs/images/create-project-22.png))
> 启动服务
```
mvn spring-boot:run
```
> 启动成功后，在注册中心中也可以看到启动成功的网管应用。
![image](https://github.com/hollycrm-td/hollycrm-td.github.io/blob/qianxm/docs/images/create-project-23.png))

> 可以访问http://localhost:8081,这里的端口号是在选择选项过程中可配置


==注意：关于端口问题，在选择端口时一定到确保端口没有被占用，否则项目启动是会报错==
![image](https://github.com/hollycrm-td/hollycrm-td.github.io/blob/qianxm/docs/images/create-project-24.png)

如果出现端口被占用情况，可以在配置applicatio-dev.yml文件中修改。
