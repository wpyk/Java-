# 新建一个eclipse工程
![01.png](https://i.loli.net/2019/12/31/5ewCyYo3WmMXR4F.png)

注意：一定要在自己指定的路径下新建一个文档存放新的代码
“java project”是一个比较简单的project选项，另一个“project”也很常用，如用来建立maven，web项目的时候。

## 新建 package  
eclipse里的package是文件路径，其命名规则：com.公司名.项目名.模块名....，当个人作为开发者的时候，可以命名为：com.wpyk.project1,com.wpyk.project2. 在这里，每一个“.”都代表一个层级，如果去存放代码的文档里看，会发现，一个名为com的文件下面有wpyk文件，wpyk文件下面有名为project1和project2两个文件。
![03.png](https://i.loli.net/2019/12/31/xCOqfw2gVRsABTU.png)
当穿件完com文件时候，右击再建新的package时，在com.后面加新文件的名字，下图中用的是wpyk。  
![04.png](https://i.loli.net/2019/12/31/tWr6mjYiuI9VlRB.png)

## 新建 Class
对于每一个class来说，其内部只能包含两种内容：属性和方法。
每一个.java文件，只能有一个public的class。也就是说，public的class必须存在于同名的java文件中。  
下面代码实现了一个非常简单的类：

```java
package com.sort;
/**
 * 这是一个文档注释
 * @author wangxiaokai
 *
 */
public class Order{
    //以下三者为属性
    private int id;
    
    //针对上面创建的属性，使用getter和setter方法来获取、改变其对应的值

    public int getId() {
        /*对于每一个调用某种方法的对象来说，getter不需要传入参数，直接返回该对象的某个*属性就行了。
        */
        return id;
    }
    
    public void setId(int id) {
        this.id = id;
    }
    
   /*这是一个构造方法，构造方法的特点有（1）方法名和类名一致；（2）没有返回值；构造方法不一定是public的*/
    public Order(int id) {
        this.id = id;
    }
    /*下面这个空的构造器是上面构造器的一个重载，Overload，重载是在同一个类的文件里实现*的。普通的方法也能重载，其名称不变，但是参数不同。
    */
    public Order(){

    }
    //Override,重写是子类对父类方法的重新改造，返回值和形参都不能改变
    @Override
    public String toString() {
        return "id: "+id;
    }
    
    
}

```


## 注释的写法
java文档的注释分三类:单行注释，多行注释及文档注释。
单行注释一般用 “//”表示，多行注释用'/*' 作为开头，'*/'作为结尾，且每一行的开头都是“*”.
文档注释是写在每一个项目开始的那里，用'/**'作为开头，'*/'作为结尾。文档注释有一些标签，用'@'符号标明。

```java
    // 这是一个单行注释
    
    
    /*这是一个多行注释
     * 构造方法的两个特点：（1）方法名和类名一致；（2）没有返回值；
     * 构造方法不一定是public的
     */

    /**
     * 这是一个文档注释
     * @author wangxiaokai
     *
     */
```