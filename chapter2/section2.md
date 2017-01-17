# 第二节 开发新的业务功能

这个部分是后台业务逻辑的核心部分，所有的业务处理均在此处完成提供给第三方使用者，因此需要定义明确的输入与输出，所有的交互均为json格式报文，暂时不接受二进制文件处理。注意：所有的业务功能必须放在pthink-bu这个工程中，否则不会被应用服务器自动管理。

## 创建新BU

在pthink-bu的工程中创建一个新的Java Class，新的class必须继承com.pthink.cloudapp.standard.abstracts.Atom

## 根据设计要求编写输入与输出的定义注解

注解的内容

```java
@Component(        
tradeCode = 业务交易功能号,必须保证唯一，以6位数字定义，我们把11开头的全部归为质量类系统
status = Component.Status.Run, 是否启用，可用的参数为Run, Stop
internal = 是否内部使用，true 或false，如果是true则不会被外部使用
tradeName = 业务交易功能名称，
author = 开发人员ID
comment = 业务交易功能详细说明
createDate = 创建日期，格式为"2016/08/22"
params = { 
@Parameter(classify = "查询", demo = "1001", 
inputs = { 
@Item(nullable = Item.Nullable.NO, id = "rq", name = "请求类型", type = Item.Type.INT, explain = "用户请求类型，默认1表示机器时间、2表示数据库时间、3表示查询一个结果集"), 
@Item(nullable = Item.Nullable.NO, id = "userid", name = "用户ID", type = Item.Type.STRING, explain = "用户ID"), 
@Item(nullable = Item.Nullable.YES, id = "username", name = "用户名称", type = Item.Type.STRING, explain = "用户名称"), 
@Item(nullable = Item.Nullable.YES, id = "userip", name = "用户IP", type = Item.Type.STRING, explain = "用户IP") }, 

outputs = { 
@Item(nullable = Item.Nullable.YES, id = "r01", name = "服务器时间", type = Item.Type.STRING, explain = "服务器时间"), 
@Item(nullable = Item.Nullable.YES, id = "r02", name = "用户IP", type = Item.Type.STRING, explain = "用户IP"), 
@Item(nullable = Item.Nullable.NO, id = "c", name = "返回码", type = Item.Type.STRING, explain = "返回码"), 
@Item(nullable = Item.Nullable.NO, id = "m", name = "说明", type = Item.Type.STRING, explain = "返回码说明") } 
), 
@Parameter(classify = "设置时间", demo = "1001", 
inputs = { 
@Item(nullable = Item.Nullable.YES, id = "usertime", name = "用户请求时间", type = Item.Type.STRING, explain = "用户请求时间"), 
@Item(nullable = Item.Nullable.YES, id = "userip", name = "用户IP", type = Item.Type.STRING, explain = "用户IP") }, 
outputs = { 
@Item(nullable = Item.Nullable.NO, id = "c", name = "返回码", type = Item.Type.STRING, explain = "返回码"), 
@Item(nullable = Item.Nullable.NO, id = "m", name = "说明", type = Item.Type.STRING, explain = "返回码说明") } )},
modified = {@Modified})

```

## 根据业务要求实现业务方法

方法名为atomicTransaction

```
boolean result = false;
String tradeCode = tradeInfo.tradeCode();
Logs.log().debug("Begin request, TradeCode[{}], clientIp=[{}]", tradeCode, tradeInfo.getConninfo().getRemoteIp());
try {    

tradeInfo.wrap2First(RFrame.entity);    //提取报文中entity部分的内容到顶层
int reqType = tradeInfo.getInt("rq");   //获取输入中rq的内容 
String userid = tradeInfo.getString("userid");    //获取输入中rq的内容
 String userName = tradeInfo.getString("username");    
String userIP = tradeInfo.getString("userip");    
if (Utility.isEmpty(userid)) {        //对输入字段进行数据校验，有错误则直接调用异常抛出
throw new RWarn(RWarn.MSG_99997, "userid不能为空");    
}    
if (Utility.isEmpty(reqType)) {        
throw new RWarn(RWarn.MSG_99997, "reqType不能为空");    
}    
//<outputs name=defaultout>    
tradeInfo.put("r02", userIP);    //构造输出字段
if (getResult(reqType, tradeInfo)) {        
tradeInfo.putReason(RWarn.MSG_00000, "调用成功");   //返回成功标志 
}    
//</outputs>    
result = true;
} catch (RWarn e) {   //异常处理 
throw e;
} catch (Exception e) {    
e.printStackTrace();    
//记录日志
Logs.log().error("Failure request, TradeCode[{}] , TradeName [{}], err=[{}]", tradeCode, tradeInfo.getAtomInfo().getTradeName(), e.getCause().getMessage());    
throw new RWarn(RWarn.MSG_90010, tradeCode, tradeInfo.getAtomInfo().getTradeName());
}
Logs.log().debug("Success TradeCode[{}]", tradeCode);
return result;
```

## 编译发布

操作步骤与数据库映射的编译发布雷同。区别只是工程名称和所在目录不同而已。

 请注意 ：

a ） 生成的pthink-bu.jar放入运行环境下覆盖同名文件，下次重启服务后就可以自动加载新的业务模块。

b ） 如果需要立刻生效并进行测试，可以直接将编译好的class放入unit目录下就可以实现热部署，不需要重启服务就能进行测试了。

c）如果只更新了class而没有更新jar，则下次应用服务器重启时会自动恢复jar文件内部的class。

## 编写测试报文范例

每一个业务功能开发完成后，需要把自己测试的接收报文与返回范例提取出来，放入resources\/docs目录中，文件名必须是对应的"tradecode".txt，比如注解中声明的tradeCode =1000，则报文范例也必须是1000.txt

