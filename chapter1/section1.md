# 第一节 父工程：Parent

仅定义pom.xml ，里面声明了distributionManagement  和plugins。开发时如果需要变动内容，请记得及时通过mvn deploy，命令发布到服务器。

这个文件中有几个属性值需要注意：

project.executor.runtime.dir，执行器的本地目录

project.testserver.ip， 测试服务器的 IP地址

project.testserver.key，测试服务器的私钥，主要用来发布最新版本

project.testserver.remotedir， 测试服务器的执行器所在目录

上述几个参数是为了让大家开发时可以更快速的进行调试而定义，当将相关业务代码编写好需要进行测试时，只要在对应的工程中执行  mvn  package，maven就会自动将最新版本的jar文件自动复制到runtime 的环境中.其中：

1、后台服务bu会直接自动重新加载，无需重启后台服务

2、如果除bu外的其他jar文件有更新，则需要手工重新启动后台服务

xml内容如下：

[include](/asset/pom.xml)
