# 第三章 创建一个新的用户展示层

在此架构下，所有业务处理均全部集中于后台服务层，在用户使用层，用户可以利用多种技术手段通过调用后台服务层提供的访问接口来获得信息服务。目前已经开发的展示层范例包括：GUI（Java开发）、Web（Java开发）、Mobile（基于IonicFramework实现），后面的章节将逐一描述。

准备相关开发环境：

1、安装maven，并设置好settings.xml，配置库中已经提供3.x版本，可直接使用。

2、安装NodeJS环境

3、安装android模拟器

4、如果需要编写文档，需要安装gitbook edit（本文档就是采用gitbook结合Markdown编写）

5、安装svn客户端

6、如果要加入gitbook的在线书写团队，请安装git客户端，并注册github和gitbook的账号，然后在本地环境下安装gitbook工具。如果要发布书请在书籍的工程目录下，先安装发布工具，执行的命令如下

```bash
npm install  gitbook  gulp gulp-gh-pages




```

然后再执行下列命令

```bash
gitbook build
gulp publish



```

执行完毕后，就可以在github网站上看到最新编写的文档了。网址是：[https:\/\/lynnhawk.github.io\/pthinkbook\/index.html](https://lynnhawk.github.io/pthinkbook/index.html)

