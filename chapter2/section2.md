# 第二节 开发新的业务功能

这个部分是后台业务逻辑的核心部分，所有的业务处理均在此处完成提供给第三方使用者，因此需要定义明确的输入与输出，所有的交互均为json格式报文，暂时不接受二进制文件处理。注意：所有的业务功能必须放在pthink-bu这个工程中，否则不会被应用服务器自动管理。

## 1、创建新BU

在pthink-bu的工程中创建一个新的Java Class，新的class必须继承com.pthink.cloudapp.standard.abstracts.Atom

## 2、根据设计要求编写输入与输出的定义注解

注解的内容

```java

tradeCode = 业务交易功能号,必须保证唯一，以6位数字定义，我们把11开头的全部归为质量类系统
status = Component.Status.Run, 是否启用，可用的参数为Run, Stop
internal =    是否内部使用，true  或false，如果是true则不会被外部使用
tradeName =  业务交易功能名称，
author = 开发人员ID
comment = 业务交易功能详细说明
createDate = 创建日期，格式为"2016/08/22"   
```

3、按照父类要求实现atomicTransaction方法

