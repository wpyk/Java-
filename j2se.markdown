# 1.package  包

## 1.1 import 

跨包，在别的类使用该类时，需要用import导入

## 1.2 与文件夹的关系
eg:package com.wpyk
则向程序所在文件夹寻找src文件下的com的wpyk


## 1.3 package com.wpyk

包的声明，会出现在java文件的顶部，声明该类所在的package，如果该声明与实际所处位置不匹配，则会报错

提示The declared package "com" does not match the expected package "com.wpyk"

# 2.main函数

```java
public static void main(String [] args) {
    System.out.println("ok");
}
```

public 

private 

protected


static
静态方法，不需要new出对象就可以直接调用

eg: People 这个类有个eating()这个方法，在入口函数处可以直接调用：
```java
People.eating();
```

main约定，固定的方法名称

# 3.类的继承

 - extends
 - 可以访问父类public和protected的属性和方法，但是不能访问父类private的方法和属性
 - @Override
```java
@Override
public void talk() {
    System.out.println("I'm student,my name is " + getName());
}

```


# 4.类的属性和方法

 - 都可以直接定义在类里面  
 - 都可以控制其访问权限public private protected

可以结合get set方法对属性进行封装

# 5.多态

 - 将一个子类对象赋值给了一个父类变量
 - 这时，调用该变量的方法时，会实际调用到子类override过了的那个方法。

# 6.overloade
 - 方法名 完全相同
 - 形参不同
 - 返回值不影响

# 7.构造器 构造方法
 - 所有类都有一个默认无参的构造方法
 - 构造器的目的是初始化对象的属性（包括自有的和父类的）
 - 如果你重写一个构造器（不管是有参还是无参的），默认的构造器就没了
 - 父类没有的构造方法，子类也不能有
 - 子类有参构造方法，如果是继承自父类，则必须使用super先初始化父类
```java
public Student(String name, int age) {
    super(name, age);
}
```

# 8.abstract

 - 方法体不要（{}不要了），用；结束语句

```java
public abstract void eat() ;
```

 - 方法要使用abstract修饰符
 - abstract方法只能存在于abstract类(类要用abstract修饰符)里面
 - abstract类可以没有abstract方法
 - abstract类不能初始化（不能new），报错Cannot instantiate the type People
 - abstract类的子类要么也abstract，要么帮他实现abstract的方法

![abstract](https://i.loli.net/2018/10/07/5bb9cca006989.png)


# 9. 接口
 
 - java是单继承，多实现（extends後面只能有一個類，但是implemnets後面可以有多個接口）
 - 接口中的方法默认并且只能是public abstract
 - 接口的声明 interface

```java
public interface Teacher{
    public abstract void  teach();
}
```

 - 接口的实现 implements

```java
public class Professor extends People implements Teacher{

    @Override
    public void eat() {
        System.out.println("I'm Professor,I'm eating");
    }

    @Override
    public void teach() {
        System.out.println("I'm Professor,I'm teaching");
        
    }

}
```


# 10 List


 - List是abstract類，不能直接new，那麽需要new它的子類，最常用的子類是ArrayList
 - 一個List只能存一種類，用<>來指定這個list存儲的對象的類別(可以存儲其子類，這是一種多態)
 - List與數組的區別在於List初始化時不需要指定長度

### 初始化

```java
List<People> list = new ArrayList<People>();
```
### add for enhanceFor

# 11 Map

 - Map是abstract類，不能直接new，那麽需要new它的子類，如:HashMap
 - 一个Map包含许多键值对，new的时候需要指定key和value的数据类型
 
 ```java
 Map<String, People> map = new HashMap<String, People>();
 ```

 - 一個Map只能存一種類(可以存儲其子類，這是一種多態)




# 11 时间戳
 - [概念](https://en.wikipedia.org/wiki/Timestamp)
 - [与时间的转换工具](https://tool.lu/timestamp/)
 - java代码中时间戳格式化(linux是秒差，java是毫秒差，所以要*1000转换)
 
```java
long dateLong = blog.getDate();
Date date = new Date(dateLong*1000);
SimpleDateFormat sdf = new SimpleDateFormat("yyyy/MM/dd/HH/mm/ss");
String dateStr = sdf.format(date);
```

# 12 Junit 单元测试

### mavaen追加
```xml
<!-- https://mvnrepository.com/artifact/junit/junit -->
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.12</version>
    <scope>test</scope>
</dependency>

```

### 新建测试样例

eclipse操作流程

 - 选中要被测试的类 
 - new Junit Test Case
 - 选择正确的包位置（测试代码专用）
 - 选择被测试的方法
 - 完成新建
 - 写测试代码


### 断言
 - [断言基础](http://wiki.jikexueyuan.com/project/junit/using-assertion.html)
 - 断言的作用：确保被测代码符合预期

# 13 String转int
Integer.valueOf(id);

# 14 servlet 乱码
https://blog.csdn.net/xiazdong/article/details/7217022

# 15 查漏補缺
 - 包裝類和基礎類，以及相互轉換
 - switch
 - final
 - hashset
 - StringBuilder
 - io.thread.exception

