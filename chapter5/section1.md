# Jfinal DAO 

## 1、数据库查询使用like查询

我们如果要使用like来进行数据库查询时，如果采用预编译方式来编写代码，sql语句中不可以直接使用%，而需要将%放入参数中，这样才可以得到正确的结果。代码范例如下：

```java


private static void getData() {
    Object[] o = new Object[]{"%1%"}; 
    List<TDepartment> customers = TDepartment.dao.find("select * from T_DEPARTMENT where 1=1 " + " and OFFICECODE like ? ", o); 

    for (TDepartment d : customers) { 
        Set<Map.Entry<String, Object>> set = d._getAttrsEntrySet();
        Iterator<Map.Entry<String, Object>> it = set.iterator(); 
        System.out.println("================="); 
        while (it.hasNext()) { 
            Map.Entry<String, Object> next = it.next(); 
            System.out.println(next.getKey() + ":" + next.getValue()); 
        } 
        System.out.println("================="); 
    }
}


```
