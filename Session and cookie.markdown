1. 取出的属性类型未知，使用（String）使其强行转换成string类型；

2. Cookie[] cookies 指的是将取得的cookie各个位存在一个list里么？
   那这个类型的list应该允许数字和字母同时存在吧，但是我记得你之前说
   java和python不一样，不能存不同类型的元素在一个list里；
   Cookie又是一个什么样的类呢
  
3. 为什么会出现，存在某个list但是该list为空的情况？

4. req.getContextPath()是什么

5. cookie.getName().equals("username")
   cookie和cookies什么关系？如果cookies是网上开发者页面中的那一串字符串，那cookie
   遍历字符串时得到的应该只是字母或者数字啊，怎么能等于用户名呢？
   
6. 为什么cookies和username要分别判断是否为空

7. Login 项目里的 method 是 "get", 这个“get” 是什么意思？



throws ServletException, IOException是什么？
 //username==""和username.length()==0有什么区别
如果在login里没设置cookie，是不是就不能进行cookie的验证了？（web1 和我的程序中login部分的内容差很多）
输入home2 的url後跳转至登录页面，登陆后再次打开home2的url无显示，白屏。
登陆成功后，再次打开一个窗口时候，是先匹配session还是先匹配cookies？
当一个程序中既有session部分又有cookie部分，哪部分放在前面，哪部分放在后面？如何实现最佳使用效果？

为什么string类型的长度是string.length(),但是list就是list.length

