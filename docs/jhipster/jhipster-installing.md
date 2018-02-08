
# windows 环境安装jhipster

## 环境准备

> 使用jhipster 需要如下配置环境：
- jdk 
- maven 
- git 
- mysql
- node.js
- compass
- yeoman
- phantomjs
- yarn
- jhipster

## 安装过程
> 这里对jdk、maven、mysql的安装不做介绍。

**1.node.js 和npm 安装**

 > 官网下载node js[下载地址](https://nodejs.org/en/),
[安装教程](https://segmentfault.com/a/1190000005602881)
安装成功后可一查看版本

```
node -v
npm -v
```
> 使用node可以进入控制台,可以打印,此步骤是测试node可以跳过。

```
C:\Users\160823b>node
> console.log("holle ,this is node.js")
holle ,this is node.js
undefined
>
# 输入.exit 可以退出node 命令行
```

- **配置npm的全局模块存放路径以及cache**

 ```
 npm config set prefix “D:\Program Files (x86)\nodejs\node_global”
 npm config set cache “D:\Program Files (x86)\nodejs\node_cache”
 ```

- **选择安装express模块在命令行中输入**

 ```
 npm install express -g
 ```
 
- **成功后配置node-path**

NODE_PATH=D:\Program Files (x86)\nodejs\node_global\node_modules

- **然后全局安装 Angular CLI** 

> jhipster 中默认时候angular js
[安装步骤](http://blog.csdn.net/zhy13087344578/article/details/60745667)

```
#指定淘宝镜像
npm config set registry https://registry.npm.taobao.org 
#安装typescript
npm install -g typescript typings  
#安装cli 1.6.6版本
npm install -g @angular/cli
```

**2.安装git**
> jhipster自动构建时会用到git  
[安装教程](https://www.cnblogs.com/ximiaomiao/p/7140456.html)

**3.compass安装** 
> **安装yeoman之前需要安装Ruby 和compass** Compass 是一个用来开发 CSS 的工具，yeoman启动时需要依赖这个工具    
  
[windows下安装sass和compass教程](http://blog.csdn.net/dw1067061570/article/details/54947106)

安装成功后
**配置环境变量：D:\Program Files (x86)\Ruby\bin**

**ruby安装成功后安装compass:**
 
使用命令安装有四个安装包无法下载，所以本地安装需要下载4个文件：SASS，Chunky_png，Fssm和Compass，下载地址分别为：
- SASS.gem: http://rubygems.org/downloads/sass-3.2.13.gem
- Chunky_png.gem: http://rubygems.org/downloads/chunky_png-1.2.9.gem
- Fssm.gem: http://rubygems.org/downloads/fssm-0.2.10.gem
- Compass.gem: http://rubygems.org/downloads/compass-0.12.2.gem

> 将这4个文件放在ruby的安装根目录下，如我安装在D:\Program Files (x86)\Ruby，然后打开控制台切换到ruby的安装目录
执行以下命令即可

```
gem install sass
sass -v

gem install compass
gem install fssm
gem install chunky_png
# 以上三个都安装成功，查看compass版本才会成功
compass -v
# 卸载
gem uninstall compass
```

> **注意：这里四个文件需要分别执行否则安装失败，如果安装失败可以将已经安装的卸载重新安装即可，安装教程里只执行了一个命令，所以在这个地方重新安装了三次才成功。**

**4. yeoman**  
[YEOMAN安装教程](http://blog.csdn.net/u012586558/article/details/52923358)
执行以下命令即可：

```
# yeoman
npm install -g yo
# bower
npm install -g bower
# grunt
 npm install -g grunt-cli 
/npm install -g gulp
```

> 安装成功后配置环境变量，yo.cmd所在路径。D:\Program Files (x86)\nodejs\node_global添加到path中


**5. phantomjs 安装**
> 　PhantomJS是一个基于webkit的JavaScript API。它使用QtWebKit作为它核心浏览器的功能，使用webkit来编译解释执行JavaScript代码

**下载地址：https://pan.baidu.com/s/1o9sGsOU 提取码：dovx**

> 解压后，配置环境变量。在path中添加phantom的解压路径。D:\phantomjs\bin
配置成功后可以查看版本号

```
phantomjs --version
```

**6. 安装yarn**

> jhipster 生成微服务应用是需要用到yarn。他是快速、可靠、安全的依赖管理工具。  

> [官网](https://yarnpkg.com/en/docs/install)下载yarn，安装成功，配置环境变量：
path添加：D:\Program Files (x86)\Yarn\bin

**7. 安装jhipster**

```
npm install -g generator-jhipster
```

到此jhipster就安装成功了，然后就可以使用jhipster开启自动生成应用的神奇之旅啦！下一篇笔记会详细介绍如果使用jhipster自动生成应用^-^.