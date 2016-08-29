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





