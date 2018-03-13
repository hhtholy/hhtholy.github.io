---
layout: post
title: hibernate的检索方式
categories: Blog
description: hibernate面试
keywords: hibernate,java
---

### 导航对象检索方式11111

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



1. 以人为主体没错，但是要有远有近，拍出来全是脸和上半身也不好。
2. 偶尔兼顾景色，不是所有情况下虚化背景都是加分。
3. 一般情况下色彩鲜艳的衣服拍出来会更好看。
4. 人像镜头不是万能的，大光圈容易虚焦，取景范围影响构图，这些都需要更好地考虑。

### 2014 年 6 月 武汉

1. 照顾好拍摄对象的心情，她开心和配合了，才容易出好片。
2. 如果她真的不愿意拍，就不拍了吧，否则出来基本也是废的。
3. 蓝天白云绿水真的很容易出好片，但是阴天加浑浊的长江边还是不要轻易挑战了。

### 2014 年 3 月 武汉

1. 气氛要活泼一点，不然模特摆拍容易表情僵硬。
2. 光圈优先在室外光线好的情况下容易过曝。
3. 只挑拍得最好的片发给模特看，如果没有出好片，宁愿不发。
