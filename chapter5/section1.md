# 数据库开发

## 数据库查询使用like查询

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

### SQL  Server 查询树状菜单语句



```
with CTE as    
(     
-->Begin 一个定位点成员     
 select ID, Name,Parent,cast(Name as nvarchar(100)) as TE,  
        ROW_NUMBER()over(order by getdate()) as OrderID  
        --最关键是上面这个字段，要获取排序字段，按字符串来排序。  
        --其中窗口函数必须要使用order by，但是不能用整型，那就用时间吧  
        from sys_resource where Parent='0' 
-->End      
union all     
-->Begin一个递归成员     
 select sys_resource.ID, sys_resource.Name,sys_resource.Parent,cast(replicate(' ',len(CTE.TE))+'|_'+sys_resource.name as nvarchar(100)) as TE,  
        CTE.OrderID*100+ROW_NUMBER()over(Order by GETDATE()) as OrderID  
        from sys_resource inner join CTE     
        on sys_resource.Parent=CTE.id     
-->End     
)     
select * from CTE  
order by LTRIM(OrderID)
```





