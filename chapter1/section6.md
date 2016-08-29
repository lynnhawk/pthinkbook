# 第六节 执行器：executor

如果需要发布新版本，仅需要执行目录下的deploy.bat即可自动完成。文件为target目录下的pthink-executor-bin.zip

zip文件解压缩后，核心配置文件包括：

app.properties： 应用程序配置文件

applicationContext.xml ：spring配置文件

apprun.bat  ：windows环境下的主执行程序

db.properties ：数据库配置文件

gen.properties：自动生成db类的配置文件，生产环境下请删除。

genmodel.bat：自动生成 db类的执行程序

logback.xml：log配置

apprun.sh ：linux环境下的测试执行程序

start.sh ：linux环境下的 启动程序

stop.sh ：linux环境下的 停止程序



---

## 1、配置文件app.properties的参数说明

`#是否打开调试模式`

`app.debug=true`

`#数据库类型，可用的参数为oracle 、 sqlserver 、 mysql 、mariadb 四种，注意全部为小写`

`dbtype=mariadb`

`#Ice.*为通讯平台的参数，可按实际情况进行调整`

`Ice.MessageSizeMax=10240`

`Ice.ThreadPool.Server.Size=50`

`Ice.ThreadPool.Server.SizeMax=100`

`# CommunicationFile*  文件传输的相关参数`

`CommunicationFilePath=./CommunicationFilePath`

`CommunicationFileLimit=32896`

`#服务器的监听名称，客户端调用时需要此参数`

`app.name=PthinkCloudAppListener`

`#服务器的监听端口`

`app.port=9701`

`#业务bu所在目录，该目录与 文件 【apprun.*】中的目录必须保持一致`

`app.pluginClasspath=file\:./units/`

`# 业务bu 的自动更新间隔，单位是毫秒，默认3秒`

`app.pluginschedulingtime=3000`

`#是否保存key，无需修改`

`app.keystore=1`

`#是否cluster，无需修改`

`app.cluster=0`

`#session超时，单位为秒`

`app.session.timeout=30`

`# 是否启动http server`

`httpserver.start=true`

`#httpserver端口`

`httpserver.port=8801`

`#是否加载ActiveRecord`

`jfinalActiveRecordPlugin.start=true`

