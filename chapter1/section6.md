# 第六节 执行器：executor


如果需要发布新版本，仅需要执行目录下的deploy.bat即可自动完成。文件为target目录下的pthink-executor-bin.zip

zip文件解压缩后，核心配置文件包括：

app.properties： 应用程序配置文件

applicationContext.xml ：spring配置文件

apprun.bat ：windows环境下的主执行程序

db.properties ：数据库配置文件

mail.properties ： 邮件发送控件的配置文件

gen.properties：自动生成db类的配置文件，生产环境下请删除。

genmodel.bat：自动生成 db类的执行程序

logback.xml：log配置

apprun.sh ：linux环境下的测试执行程序

start.sh ：linux环境下的 启动程序

stop.sh ：linux环境下的 停止程序



## 1、配置文件app.properties的参数说明

```java

#是否打开调试模式

app.debug=true

#数据库类型，可用的参数为oracle 、 sqlserver 、 mysql 、mariadb 四种，注意全部为小写

dbtype=mariadb

# CommunicationFile* 文件传输的相关参数

CommunicationFilePath=.\/CommunicationFilePath

CommunicationFileLimit=32896

#服务器的监听名称，客户端调用时需要此参数

app.name=PthinkCloudAppListener

#服务器的监听端口

app.port=9701

#业务bu所在目录，该目录与 文件 【apprun.*】中的目录必须保持一致

app.pluginClasspath=file:./units/

# 业务bu 的自动更新间隔，单位是毫秒，默认3秒

app.pluginschedulingtime=3000

#多语言资源文件名
app.fieldFilename=fields

#默认语言环境，在输出报文时会根据此处内容自动调整columns部分titile和cn的值
app.defaultLocale=zh

#为通讯平台的参数，可按实际情况进行调整 

app.MessageSizeMax=10240 

app.ThreadPool.Server.Size=50 

app.ThreadPool.Server.SizeMax=100

#是否保存key，无需修改

app.keystore=1

#是否cluster，无需修改

app.cluster=0

#session超时，单位为秒

app.session.timeout=30

# 是否启动http server

httpserver.start=true

#httpserver端口

httpserver.port=8801

#是否加载ActiveRecord

jfinalActiveRecordPlugin.start=true

#系统需要启用的插件列表，目前包括encache/mailer/shiro

app.plugins=ehcache,mailer


```

## 2、  配置文件 applicationContext .xml说明

该文件为spring配置文件，无需修改。

## 3、配置文件db.properties说明

数据库配置文件

```java

jdbc.initialSize=1

jdbc.maxActive=50

jdbc.maxIdle=10

jdbc.minIdle=1

jdbc.maxWait=5000

jdbc.removeAbandoned=true

jdbc.removeAbandonedTimeout=300000

jdbc.logAbandoned=true

jdbc.testOnBorrow=true

#数据库JDBC驱动

jdbc.driverClassName=org.mariadb.jdbc.Driver

#JDBC连接串

jdbc.url=jdbc:mariadb://IP:Port/databaseName?characterEncoding=utf8&autoReconnect=true

#数据库用户名

jdbc.username=username

#数据库密码

jdbc.password=password

jdbc.validationQuery=select 1

hibernate.dialect=org.hibernate.dialect.MySQLDialect

```

上述参数一般只需要修改粗体部分的内容即可。

## 4、配置文件gen.properties

该文件为自动生成ActiveRecord对象的配置文件，配置内容如下：

```java

# base model 所使用的包名

baseModelPackageName=com.pthink.cloudapp.model.base

#base model 文件保存路径

baseModelOutputDir=./src/com/pthink/cloudapp/model/base

#model 所使用的包名 (MappingKit 默认使用的包名)

modelPackageName= com.pthink.cloudapp.model

#model 文件保存路径 (MappingKit 与 DataDictionary 文件默认保存路径)

modelOutputDir=./

#不需要生成的表名，多个表则用,分隔，比如a,b,c

excludedTable=adv

#是否在 Model 中生成 dao 对象

generateDaoInModel=true

#是否生成字典文件

generateDataDictionary=false

#需要被移除的表名前缀用于生成modelName。例如表名 "osc_user"，移除前缀 "osc_"后生成的model名为 "User"而非 OscUser，如果有多个表则用,分隔，比如a_,b_,c_

tableNamePrefixes=t_

```

## 5、配置文件logback.xml

该文件为logback的配置文件，配置内容如下：

```xml

<?xml version="1.0" encoding="UTF-8"?>
<configuration debug="false">
    <property name="LOG_HOME" value="./log"/>
    <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
        <encoder class="ch.qos.logback.classic.encoder.PatternLayoutEncoder">
            <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %-5level %logger{50} - %msg%n</pattern>
        </encoder>
    </appender>
    <appender name="FILE" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
            <FileNamePattern>${LOG_HOME}/pthinkserver.%d{yyyy-MM-dd}.log</FileNamePattern>
            <MaxHistory>30</MaxHistory>
        </rollingPolicy>
        <encoder class="ch.qos.logback.classic.encoder.PatternLayoutEncoder">
            <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %-5level %logger{50} - %msg%n</pattern>
            <charset>UTF-8</charset>
        </encoder>
        <triggeringPolicy class="ch.qos.logback.core.rolling.SizeBasedTriggeringPolicy">
            <MaxFileSize>1MB</MaxFileSize>
        </triggeringPolicy>
    </appender>
    <logger name="org.hibernate" level="ERROR"/>
    <logger name="java.sql.Connection" level="DEBUG"/>
    <logger name="java.sql.Statement" level="DEBUG"/>
    <logger name="java.sql.PreparedStatement" level="DEBUG"/>

    <logger name="com.pthink" level="DEBUG"/>

    <root level="DEBUG">
        <appender-ref ref="STDOUT"/>
        <appender-ref ref="FILE"/>
    </root>
</configuration>



```

大部分内容基本不用修改，可以调节的参数为<root level="DEBUG"> ，生产环境下建议将DEBUG修改为ERROR



## 6、邮件配置文件mail.properties

邮件发送服务器的配置文件


```java

#smtp服务器地址

smtp.host=smtp.pthink.com.cn

#端口号

smtp.port=25


#超时时间，单位ms

smtp.timeout=900000

#ssl port

smtp.sslport=587

#是否需要ssl

smtp.ssl=false

#是否需要tls

smtp.tls=false

#是否打印debug信息

smtp.debug=true

#发件人账户

smtp.user=cpb-noreply@pthink.com.cn

#发件人邮箱密码，正式环境下需要加密

smtp.password=a123456

#发件人称呼

smtp.name=[pthink]

#发件人来源显示信息

smtp.from=cpb-noreply@pthink.com.cn



```



