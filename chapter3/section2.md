# 第二节 创建新的移动客户端

## 1、范例程序说明

程序采用ionic框架开发，可直接发布到iOS和android平台使用，开发过程中也可以通过浏览器直接进行测试。

界面截图如下：

![](/assets/02.png)

![](/assets/03.png)

![](/assets/04.png)

## 2、 完整的系统开发步骤

### A、 准备开发环境

安装NodeJS （4.x版本即可）

利用npm安装cordova 和 ionic
```bash

npm install -g cordova ionic


```

### B、 创建初始工程

ionic start appname  tabs

### C、 修改相关js

app.js 、controllers.js 、/ service.js..

### D、 编译发布

本地浏览器测试：ionic  serve

android 和iOS均要有相应的模拟器

