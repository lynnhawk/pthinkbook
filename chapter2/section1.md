# 第一节 创建新的数据库映射


这部分的业务逻辑全部转移到对应的组件层，DB层不再管理业务相关数据库处理代码，只接受与db相关的工具类代码。

注意事项：

* 数据库表中，真实表中的列 名 不允许使用的名字包括：RN、tempcolumn、temprownumber，这些名字已经被系统内部使用，否则会系统自动过滤这些列信息，不会输出给客户端。



## 使用JFinal控件：定义或生成数据库表的映射

如果是JFinal的ActiveRecord，则配置好db.properties和gen.properties文件（配置说明请参看[第一章 第六节](/chapter1/section6.md)）后，直接调用genmodal.bat，然后将生成的文件复制到db的工程里面就可以进行编译打包了。

## 使用ActiveRecord时 需要追加的工作

修改

```java

public class MappingKit {

    public static void mapping(ActiveRecordPlugin arp) {
        arp.addMapping("CUSTOMERS", "CUSTOMERNUMBER", CUSTOMERS.class);
        arp.addMapping("EMPLOYEES", "EMPLOYEENUMBER", EMPLOYEES.class);
        arp.addMapping("OFFICES", "OFFICECODE", OFFICES.class);
        // Composite Primary Key order: ORDERNUMBER,PRODUCTCODE
        arp.addMapping("ORDERDETAILS", "ORDERNUMBER,PRODUCTCODE", ORDERDETAILS.class);
        arp.addMapping("ORDERFACT", ORDERFACT.class);
        arp.addMapping("ORDERS", "ORDERNUMBER", ORDERS.class);
        // Composite Primary Key order: CHECKNUMBER,CUSTOMERNUMBER
        arp.addMapping("PAYMENTS", "CHECKNUMBER,CUSTOMERNUMBER", PAYMENTS.class);
        arp.addMapping("PRODUCTS", "PRODUCTCODE", PRODUCTS.class);
        arp.addMapping("QUADRANT_ACTUALS", QuadrantActuals.class);
        arp.addMapping("TRIAL_BALANCE", TrialBalance.class);
        arp.addMapping("T_DEPARTMENT", TDepartment.class);
    }
}

```

将不需要的文件或者没有主键的表内容剔除。默认生成的代码，如果表中无主键，则会生成arp.addMapping\("TRIAL\_BALANCE", "",TrialBalance.class\);  我们需要手工修改该内容变更为： arp.addMapping\("TRIAL\_BALANCE", TrialBalance.class\);

## 复制代码到工程

将所有映射类的代码加入到 pthink-db的工程中，代码放入pthink-db\src\main\java目录下面即可。

## 为自动生成的部分数据库类开发相应的DAO操作（可选）

可根据业务需要为相应的类开发一系列业务要求的dao操作类。

## 编译发布

在IDE环境下执行调用maven的compile、jar、delpoy等命令均可完成；或在命令行环境下执行mvn deploy也可以。然后将生成的jar文件（在target目录中）复制到运行环境下替换原来的pthink-db\*.jar的文件即可。

