# 第一节 父工程：Parent
仅定义pom.xml

里面声明了distributionManagement  和plugins。

内容如下：

&lt;project xmlns="http:\/\/maven.apache.org\/POM\/4.0.0" xmlns:xsi="http:\/\/www.w3.org\/2001\/XMLSchema-instance"

 xsi:schemaLocation="http:\/\/maven.apache.org\/POM\/4.0.0 http:\/\/maven.apache.org\/maven-v4\_0\_0.xsd"&gt;

 &lt;modelVersion&gt;4.0.0&lt;\/modelVersion&gt;

 &lt;properties&gt;

 &lt;jdk.version&gt;1.7&lt;\/jdk.version&gt;

 &lt;encoding.type&gt;UTF-8&lt;\/encoding.type&gt;

 &lt;project.reporting.outputEncoding&gt;UTF-8&lt;\/project.reporting.outputEncoding&gt;

 &lt;project.build.sourceEncoding&gt;UTF-8&lt;\/project.build.sourceEncoding&gt;

 &lt;jquery.version&gt;2.1.1&lt;\/jquery.version&gt;

 &lt;bootstrap.version&gt;3.3.0&lt;\/bootstrap.version&gt;

 &lt;bootstrapvalidator.version&gt;0.5.2&lt;\/bootstrapvalidator.version&gt;

 &lt;bootstrap-datetimepicker.version&gt;2.3.1&lt;\/bootstrap-datetimepicker.version&gt;

 &lt;bootstrap-multiselect.version&gt;0.9.8&lt;\/bootstrap-multiselect.version&gt;

 &lt;font-awesome.version&gt;4.1.0&lt;\/font-awesome.version&gt;

 &lt;requirejs.version&gt;2.1.14-1&lt;\/requirejs.version&gt;

 &lt;require-css.version&gt;0.1.7&lt;\/require-css.version&gt;

 &lt;nprogress.version&gt;0.1.2&lt;\/nprogress.version&gt;

 &lt;servlet.version&gt;3.1.0&lt;\/servlet.version&gt;

 &lt;logback.version&gt;1.1.3&lt;\/logback.version&gt;

 &lt;slf4j.version&gt;1.7.12&lt;\/slf4j.version&gt;

 &lt;ehcache.version&gt;2.10.0&lt;\/ehcache.version&gt;

 &lt;spring.version&gt;3.0.5.RELEASE&lt;\/spring.version&gt;

 &lt;ice.version&gt;3.4.2&lt;\/ice.version&gt;

 &lt;testng.version&gt;6.9.10&lt;\/testng.version&gt;

 &lt;mysql.version&gt;5.1.33&lt;\/mysql.version&gt;

 &lt;mariadb.version&gt;1.2.3&lt;\/mariadb.version&gt;

 &lt;oracle.version&gt;10.2.0.5.0&lt;\/oracle.version&gt;

 &lt;jfinal.version&gt;2.2&lt;\/jfinal.version&gt;

 &lt;jfinal-dreampie.version&gt;1.2&lt;\/jfinal-dreampie.version&gt;

 &lt;jfinal-web.version&gt;0.2.1&lt;\/jfinal-web.version&gt;

 &lt;jfinal-shiro.version&gt;0.2&lt;\/jfinal-shiro.version&gt;

 &lt;jfinal-shiro-freemarker.version&gt;0.2&lt;\/jfinal-shiro-freemarker.version&gt;

 &lt;jfinal-tablebind.version&gt;0.1&lt;\/jfinal-tablebind.version&gt;

 &lt;jfinal-routebind.version&gt;0.1&lt;\/jfinal-routebind.version&gt;

 &lt;jfinal-sqlinxml.version&gt;0.1&lt;\/jfinal-sqlinxml.version&gt;

 &lt;jfinal-quartz.version&gt;0.2&lt;\/jfinal-quartz.version&gt;

 &lt;jfinal-mailer.version&gt;0.2&lt;\/jfinal-mailer.version&gt;

 &lt;jfinal-utils.version&gt;0.1&lt;\/jfinal-utils.version&gt;

 &lt;jfinal-slf4j.version&gt;0.1&lt;\/jfinal-slf4j.version&gt;

 &lt;druid.version&gt;1.0.24&lt;\/druid.version&gt;

 &lt;\/properties&gt;

 &lt;groupId&gt;com.pthink.cloudapp&lt;\/groupId&gt;

 &lt;artifactId&gt;pthink-parent&lt;\/artifactId&gt;

 &lt;packaging&gt;pom&lt;\/packaging&gt;

 &lt;version&gt;0.5&lt;\/version&gt;

 &lt;name&gt;pthink-parent&lt;\/name&gt;

 &lt;description&gt;AppProject Parent&lt;\/description&gt;

 &lt;url&gt;http:\/\/www.pthink.com.cn&lt;\/url&gt;

 &lt;distributionManagement&gt;

 &lt;repository&gt;

 &lt;id&gt;nexus-releases&lt;\/id&gt;

 &lt;url&gt;http:\/\/www.lynnhawk.com:8081\/repository\/maven-releases&lt;\/url&gt;

 &lt;\/repository&gt;

 &lt;snapshotRepository&gt;

 &lt;id&gt;nexus-snapshots&lt;\/id&gt;

 &lt;url&gt;http:\/\/www.lynnhawk.com:8081\/repository\/maven-snapshots&lt;\/url&gt;

 &lt;\/snapshotRepository&gt;

 &lt;\/distributionManagement&gt;

 &lt;build&gt;

 &lt;finalName&gt;${project.name}&lt;\/finalName&gt;

 &lt;pluginManagement&gt;

 &lt;plugins&gt;

 &lt;plugin&gt;

 &lt;groupId&gt;org.apache.maven.plugins&lt;\/groupId&gt;

 &lt;artifactId&gt;maven-compiler-plugin&lt;\/artifactId&gt;

 &lt;configuration&gt;

 &lt;encoding&gt;${encoding.type}&lt;\/encoding&gt;

 &lt;source&gt;${jdk.version}&lt;\/source&gt;

 &lt;target&gt;${jdk.version}&lt;\/target&gt;

 &lt;optimize&gt;false&lt;\/optimize&gt;

 &lt;debug&gt;false&lt;\/debug&gt;

 &lt;showDeprecation&gt;false&lt;\/showDeprecation&gt;

 &lt;showWarnings&gt;false&lt;\/showWarnings&gt;

 &lt;compilerArguments&gt;

 &lt;verbose\/&gt;

 &lt;\/compilerArguments&gt;

 &lt;\/configuration&gt;

 &lt;\/plugin&gt;

 &lt;plugin&gt;

 &lt;groupId&gt;org.apache.maven.plugins&lt;\/groupId&gt;

 &lt;artifactId&gt;maven-site-plugin&lt;\/artifactId&gt;

 &lt;version&gt;3.5&lt;\/version&gt;

 &lt;configuration&gt;

 &lt;generateReports&gt;true&lt;\/generateReports&gt;

 &lt;inputEncoding&gt;${encoding.type}&lt;\/inputEncoding&gt;

 &lt;outputEncoding&gt;${encoding.type}&lt;\/outputEncoding&gt;

 &lt;\/configuration&gt;

 &lt;\/plugin&gt;

 &lt;plugin&gt;

 &lt;groupId&gt;org.apache.maven.plugins&lt;\/groupId&gt;

 &lt;artifactId&gt;maven-javadoc-plugin&lt;\/artifactId&gt;

 &lt;version&gt;2.10.1&lt;\/version&gt;

 &lt;configuration&gt;

 &lt;aggregate&gt;true&lt;\/aggregate&gt;

 &lt;\/configuration&gt;

 &lt;\/plugin&gt;

 &lt;\/plugins&gt;

 &lt;\/pluginManagement&gt;

 &lt;\/build&gt;

 &lt;dependencies&gt;

 &lt;dependency&gt;

 &lt;groupId&gt;com.oracle&lt;\/groupId&gt;

 &lt;artifactId&gt;ojdbc14&lt;\/artifactId&gt;

 &lt;version&gt;${oracle.version}&lt;\/version&gt;

 &lt;scope&gt;runtime&lt;\/scope&gt;

 &lt;\/dependency&gt;

 &lt;dependency&gt;

 &lt;groupId&gt;mysql&lt;\/groupId&gt;

 &lt;artifactId&gt;mysql-connector-java&lt;\/artifactId&gt;

 &lt;version&gt;${mysql.version}&lt;\/version&gt;

 &lt;scope&gt;runtime&lt;\/scope&gt;

 &lt;\/dependency&gt;

 &lt;dependency&gt;

 &lt;groupId&gt;org.mariadb.jdbc&lt;\/groupId&gt;

 &lt;artifactId&gt;mariadb-java-client&lt;\/artifactId&gt;

 &lt;version&gt;${mariadb.version}&lt;\/version&gt;

 &lt;scope&gt;runtime&lt;\/scope&gt;

 &lt;\/dependency&gt;

 &lt;!-- log begin --&gt;

 &lt;dependency&gt;

 &lt;groupId&gt;ch.qos.logback&lt;\/groupId&gt;

 &lt;artifactId&gt;logback-classic&lt;\/artifactId&gt;

 &lt;version&gt;${logback.version}&lt;\/version&gt;

 &lt;\/dependency&gt;

 &lt;dependency&gt;

 &lt;groupId&gt;ch.qos.logback&lt;\/groupId&gt;

 &lt;artifactId&gt;logback-core&lt;\/artifactId&gt;

 &lt;version&gt;${logback.version}&lt;\/version&gt;

 &lt;\/dependency&gt;

 &lt;dependency&gt;

 &lt;groupId&gt;org.slf4j&lt;\/groupId&gt;

 &lt;artifactId&gt;slf4j-log4j12&lt;\/artifactId&gt;

 &lt;version&gt;${slf4j.version}&lt;\/version&gt;

 &lt;\/dependency&gt;

 &lt;dependency&gt;

 &lt;groupId&gt;org.slf4j&lt;\/groupId&gt;

 &lt;artifactId&gt;jcl-over-slf4j&lt;\/artifactId&gt;

 &lt;version&gt;${slf4j.version}&lt;\/version&gt;

 &lt;\/dependency&gt;

 &lt;dependency&gt;

 &lt;groupId&gt;org.slf4j&lt;\/groupId&gt;

 &lt;artifactId&gt;slf4j-api&lt;\/artifactId&gt;

 &lt;version&gt;${slf4j.version}&lt;\/version&gt;

 &lt;\/dependency&gt;

 &lt;!-- log end --&gt;

 &lt;dependency&gt;

 &lt;groupId&gt;org.testng&lt;\/groupId&gt;

 &lt;artifactId&gt;testng&lt;\/artifactId&gt;

 &lt;version&gt;${testng.version}&lt;\/version&gt;

 &lt;scope&gt;test&lt;\/scope&gt;

 &lt;\/dependency&gt;

 &lt;\/dependencies&gt;

&lt;\/project&gt;









