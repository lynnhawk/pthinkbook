# 数据字典

数据字典的插件是用来管理所有的系统字典数据的，目前没有实现多语言版本。
它支持的形式为文件或数据库两种类型。

* 文件型：通过定义properties文件来实现。
* 数据库：通过在数据库中增加对应数据表来实现。

系统启动并加载成功后，它能够将所有的数据字典加载到ehcache中，实现字典数据的快速访问，如果系统变动了字典数据，它也可以自动更新cache并写入到数据库或字典文件中。

需要使用的配置文件： {% em type="green" %} config.properties {% endem %}
[include](../assets/config.properties)


如果使用的是文件型字典数据，则还需要 {% em type="green" %} dict.properties {% endem %}

[include](../assets/dict.properties)

