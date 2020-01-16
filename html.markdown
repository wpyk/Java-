# 1. HTML
超文本标记语言，HyperTextMarkupLanguage,是一种用于创建网页的标准标记语言，目前最新的是HTML5。网页浏览器能够通过读取HTML生成网页。HTML通过多种多样的标签实现结构化信息，比较主要的标签有<html>,<head>,<body>等等，一般都有开始和结束标签，也有可以单独作用的标签，如<br(换行)>标签。
# 2. HTML 实现功能
## 2.1 视频 <video>
HTML5 通过video元素来包含视频，使用<video> 标签，举例如下：  
	    
	
	<video width="320" height="240" controls="controls">
  		<source src="movie.ogg" type="video/ogg">      
  		<source src="movie.mp4" type="video/mp4">    
		Your browser does not support the video tag.  
	</video>


![video.png](https://i.loli.net/2020/01/16/Q9DvGiUWgsb6JdC.png)


## 2.2 音频<audio> 
 
    <audio controls="controls">
  		<source src="song.ogg" type="audio/ogg">
  		<source src="song.mp3" type="audio/mpeg">
		Your browser does not support the audio tag.
	</audio>


![audio.png](https://i.loli.net/2020/01/16/vAiGFgJjyrK2Zow.png)


## 2.3 拖放
拖放是一种常见的特性，即抓取对象以后拖到另一个位置。在 HTML5 中，拖放是标准的一部分，任何元素都能够拖放。

`<img id="drag1" src="/i/eg_dragdrop_w3school.gif" draggable="true" ondragstart="drag(event)" />`

## 2.4 画布 canvas
canvas 元素用于在网页上绘制图形。HTML5 的 canvas 元素使用 JavaScript 在网页上绘制图像。画布是一个矩形区域，您可以控制其每一像素。canvas 拥有多种绘制路径、矩形、圆形、字符以及添加图像的方法。

规定元素的 id、宽度和高度：

    <canvas id="myCanvas" width="200" height="100"></canvas>

canvas 元素本身是没有绘图能力的。所有的绘制工作必须在 JavaScript 内部完成：

    <script type="text/javascript">
	var c=document.getElementById("myCanvas");
	var cxt=c.getContext("2d");
	cxt.fillStyle="#FF0000";
	cxt.fillRect(0,0,150,75);
	</script>

## 2.5 可伸缩矢量图形 SVG 


    <!DOCTYPE html>
	<html>
	<body>
	
	<svg xmlns="http://www.w3.org/2000/svg" version="1.1" height="190">
	  <polygon points="100,10 40,180 190,60 10,60 160,180"
	  style="fill:lime;stroke:purple;stroke-width:5;fill-rule:evenodd;" />
	</svg>
	
	</body>
	</html>


### 与canvas的区别

SVG：SVG 是一种使用 XML 描述 2D 图形的语言。  
SVG 基于 XML，这意味着 SVG DOM 中的每个元素都是可用的。您可以为某个元素附加 JavaScript 事件处理器。  
在 SVG 中，每个被绘制的图形均被视为对象。如果 SVG 对象的属性发生变化，那么浏览器能够自动重现图形。

Canvas：Canvas 通过 JavaScript 来绘制 2D 图形。  
Canvas 是逐像素进行渲染的。  
在 canvas 中，一旦图形被绘制完成，它就不会继续得到浏览器的关注。如果其位置发生变化，那么整个场景也需要重新绘制，包括任何或许已被图形覆盖的对象。

## 2.6 地理位置 Geolocation
HTML5 Geolocation API 用于获得用户的地理位置。鉴于该特性可能侵犯用户的隐私，除非用户同意，否则用户位置信息是不可用的。

## 2.7 WEB 存储

HTML5 提供了两种在客户端存储数据的新方法：

localStorage - 没有时间限制的数据存储。   
sessionStorage - 针对一个 session 的数据存储
之前，这些都是由 cookie 完成的。但是 cookie 不适合大量数据的存储，因为它们由每个对服务器的请求来传递，这使得 cookie 速度很慢而且效率也不高。

在 HTML5 中，数据不是由每个服务器请求传递的，而是只有在请求时使用数据。它使在不影响网站性能的情况下存储大量数据成为可能。

对于不同的网站，数据存储于不同的区域，并且一个网站只能访问其自身的数据。

HTML5 使用 JavaScript 来存储和访问数据。

### 2.7.1 localStorage 

localStorage 方法存储的数据没有时间限制。第二天、第二周或下一年之后，数据依然可用。  

### 2.7.2 sessionStorage 

sessionStorage 方法针对一个 session 进行数据存储。当用户关闭浏览器窗口后，数据会被删除。

## 2.8 应用程序缓存

### 2.8.1 基本内容介绍

HTML5 引入了应用程序缓存，这意味着 web 应用可进行缓存，并可在没有因特网连接时进行访问。通过创建 cache manifest 文件实现缓存。

应用程序缓存为应用带来三个优势：

离线浏览 - 用户可在应用离线时使用它们
速度 - 已缓存资源加载得更快
减少服务器负载 - 浏览器将只从服务器下载更新过或更改过的资源。  
下面的例子中，HTML文件包含了cache manifest。

    <!DOCTYPE HTML>
	<html manifest="demo.appcache">

	<body>
	The content of the document......
	</body>
	
	</html>

每个指定了 manifest 的页面在用户对其访问时都会被缓存。如果未指定 manifest 属性，则页面不会被缓存（除非在 manifest 文件中直接指定了该页面）。

manifest 文件的建议的文件扩展名是：".appcache"。

请注意，manifest 文件需要配置正确的 MIME-type，即 "text/cache-manifest"。必须在 web 服务器上进行配置。

### 2.8.2 Manifest 文件

manifest 文件是简单的文本文件，它告知浏览器被缓存的内容（以及不缓存的内容）。

manifest 文件可分为三个部分：

CACHE MANIFEST - 在此标题下列出的文件将在首次下载后进行缓存  
NETWORK - 在此标题下列出的文件需要与服务器的连接，且不会被缓存  
FALLBACK - 在此标题下列出的文件规定当页面无法访问时的回退页面（比如 404 页面）  

### 2.8.3 更新缓存

更新缓存
一旦应用被缓存，它就会保持缓存直到发生下列情况：

1. 用户清空浏览器缓存  
2. manifest 文件被修改（参阅下面的提示）  
3. 由程序来更新应用缓存  


# 3. HTML 常见标签和用法
## 3.1 
## 3.2 target = blank