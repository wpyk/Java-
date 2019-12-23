# 简单的Q&A合集
## Mybatis 中 sql 语句的占位符 #{} 和 ${}
### 占位符 #{}  
在Mybatis中#{}是一个占位符,可以实现preparedStatement向占位符中设置值，自动进行java类型和jdbc的转换。能够可以接收简单类型的值，或者pojo的属性。在接收简单类型值的时候，#{}中可以填写value或者其它名称，也可以空着不写。这种方法可以有效的防止sql注入。
### 拼接符${}
在Mybatis中${} 表示拼接sql串，通过 ${} 可以将 parameterType 传入的内容拼接在 sql 中且不进行 jdbc 类型转换，不能防止 sql 注入问题， 可以接收简单类型值或pojo属性值，如果parameterType传输单个简单类型值，{} 括号中只能是 value。

## pojo 和 po 的区别？  
pojo是简单的java类，全称是plain old java object。 这种类有一些简单的属性, 以及每一个属性的get/set方法。 但是其不拥有复杂的方法。POJO是一个简单的、普通Java对象，它包含业务逻辑处理或持久化逻辑等，但不是JavaBean、EntityBean等，不具有任何特殊角色，不继承或不实现任何其它Java框架的类或接口。例如：  

public class People { //简单的Java类，称之为POJO，不继承，不实现接口
 
   　　private String name;
 
   　　public void setName(String name) {
 
          　　this.name = name;
 
   　　}
      public String getName() {
 
          　　return this.name;
 
   　　}

 
}  
po是pojo持久化之后的对象，在Hibernate或则Mybatis中PO相对于POJO会增加一些用来管理数据库entity状态的属性和方法。可以认为po就是一条数据库查询记录的存储容器。  
JavaBean是特殊化的pojo，当pojo按照一定的约束规则创建时，就成为了JavaBean，这些规则是：  
1、这个类必须具有一个公共的(public)无参构造函数；
2、所有属性私有化（private）；
3、私有化的属性必须通过public类型的方法（getter和setter）暴露给其他程序，并且方法的命名也必须遵循一定的命名规范。 
4、这个类应是可序列化的。（比如可以实现Serializable 接口，用于实现bean的持久性）


## java.lang.Integer 是什么？

首先要明白java.lang.Integer是什么，它是Integer这个class的全地址。
在每一个java class的文件中，最开始的地方需要import package。通过import，在当前的项目中就可以使用被引用的package里的class。举例说明，假如我在com.wpyk 这个package中创建了People类，想要在位于com.wxk这个package中的Teacher类中使用People类，就可以 import com.wpyk.People，然后就能够直接 People p = new People（）。如果在最初没有import，则上述的语句要变为： com.wpyk.People p = new com.wpyk.People()。  
但是要注意，在以下情况时必须使用全地址：   

1. 当某一个类名出现在两个package中。举例说明： import com.wpyk.People， import com.wxk.People，那在新创建People对象的时候，到底用的是import的哪一个类呢？此时需要通过全地址来区分；
2. 如上文分析中提到的，没有import的时候；
3. 在无法import的文件，如xml中。
