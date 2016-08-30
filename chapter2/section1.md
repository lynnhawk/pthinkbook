# 第一节 创建新的数据库映射

## 1、定义或生成数据库表的映射

如果是Hibernate，则直接采用注解声明方式即可。

如果是JFinal的ActiveRecord，则配置好db.properties和gen.properties文件（配置说明请参看[第一章 第六节](/chapter1/section6.md)）后，直接调用genmodal.bat，然后将生成的文件复制到db的工程里面就可以进行编译打包了。

## 2、 使用ActiveRecord时 需要追加的工作

修改

```java

public class _MappingKit {

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

将不需要的文件或者没有主键的表内容剔除。默认生成的代码，如果表中无主键，则会生成arp.addMapping\("TRIAL\_BALANCE", “”,TrialBalance.class\);  我们需要手工修改该内容变更为： arp.addMapping\("TRIAL\_BALANCE", TrialBalance.class\);

## 3、为自动生成的部分数据库类开发相应的DAO操作（可选）

可根据业务需要为相应的类开发一系列业务要求的dao操作类。

