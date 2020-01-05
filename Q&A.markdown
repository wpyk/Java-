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