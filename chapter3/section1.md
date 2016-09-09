# 第一节 创建新的Web客户端



程序开发注意点：

* 范例程序中表格显示采用的是jQuery 的DataTable控件，它在进行翻页时默认限制了服务端返回的json数据格式内容，因此我们在使用该控件时，需要在最后返回数据时调用clientapi中的DataTableUtil.getRetData进行二次加工后再输出即可正常工作。





## 1、范例程序说明

程序是基于jfinal的框架开发的，下载地址：[http:\/\/222.44.18.140\/svn\/pthink\/product\/PthinkCloudApp\/02.example\/02.client\/ExampleWeb](http://222.44.18.140/svn/pthink/product/PthinkCloudApp/02.example/02.client/ExampleWeb)

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

### B）编写调用功能

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
AppConst.ICE\_Connection是一个ICE连接，一个应用只需要创建一个连接实例，如果断开则会自动重连。

### C）编写展示页面功能

范例代码如下

```javascript
<#include "/common/head_manage.html" />
<body class="hold-transition skin-blue sidebar-mini"><div class="wrapper">
<#include "/common/manage_top_left.html" /> 
<!-- Content Wrapper. Contains page content --> 
<div class="content-wrapper"> 
 <!-- Content Header (Page header) --> 
<section class="content-header">
 <h1> 交易管理 <small>交易明细</small> </h1> <ol class="breadcrumb"> <li><i class="icon-dashboard"></i> 商户管理平台</li> <li>交易管理</li> <li>交易明细</li> </ol> </section>  <!-- Main content --> <section class="content">  <!-- Info boxes --> <div class="row">  <div class="col-md-3 col-sm-6 col-xs-12"> <div class="info-box"> <span class="info-box-icon bg-aqua"><i class="ion glyphicon glyphicon-hdd"></i></span> <div class="info-box-content svr"> <div class="info-box-text"><i class="glyphicon glyphicon-hdd"></i> ${(d.gamename)!''} (ID:${(d.id)!'0'})</div> <div class="info-box-text"><i class="glyphicon glyphicon-map-marker"></i> ${(d.serverip)!'0.0.0.0'}:${(d.serverport)!'0'}</div> <div class="info-box-text"><i class="glyphicon glyphicon-yen"></i> 当日 <span>${(d.amount/100)!'0'}</span> 元</div> </div> </div> </div>  </div>  <!-- /.row --> <!-- Main row --> <div class="row">  <!-- Left col --> <div class="col-md-12"> <div class="box box-primary "> <div class="box-header with-border"> <h3 class="box-title"><i class="icon-list-alt"></i> 交易明细列表</h3> <div class="box-title-right"> <div class="input-group"> <button type="button" class="btn btn-default pull-right" id="daterange-btn"> <span> <i class="icon-calendar"></i> 时间区间选择 </span> <i class="icon-caret-down"></i> </button> </div></div> </div> <!-- /.box-header --> <div class="box-body"> <div class="table-responsive"> <table id="datalist" class="display" cellspacing="0" width="100%"> <thead><tr></tr></thead> </table>  </div> <!-- /.table-responsive -->  </div> <!-- /.box-body 翻页--> <div class="box-footer clearfix">   </div> <!-- /.box-footer -->  </div> <!-- /.box -->  </div> </div> <!-- /.row -->  </section> <!-- /.content -->  </div> <!-- /.content-wrapper --> <#include "/common/foot.html" /> </div><!-- ./wrapper --><script>$(document).ready(function() { var data, tableName= '#datalist', columns, str, jqxhr = $.ajax('${base.getContextPath()}/f1000j') .done(function () { data = JSON.parse(jqxhr.responseText); $.each(data.BODY.columns, function (k, colObj) { str = '<th>' + colObj.title + '</th>'; $(str).appendTo(tableName+'>thead>tr'); }); $(tableName).dataTable({ language: { url: '${base.getContextPath()}/plugins/datatables/chinese.json' }, "data": data.BODY.result, "columns": data.BODY.columns, "fnInitComplete": function () { // Event handler to be fired when rendering is complete (Turn off Loading gif for example) console.log('Datatable rendering complete'); } }); }) .fail(function (jqXHR, exception) { var msg = ''; if (jqXHR.status === 0) { msg = 'Not connect. Verify Network please!'; } else if (jqXHR.status == 404) { msg = 'Requested page not found. [404]'; } else if (jqXHR.status == 500) { msg = 'Internal Server Error [500].'; } else if (exception === 'parsererror') { msg = 'Requested JSON parse failed.'; } else if (exception === 'timeout') { msg = 'Time out error.'; } else if (exception === 'abort') { msg = 'Ajax request aborted.'; } else { msg = 'Uncaught Error.\n' + jqXHR.responseText; } //console.log(msg); });} );</script></body></html>


```

其中由于使用Jquery的 DataTable的原因，数据获取利用ajax方式进行提取。列表头也利用datatable的属性直接自动构建了，另外还翻译了DataTable的相关资源内容，直接展示为中文。

### D）配置server.properties

配置文件如下

```java
AppName=应用系统名称
AppDebug=是否处于调试模式
AppVersion=系统版本
AppDeveloper=开发者信息
#应用服务器配置
serverId=应用服务器监听名称
#设置服务器地址格式是IP:端口:超时（毫秒），如果有多台用“,”分隔
servers=127.0.0.2:9701:0,115.159.64.16:9701:0
#common 
packetpacket_default={{},"DATA":{"opttype":"{}","pager":{"pageNo":{},"pageSize":{}},"params":{"entity":{}}}}
packet_header="CMD":{"appver":"v1.0","tradeid":"{}","src":"{}","des":"{}","tradecode":"{}","opercode":"{}","workdate":"{}","worktime":"{}"}
packet_pager="pager":{"pageNo":{},"pageSize":{}}
packet_params="params":{"entity":{}}
# Function List
F1000={{},"DATA":{"opttype":"{}","pager":{"pageNo":{},"pageSize":{}},"params":{"entity":{"rq":{},"userid":"{}","username":"{}","userip":"{}"}}}}}
F1001={{},"DATA":{"opttype":"{}","pager":{"pageNo":{},"pageSize":{}},"params":{"entity":{"rq":{},"userid":"{}","username":"{}","userip":"{}"}}}}}


```

packetpacket\_default是完整报文模板
packet\_header是报文头部分模板
packet\_pager是分页区模板
packet\_params是参数区模板
F\*\*\*（\*\*\*为后台已经开发好的功能号数字）是对应功能号的报文模板

### E）编译发布

利用maven或ide工具打包发布后部署到server中即可测试

