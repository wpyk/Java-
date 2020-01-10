# 1. 什么是FreeMarker

FreeMarker 是一款 模板引擎： 即一种基于模板和要改变的数据， 并用来生成输出文本(HTML网页，电子邮件，配置文件，源代码等)的通用工具。 它不是面向最终用户的，而是一个Java类库，是一款程序员可以嵌入他们所开发产品的组件。


	//template
    <html>
		<head>
		  <title>Welcome!</title>
		</head>
		<body>
		  <h1>Welcome ${user}!</h1>
		  <p>Our latest product:
		  <a href="${latestProduct.url}">${latestProduct.name}</a>!
		</body>
	</html>
当开发者编写一个上面的FreeMarker代码，其中用${}标识出的部分是动态的，数据应来自于数据库，因此不能用静态的HTML代码。上面的模板就实现了在静态模板中包含动态信息。模板文件存放在Web服务器上，就像通常存放静态HTML页面那样。当有人来访问这个页面， FreeMarker将会介入执行，然后动态转换模板，用最新的数据内容替换模板中 ${...} 的部分， 之后将结果发送到访问者的Web浏览器中。访问者的Web浏览器就会接收到例如第下面output所描写的HTML示例那样的内容 (也就是没有FreeMarker指令的HTML代码)，访问者也不会察觉到服务器端使用的FreeMarker。

	//output
	<html>
		<head>
		  <title>Welcome!</title>
		</head>
		<body>
		  <h1>Welcome John Doe!</h1>
		  <p>Our latest product:
		  <a href="products/greenmouse.html">green mouse</a>!
		</body>
	</html>

请注意，模板并没有包含程序逻辑来查找当前的访问者是谁，或者去查询数据库获取最新的产品。 显示的数据是在 FreeMarker 之外准备的，通常是一些 "真正的" 编程语言(比如Java) 所编写的代码。模板作者无需知道这些值是如何计算出的。事实上，这些值的计算方式可以完全被修改， 而模板可以保持不变，而且页面的样式也可以完全被修改而无需改动模板。 当模板作者(设计师)和程序员不是同一人时，显示逻辑和业务逻辑相分离的做法是非常有用的， 即便模板作者和程序员是一个人，这么来做也会帮助管理应用程序的复杂性。 保证模板专注于显示问题(视觉设计，布局和格式化)是高效使用模板引擎的关键。