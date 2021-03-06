# 第三节 为后台返回列信息加入多语言翻译

如果需要使用让返回信息的字段说明能支持多语言，可以利用后台的多语言服务，将自动把返回报文中字段部分的中文信息自动输出到报文中。当没有找到中文资源时，会直接返回原始英文字段内容，如果匹配到了多个字段翻译，则只会返回第一个匹配的内容。多语言的资源文件在工程目录下的resources中，中文资源文件使用的编码格式为UTF-8，无需转换。

如果资源文件名已修改（比如名称变更为pthink.properties），请记得修改执行器中app.prpoperties中的参数“**app.fieldFilename**”属性值，将默认值“fields”变更为“pthink”，然后重新发布pthink-db.jar和app.properties到生成环境中即可。如需要更多语言支持，请自行直接添加对应的语言资源文件即可。

多语言范例文件如下：

## fields.properties  -- 默认

```java
T_DEPARTMENT.OFFICECODE=OFFICECODE
T_DEPARTMENT.CITY=CITY
T_DEPARTMENT.PHONE=PHONE
T_DEPARTMENT.ADDRESSLINE1=ADDRESSLINE1
T_DEPARTMENT.ADDRESSLINE2=ADDRESSLINE2
T_DEPARTMENT.STATE=STATE
T_DEPARTMENT.COUNTRY=COUNTRY
T_DEPARTMENT.POSTALCODE=POSTALCODE
T_DEPARTMENT.TERRITORY=TERRITORY
T_DEPARTMENT.BMDM=BMDM

```

## fields\_en.properties -- 英文

```java
T_DEPARTMENT.OFFICECODE=OFFICECODE
T_DEPARTMENT.CITY=CITY
T_DEPARTMENT.PHONE=PHONE
T_DEPARTMENT.ADDRESSLINE1=ADDRESSLINE1
T_DEPARTMENT.ADDRESSLINE2=ADDRESSLINE2
T_DEPARTMENT.STATE=STATE
T_DEPARTMENT.COUNTRY=COUNTRY
T_DEPARTMENT.POSTALCODE=POSTALCODE
T_DEPARTMENT.TERRITORY=TERRITORY
T_DEPARTMENT.BMDM=BMDM

```

## fields\_zh.properties -- 中文

```java
T_DEPARTMENT.OFFICECODE=部门
T_DEPARTMENT.CITY=城市
T_DEPARTMENT.PHONE=电话
T_DEPARTMENT.ADDRESSLINE1=地址1
T_DEPARTMENT.ADDRESSLINE2=地址2
T_DEPARTMENT.STATE=省
T_DEPARTMENT.COUNTRY=国家
T_DEPARTMENT.POSTALCODE=邮编
T_DEPARTMENT.BMDM=部门代码

```

{% em type="red" %}

开发注意：
文件中的所有KEY部分的英文字母内容必须是大写，否则会导致无法正常显示对应的语言资源。如果使用NotePad++  ，选中所有文本后输入Ctrl+Shift+u即可；如果是Idea，输入Ctrl+u


{% endem %}



