---
layout: post
title: hibernate的检索方式
categories: Blog
description: hibernate的检索方式
keywords: java,hibernate
---



### 导航对象检索方式

>1、根据已经加载的对象导航到其他对象

一个entity实体或者POJO类中包含着对其他类的引用(数据库中一对多或者多对多关系等)
dept对象关联staff集合 hibernate自动检索出staff的数据。  sql语句如下:

```java
     Dept d = (Dept) session.get(Dept.class,2);
     d.getStaffSet().size();
```
    

<img src="/images/blog/javaEE/2018_03_08hibernateQuery.PNG" width="80%" height="40%" border="black" alt="检索sql语句" />

>2、OID的检索方式

按照对象的OID来检索对象  比如: session.get(id值);/session.load(id值);

```java
下面是示例代码:
           Customer c = session.get(Customer.class, 1L);
		    
		    System.out.println("------------------------------------");
		    
		    //查询该客户下的所有联系人
		    
		    System.out.println(c.getLinkmans().size());

```

>3、HQL的检索方式 (createQuery) hibernate框架特有的 使用最广泛的hql 

<b>需要注意的是:</b> hql里面的字段是属性是entity实体的属性字段 不是数据库字段
```java
   1、带别名和链式编程

    session.createQuery("select c from Customer c").list();

   2、排序  order by asc 升序 desc 降序

   session.createQuery("from Linkman l order by l.lkm_id desc").list();

   3、分页

   query.setFirstResult(a);  从哪条记录开始 
   query.setMaxResults(b);  每页显示的记录数

   假设每页展示3条数据:

   //从第一条记录开始
     query.setFirstResult(0);

     //每页展示3条数据
      query.setMaxResults(3);

      //第二页数据
     
        query.setFirstResult(3);

		// 每页的条数是3
		query.setMaxResults(3);

其实和limit是一样的  limit m,n

m相当于上面的 



```


