# 第一节 创建新的Web客户端

## 1、范例程序说明

范例代码下载地址：[http:\/\/222.44.18.140\/svn\/pthink\/product\/PthinkCloudApp\/02.example\/02.client\/ExampleWeb](http://222.44.18.140/svn/pthink/product/PthinkCloudApp/02.example/02.client/ExampleWeb)

从配置取得后直接通过maven进行构建即可，可以直接在jetty中测试或发布到tomcat等类似的web Application中测试均可。

发布后可以访问http:\/\/ip:端口号\/虚拟目录\/f1000来访问测试页面。截图如下：

![](/assets/01.png)

页面使用了Jquery 的DataTables控件，列信息与数据信息均来自于返回报文。

该页面调用的功能号为1000，请求报文范例如下：

```java


 {

 "CMD": {

 "appver": "v1.0",

 "tradeid": "b0e5265ffbe94e62903207fe29f0baa5",

 "src": "cardclient",

 "des": "cardserver",

 "tradecode": "1000",

 "opercode": "pthink",

 "workdate": "20160812",

 "worktime": "165232"

 },

 "DATA": {

 "params": {

 "entity": {

 "rq": 4,

 "userid": "phy",

 "username": "penghaiyu",

 "userip": "192.168.0.14"

 }

 }

 }

 }

}


```

返回报文范例如下：

```java


{

 "HEAD": {

 "traderef": "f13e2fca50b943a59ba6091e04783c34",

 "workdate": "20160830"

 },

 "BODY": {

 "r02": "hello",

 "pager": {

 "position": 0,

 "pageNo": 1,

 "totalPage": 1,

 "firstPage": true,

 "lastPage": true,

 "nextPage": 1,

 "prePage": 1,

 "totalItems": 2,

 "pageSize": 3

 },

 "columns": [

 {

 "title": "OFFICECODE",

 "cn": "OFFICECODE",

 "data": "OFFICECODE",

 "name": "OFFICECODE",

 "id": "OFFICECODE"

 },

 {

 "title": "城市",

 "cn": "城市",

 "data": "CITY",

 "name": "CITY",

 "id": "CITY"

 },

 {

 "title": "电话",

 "cn": "电话",

 "data": "PHONE",

 "name": "PHONE",

 "id": "PHONE"

 },

 {

 "title": "地址1",

 "cn": "地址1",

 "data": "ADDRESSLINE1",

 "name": "ADDRESSLINE1",

 "id": "ADDRESSLINE1"

 },

 {

 "title": "地址2",

 "cn": "地址2",

 "data": "ADDRESSLINE2",

 "name": "ADDRESSLINE2",

 "id": "ADDRESSLINE2"

 },

 {

 "title": "省",

 "cn": "省",

 "data": "STATE",

 "name": "STATE",

 "id": "STATE"

 },

 {

 "title": "国家",

 "cn": "国家",

 "data": "COUNTRY",

 "name": "COUNTRY",

 "id": "COUNTRY"

 },

 {

 "title": "邮编",

 "cn": "邮编",

 "data": "POSTALCODE",

 "name": "POSTALCODE",

 "id": "POSTALCODE"

 },

 {

 "title": "TERRITORY",

 "cn": "TERRITORY",

 "data": "TERRITORY",

 "name": "TERRITORY",

 "id": "TERRITORY"

 }

 ],

 "result": [

 {

 "OFFICECODE": "1",

 "CITY": "San Francisco",

 "PHONE": "+1 650 219 4782",

 "ADDRESSLINE1": "100 Market Street",

 "ADDRESSLINE2": "Suite 300",

 "STATE": "CA",

 "COUNTRY": "USA",

 "POSTALCODE": "94080",

 "TERRITORY": "NA"

 },

 {

 "OFFICECODE": "4",

 "CITY": "Paris",

 "PHONE": "+33 14 723 4404",

 "ADDRESSLINE1": "43 Rue Jouffroy D'abbans",

 "ADDRESSLINE2": null,

 "STATE": "",

 "COUNTRY": "France",

 "POSTALCODE": "75017",

 "TERRITORY": "EMEA"

 }

 ],

 "c": "00000",

 "m": "调用成功"

 }

}

```

## 2、完整的系统开发步骤

### A）利用IDE或maven等类似工具新建一个web应用

项目中引用了一个ClientAPI，可以直接通过maven 引入即可。

```xml
<dependency> 
<groupId>penghaiyu.cloudapp.client</groupId> 
<artifactId>clientapi</artifactId> 
<version>1.0-SNAPSHOT</version>
</dependency>

```

B）编写调用功能

代码范例如下：

```java
String F1000 = ConfigUtil.getInstance(ConfigUtil.ConfigName).getValueFromPropFile("F1000").toString();
String s1000 = PacketUtil.format(
 F1000, PacketUtil.getHeader("1000", "pthink"), "Q", 0, 3, 4, "phy", "penghaiyu", "hello");
String result = IceTradeUtil.makeTrade(AppConst.ICE_Connection, "1000", s1000);

```

result就是后台返回的json数据，详细内容可看开头部分说明。

类ConfigUtil是用来读取配置文件中的报文模板。
类PacketUtil是用来处理报文模板与参数，最终构建请求报文。
类IceTradeUtil是向后台发送请求报文的工具类。
AppConst.ICE_Connection是一个ICE连接，一个应用只需要创建一个连接实例，如果断开则会自动重连。



C）编写展示页面功能

bbbb

```java



```

bbbb

D）配置server.properties

cccc
\`\`\`java

\`\`\`
ccccc

E）编译发布

