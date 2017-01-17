# 产品开发指导书

本文采用GitBook+Markdown进行编写。相关知识请自行查找并学习。

## 介绍

整个产品开发架构采用分布式技术为基础，利用[ICE](https://zeroc.com"ICE framework")（Internet Communication Engine）作为通讯和分布式基础平台，所有的核心业务采用业务交易单元统一管理，实现自动加载、动态更新的功能。每个交易单元均为独立的业务组件，不同交易单元也可以相互调用、自由组合。

整个框架核心部分采用java开发，整个工程采用maven进行管理。主要用到的第三方jar包括：

* ICE

* apache commons系列

* spring

* hiberbate（可选）

* JFinal（可选）

* log4j & logback

* c3p0、dbcp 、druid （数据库连接池，可任选，默认druid）


......

## 系统架构

![](/assets/system.png)

