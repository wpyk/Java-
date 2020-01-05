# 简单的Q&A合集
## 1.Mybatis 中 sql 语句的占位符 #{} 和 ${}
### 占位符 #{}  
在Mybatis中#{}是一个占位符,可以实现preparedStatement向占位符中设置值，自动进行java类型和jdbc的转换。能够可以接收简单类型的值，或者pojo的属性。在接收简单类型值的时候，#{}中可以填写value或者其它名称，也可以空着不写。这种方法可以有效的防止sql注入。
### 拼接符${}
在Mybatis中${} 表示拼接sql串，通过 ${} 可以将 parameterType 传入的内容拼接在 sql 中且不进行 jdbc 类型转换，不能防止 sql 注入问题， 可以接收简单类型值或pojo属性值，如果parameterType传输单个简单类型值，{} 括号中只能是 value。

## 2.pojo 和 po 的区别？  
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


## j3.ava.lang.Integer 是什么？

首先要明白java.lang.Integer是什么，它是Integer这个class的全地址。
在每一个java class的文件中，最开始的地方需要import package。通过import，在当前的项目中就可以使用被引用的package里的class。举例说明，假如我在com.wpyk 这个package中创建了People类，想要在位于com.wxk这个package中的Teacher类中使用People类，就可以 import com.wpyk.People，然后就能够直接 People p = new People（）。如果在最初没有import，则上述的语句要变为： com.wpyk.People p = new com.wpyk.People()。  
在Mybatis中，官方定义了别名，xml文件中可以不使用权名称，直接使用int也能够识别。
但是要注意，在以下情况时必须使用全地址：   

1. 当某一个类名出现在两个package中。举例说明： import com.wpyk.People， import com.wxk.People，那在新创建People对象的时候，到底用的是import的哪一个类呢？此时需要通过全地址来区分；
2. 如上文分析中提到的，没有import的时候；
3. 在无法import的文件，如xml中。


1.若子类继承父类时没有重写函数并且没有声明这个函数，是否可以调用父类函数？

2. - 子类有参构造方法，如果是继承自父类，则必须使用super先初始化父类
```java
public Student(String name, int age) {
    super(name, age);
}
```
是否需要在Student后面写extends People 呢？


3. 有接口的类是否必须将该接口的所有abstract函数都实体化才能用这个接口？

4. Open implementation 是啥，按住ctrl後将鼠标移到arraylist那里时候

5. Map的键不能是int么？
   在Map增加内容时，键只能是string，那string+int是啥类型，比如“key”+i
   
6.User 的26行为什要先进行super

7. final string是个什么高级类

8. UserDao中38行的stmt本身就有execute方法么
   是的，除了execute方法之外还有executeQuery方法，根据执行的内容进行选取

9.UserDao中127行return回去的是什么？只是个布尔值还是说return回去的是个resultUser

10.如果在用户进行注册时想要控制其用户名：如不能为空，不能和已有的用户名重复，该如何控制？
   是否要再加入一个作为控制的java问价，先进行判断，再选择是否把数据提交给数据库？还是说有servlet的interface？
   
11.复制java文件夹后哪些路径信息需要修改？

12. 如果将变量放在循环外，所有变量都会变？为什么后续的变量冲掉了前面的变量？
