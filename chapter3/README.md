# 第三章 创建一个新的用户展示层

在此架构下，所有业务处理均全部集中于后台服务层，在用户使用层，用户可以利用多种技术手段通过调用后台服务层提供的访问接口来获得信息服务。目前已经开发的展示层范例包括：GUI（Java开发）、Web（Java开发）、Mobile（基于IonicFramework实现），后面的章节将逐一描述。

准备相关开发环境：

1、安装maven，并设置好settings.xml，配置库中已经提供3.x版本，可直接使用。

2、安装NodeJS环境

3、安装android模拟器

4、如果需要编写文档，需要安装gitbook edit（本文档就是采用gitbook结合Markdown编写）

5、安装svn客户端

6、如果要加入gitbook的在线书写团队，请安装git客户端，并注册github和gitbook的账号，然后在本地环境下安装gitbook工具。如果要发布最新的内容，请先确定把所有内容已经同步到github，然后在书籍的工程目录下，第一次需要安装发布工具（以后就不需要了），执行的命令如下

```bash
npm install -g gitbook  
npm install gulp gulp-gh-pages

```

然后再执行下列命令

```bash
gitbook build
gulp publish

```

执行完毕后，就可以在github网站上看到最新编写的文档了。网址是：[https:\/\/lynnhawk.github.io\/pthinkbook\/index.html](https://lynnhawk.github.io/pthinkbook/index.html)

由于所有客户端都需要通过clientapi来与服务层进行通讯，因此所有的java工程需要记得引入api。maven的引入方式如下：

```xml

<dependency>
 <groupId>penghaiyu.cloudapp.client</groupId>
 <artifactId>clientapi</artifactId>
 <version>1.0-SNAPSHOT</version>
</dependency>


```

该插件有一个配置文件，名称为server.properties，记得配置并放入classpath中即可。配置文件范例如下：

```java

#服务器URL
AppServerURL=PthinkCloudAppListener:default -h 127.0.0.1 -p 9701 -t 3000
serverId=PthinkCloudAppListener
servers=127.0.0.2:9701:0,115.159.64.16:9701:0

#服务器报文
app.MessageSizeMax=10240
app.ThreadPool.Server.Size=50
app.ThreadPool.Server.SizeMax=100

#缺省报文模板
packet_default={{},"DATA":{"opttype":"{}","pager":{"pageNo":{},"pageSize":{}},"params":{"entity":{}}}}}
packet_header="CMD":{"appver":"v1.0","tradeid":"{}","src":"{}","des":"{}","tradecode":"{}","opercode":"{}","workdate":"{}","worktime":"{}"}
packet_pager="pager":{"pageNo":{},"pageSize":{}}
packet_params="params":{"entity":{}}#functiontemplate

#业务功能调用模板
F1000={{},"DATA":{"opttype":"{}","pager":{"pageNo":{},"pageSize":{}},"params":{"entity":{"rq":{},"userid":"{}","username":"{}","userip":"{}"}}}}}
F1001={{},"DATA":{"opttype":"{}","pager":{"pageNo":{},"pageSize":{}},"params":{"entity":{"rq":{},"userid":"{}","username":"{}","userip":"{}"}}}}}



```

