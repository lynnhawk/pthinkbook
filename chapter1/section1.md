# 第一节 父工程：Parent

仅定义pom.xml ，里面声明了distributionManagement  和plugins。开发时如果需要变动内容，请记得及时通过mvn deploy，命令发布到服务器。

这个文件中有一个属性值project.executor.runtime.dir，它是为了让大家开发时可以更快速的进行调试而定义，当将相关业务代码编写好需要进行测试时，只要在对应的工程中执行  mvn  package，maven就会自动将最新版本的jar文件自动复制到runtime 的环境中，其中：

1、后台服务bu会直接自动重新加载，无需重启后台服务

2、如果除bu外的其他jar文件有更新，则需要手工重新启动后台服务

xml内容如下：

```xml

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"

xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">

<modelVersion>4.0.0</modelVersion>

<properties>

<jdk.version>1.7</jdk.version>

<encoding.type>UTF-8</encoding.type>

<project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>

<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>

<jquery.version>2.1.1</jquery.version>

<bootstrap.version>3.3.0</bootstrap.version>

<bootstrapvalidator.version>0.5.2</bootstrapvalidator.version>

<bootstrap-datetimepicker.version>2.3.1</bootstrap-datetimepicker.version>

<bootstrap-multiselect.version>0.9.8</bootstrap-multiselect.version>

<font-awesome.version>4.1.0</font-awesome.version>

<requirejs.version>2.1.14-1</requirejs.version>

<require-css.version>0.1.7</require-css.version>

<nprogress.version>0.1.2</nprogress.version>

<servlet.version>3.1.0</servlet.version>

<logback.version>1.1.3</logback.version>

<slf4j.version>1.7.12</slf4j.version>

<ehcache.version>2.10.0</ehcache.version>

<spring.version>3.0.5.RELEASE</spring.version>

<ice.version>3.4.2</ice.version>

<testng.version>6.9.10</testng.version>

<mysql.version>5.1.33</mysql.version>

<mariadb.version>1.2.3</mariadb.version>

<oracle.version>10.2.0.5.0</oracle.version>

<jfinal.version>2.2</jfinal.version>

<jfinal-dreampie.version>1.2</jfinal-dreampie.version>

<jfinal-web.version>0.2.1</jfinal-web.version>

<jfinal-shiro.version>0.2</jfinal-shiro.version>

<jfinal-shiro-freemarker.version>0.2</jfinal-shiro-freemarker.version>

<jfinal-tablebind.version>0.1</jfinal-tablebind.version>

<jfinal-routebind.version>0.1</jfinal-routebind.version>

<jfinal-sqlinxml.version>0.1</jfinal-sqlinxml.version>

<jfinal-quartz.version>0.2</jfinal-quartz.version>

<jfinal-mailer.version>0.2</jfinal-mailer.version>

<jfinal-utils.version>0.1</jfinal-utils.version>

<jfinal-slf4j.version>0.1</jfinal-slf4j.version>

<druid.version>1.0.24</druid.version>

<!-- executor runtime dir-->

 <project.executor.runtime.dir>开发者本机的svn目录/PthinkCloudApp/test/pthink-executor</project.executor.runtime.dir>

 <project.testserver.key>开发者本机的svn/PthinkCloudApp/test/10.10.241.24.ppk</project.testserver.key>

 <project.testserver.remotedir>/home/cloudapp/server</project.testserver.remotedir>

 <project.testserver.ip>222.44.18.147</project.testserver.ip>


</properties>

<groupId>com.pthink.cloudapp</groupId>

<artifactId>pthink-parent</artifactId>

<packaging>pom</packaging>

<version>0.5</version>

<name>pthink-parent</name>

<description>AppProject Parent</description>

<url>http://www.pthink.com.cn</url>

<distributionManagement>

<repository>

<id>nexus-releases</id>

<url>http://www.lynnhawk.com:8081/repository/maven-releases</url>

</repository>

<snapshotRepository>

<id>nexus-snapshots</id>

<url>http://www.lynnhawk.com:8081/repository/maven-snapshots</url>

</snapshotRepository>

</distributionManagement>

<build>

<finalName>${project.name}</finalName>

<pluginManagement>

<plugins>

<plugin>

<groupId>org.apache.maven.plugins</groupId>

<artifactId>maven-compiler-plugin</artifactId>

<configuration>

<encoding>${encoding.type}</encoding>

<source>${jdk.version}</source>

<target>${jdk.version}</target>

<optimize>false</optimize>

<debug>false</debug>

<showDeprecation>false</showDeprecation>

<showWarnings>false</showWarnings>

<compilerArguments>

<verbose/>

</compilerArguments>

</configuration>

</plugin>

<plugin>

<groupId>org.apache.maven.plugins</groupId>

<artifactId>maven-site-plugin</artifactId>

<version>3.5</version>

<configuration>

<generateReports>true</generateReports>

<inputEncoding>${encoding.type}</inputEncoding>

<outputEncoding>${encoding.type}</outputEncoding>

</configuration>

</plugin>

<plugin>

<groupId>org.apache.maven.plugins</groupId>

<artifactId>maven-javadoc-plugin</artifactId>

<version>2.10.1</version>

<configuration>

<aggregate>true</aggregate>

</configuration>

</plugin>

</plugins>

</pluginManagement>

</build>

<dependencies>

<dependency>

<groupId>com.oracle</groupId>

<artifactId>ojdbc14</artifactId>

<version>${oracle.version}</version>

<scope>runtime</scope>

</dependency>

<dependency>

<groupId>mysql</groupId>

<artifactId>mysql-connector-java</artifactId>

<version>${mysql.version}</version>

<scope>runtime</scope>

</dependency>

<dependency>

<groupId>org.mariadb.jdbc</groupId>

<artifactId>mariadb-java-client</artifactId>

<version>${mariadb.version}</version>

<scope>runtime</scope>

</dependency>

<!-- log begin -->

<dependency>

<groupId>ch.qos.logback</groupId>

<artifactId>logback-classic</artifactId>

<version>${logback.version}</version>

</dependency>

<dependency>

<groupId>ch.qos.logback</groupId>

<artifactId>logback-core</artifactId>

<version>${logback.version}</version>

</dependency>

<dependency>

<groupId>org.slf4j</groupId>

<artifactId>slf4j-log4j12</artifactId>

<version>${slf4j.version}</version>

</dependency>

<dependency>

<groupId>org.slf4j</groupId>

<artifactId>jcl-over-slf4j</artifactId>

<version>${slf4j.version}</version>

</dependency>

<dependency>

<groupId>org.slf4j</groupId>

<artifactId>slf4j-api</artifactId>

<version>${slf4j.version}</version>

</dependency>

<!-- log end -->

<dependency>

<groupId>org.testng</groupId>

<artifactId>testng</artifactId>

<version>${testng.version}</version>

<scope>test</scope>

</dependency>

</dependencies>

</project>

```

