# 本文档主要总结了在创建user之后，如何创建Blog的增删改查。相比于User增加的地方：能够在浏览器网页页面实现增和查，并且通过css和js的渲染使文本更好看。

# 1. DAO层的整合
## 1.1 entity文件夹与Bean
在wpyk.blog下面创建entity文件夹，其本质和bean是一样的，用那种都行。  
**注意1** 一般任何一个entity，都留一个无参的构造器，这样框架想要new一个这样的对象的时候不会抱错。不然容易发生空指针错误。  
**注意2**对于web架构中的对象，在view，controller端有可能不能以不变的形式出现，即从浏览器获取数据的bean和通过controller实现的bean，虽然都是为了传递一定的参数，但是其属性名称可能无法一一对应，并且在实际项目监理过程中也不能一一对应。这时就要简历这些bean之间的构造器，如下面的代码中的注意2，就通过BlogView构建出了blog.  
```java
package wpyk.blog.entity;

import java.util.Date;

import wpyk.blog.entity.vo.BlogView;

public class Blog {
    private int id;

    private String title;
    
    private String summary;
    
    private Date releaseDate;
    
    private int clickHit;
    
    private int replyHit;
    
    private String content;
    
    private String keyword;
    
    // 注意1
    public Blog() {
        
    }
    
    //注意2
    public Blog(BlogView blogView) {
        this.title = blogView.getTitle();
        this.content = blogView.getHtmlMaterial();
    }
    
    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getTitle() {
        return title;
    }

    public void setTitle(String title) {
        this.title = title;
    }

    public String getSummary() {
        return summary;
    }

    public void setSummary(String summary) {
        this.summary = summary;
    }

    public Date getReleaseDate() {
        return releaseDate;
    }

    public void setReleaseDate(Date releaseDate) {
        this.releaseDate = releaseDate;
    }

    public int getClickHit() {
        return clickHit;
    }

    public void setClickHit(int clickHit) {
        this.clickHit = clickHit;
    }

    public int getReplyHit() {
        return replyHit;
    }

    public void setReplyHit(int replyHit) {
        this.replyHit = replyHit;
    }

    public String getContent() {
        return content;
    }

    public void setContent(String content) {
        this.content = content;
    }

    public String getKeyword() {
        return keyword;
    }

    public void setKeyword(String keyword) {
        this.keyword = keyword;
    } 
    
}

```


## 1.2 配置相关的Service，DAO 和 Mapper.xml

*与上文中说到的相同。之前某个类访问数据库的时候我们给文件夹起的名字叫mapper，这里新建一个叫dao的文件夹，用于实现对数据库的访问。*  
与User.markdown文件中说道的业务流程相似，当通过controller访问某个连接的时候，服务器这边能够找打一个Service， Service会new一个同名的Dao对象，然后通过与该Dao对象映射的.xml文件来实现业务逻辑。这个**映射的实现方式是在.xml文件中的namespace**中指定其对应的Dao。下面是Service， Dao和.xml的代码：   
Service:

    package wpyk.blog.service;

	import java.util.List;
	
	import org.springframework.beans.factory.annotation.Autowired;
	import org.springframework.stereotype.Service;
	
	import wpyk.blog.dao.BlogDao;
	import wpyk.blog.entity.Blog;
	import wpyk.blog.entity.vo.BlogView;
	
	@Service
	public class BlogService {
	
	@Autowired
	private BlogDao blogDao;
	
		public List<Blog> queryBlog(){
			List<Blog> list = blogDao.queryBlog();
			return list;
		}
		
		public BlogView queryById(int id) {
			return new BlogView(blogDao.queryById(id));
		}
		
		public void addBlog(Blog blog) {
			blogDao.addBlog(blog);
		}
		
		public void deleteBlog(int id) {
			blogDao.deleteBlog(id);
		}
		
		private void updateBlog(Blog blog) {
			blogDao.updateBlog(blog);
		}
	}

Dao

    package wpyk.blog.dao;

	import java.util.List;
	
	import wpyk.blog.entity.Blog;
	import wpyk.blog.entity.vo.BlogView;
	
	public interface BlogDao {
		
		//增
		public void addBlog(Blog blog);
		//删
		public void deleteBlog(int id);
		//改
		public void updateBlog(Blog blog);
		//查
		public List<Blog> queryBlog();
		//query by id
		public Blog queryById(int id);
	}
.xml

    <?xml version="1.0" encoding="UTF-8" ?>
	<!DOCTYPE mapper
	PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
	"http://mybatis.org/dtd/mybatis-3-mapper.dtd">
	<mapper namespace="wpyk.blog.dao.BlogDao">
		<select id="queryBlog" resultType="Blog">
			SELECT * FROM t_blog 
		</select>
		
		<select id="queryById" resultType="Blog">
			SELECT * FROM t_blog b WHERE b.id = #{id}
		</select>
	
		<insert id="addBlog">
			insert into t_blog(title, summary, releaseDate, clickHit, replyHit,content,keyword)
			values(#{title}, #{summary}, #{releaseDate}, #{clickHit}, #{replyHit},#{content},#{keyword})
		</insert>
		
		<delete id="deleteBlog">
			delete from t_blog b where b.id = #{id}
		</delete>
		
		<update id="updateBlog">
			update t_blog
			<set>
				<if test="title!=null and title!=''">
			 		title=#{title},
			 	</if>
			 	<if test="summary!=null and summary!=''">
			 		summary=#{summary},
			 	</if>
			 	<if test="content!=null and content!=''">
			 		content=#{content},
			 	</if>
				<if test="clickHit!=null">
					clickHit=#{clickHit},
				</if>
				<if test="replyHit!=null">
					replyHit=#{replyHit},
				</if>
				<if test="keyWord!=null and keyWord!=''">
			 		keyword=#{keyword},
			 	</if>
			</set>
			where id=#{id}
		</update>

	</mapper>



# 2. Controller 的编写
Controller的编写是这个Blog项目中最重要的东西，因此单独取出来作为一个部分。注意，下方代码目前和js，css整合了的方法是addBlog和queryById.

    package wpyk.blog.controller;

	import java.util.List;
	
	import org.springframework.beans.factory.annotation.Autowired;
	import org.springframework.stereotype.Controller;
	import org.springframework.web.bind.annotation.PathVariable;
	import org.springframework.web.bind.annotation.RequestBody;
	import org.springframework.web.bind.annotation.RequestMapping;
	import org.springframework.web.bind.annotation.RestController;
	import org.springframework.web.servlet.ModelAndView;
	
	import wpyk.blog.entity.Blog;
	import wpyk.blog.entity.vo.BlogView;
	import wpyk.blog.service.BlogService;
	
	@Controller
	public class BlogController {
	
		@Autowired
		private BlogService blogService;
		
		@RequestMapping("/blogs/all")
		public List<Blog> queryBlog(){
			return blogService.queryBlog();
		}
		
		@RequestMapping("/blog/delete/{id}")
		public void deleteBlog(@PathVariable int id){
			blogService.deleteBlog(id);
		}
		
		@RequestMapping("/blog/{id}")
		public ModelAndView queryById(ModelAndView modelAndView, @PathVariable int id){
			BlogView blogView = blogService.queryById(id);
			modelAndView.addObject("article", blogView);
			modelAndView.setViewName("article");
			return modelAndView;
		}
		
		@RequestMapping("/blog/update")
		public void updateBlog(@RequestBody int id){
			blogService.deleteBlog(id);;
		}
		
		@RequestMapping("/admin/blog/add")
		public String addBlogPage(){
			return "admin/blogadd";
		}
		
		@RequestMapping("/admin/blogadd.f")
		public void addBlog(BlogView blogView){
			blogService.addBlog(new Blog(blogView));
		}
		
	}

## 2.1 addBlog()方法的实现

我们来简单想一下写一个blog的逻辑，当在浏览器中输入../blog/add的时候，应该出来一个能够写东西的框，就像markdown一样。展示在前端的是js文件，因此在下面的代码中，我们要做的是当用户访问../blog/add时，给他返回一个可编辑文本的页面，即项目中的blogadd.ftl

//根据框架的约束，返回是String的时候自动对应到application.properties里配置的ftl文件中。
   		
	//根据框架的约束，返回是String的时候自动对应到application.properties里配置的ftl文件中。
	@RequestMapping("/admin/blog/add")
    public String addBlogPage(){
			return "admin/blogadd";
	}
该ftl文件为：   
    <!DOCTYPE html>
	<html lang="zh">
	<#-- 写博客 -->
	<head>

	    <meta charset="utf-8">
	    <meta http-equiv="X-UA-Compatible" content="IE=edge">
	    <meta name="viewport" content="width=device-width, initial-scale=1">
	    <meta name="description" content="">
	    <meta name="author" content="">
	
	    <title>Full-Stack 系统后台管理</title>
	
	    <!-- Bootstrap Core CSS -->
	    <link href="../../vendor/admin/bootstrap/css/bootstrap.min.css" rel="stylesheet">
	
	    <!-- MetisMenu CSS -->
	    <link href="../../vendor/admin/metisMenu/metisMenu.min.css" rel="stylesheet">
	
	    <!-- Custom CSS -->
	    <link href="../../dist/admin/css/sb-admin-2.css" rel="stylesheet">
	
	    <!-- Morris Charts CSS -->
	    <link href="../../vendor/admin/morrisjs/morris.css" rel="stylesheet">
	
	    <!-- Custom Fonts -->
	    <link href="../../vendor/admin/font-awesome/css/font-awesome.min.css" rel="stylesheet" type="text/css">
	
	    <!-- EditorMD -->
	    <link rel="stylesheet" href="../../vendor/editor/css/editormd.css"/>
	
	    <!-- HTML5 Shim and Respond.js IE8 support of HTML5 elements and media queries -->
	    <!-- WARNING: Respond.js doesn't work if you view the page via file:// -->
	    <!--[if lt IE 9]>
	    <script src="https://oss.maxcdn.com/libs/html5shiv/3.7.0/html5shiv.js"></script>
	    <script src="https://oss.maxcdn.com/libs/respond.js/1.4.2/respond.min.js"></script>
	    <![endif]-->
	
	    <!-- 自定义样式 -->
	    <link rel="stylesheet" href="/css/public.css">
		</head>
	
	<body>
	
	<div id="wrapper">
	<#-- s 导航 -->
	<#include "public/nav.ftl">
	<#-- e 导航 -->
	
	<#-- s 页面内容 -->
	    <div id="page-wrapper">
	    <#-- s 页面内容 -->
	        <form>
	        <#-- s 隐藏字段 -->
	            <input name="mdMaterial" id="id_input_md" type="hidden">
	            <input name="htmlMaterial" id="id_input_html" type="hidden">
	            <input name="description" id="id_input_article_description" type="hidden">
	            <input name="rawTags" id="id_input_article_tags" type="hidden">
	        <#-- e 隐藏字段 -->
	        <#-- s 标题、标签等 -->
	            <div class="row">
	                <div class="col-sm-12">
	                    <div class="input-group">
	                        <div class="row">
	                            <div class="col-md-12"></div>
	                        </div>
	                    <#-- 文章标题 -->
	                        <input name="title" type="text" class="form-control" placeholder="标题">
	                        <div class="row">
	                            <div class="col-md-12"></div>
	                        </div>
	                        <span class="input-group-btn">
	                        <button id="id_btn_blog_submit" class="btn btn-primary" type="button">提交</button>
	                    </span>
	                    </div>
	                </div>
	            </div>
	        <#-- e 标题 -->
	        </form>
	        <div class="row">
	            <div class="col-sm-12">
	                <div id="test-editormd">
	                <#-- 文章内容 -->
	                    <textarea style="display:none;"></textarea>
	                </div>
	            </div>
	        </div>
	    <#-- e 页面内容 -->
	    </div>
	<#-- e 页面内容 -->
	
	</div>
	
	<#-- s 文章描述内容填写模态框 -->
	<div class="modal fade" tabindex="-1" role="dialog" id="id_modal_article_detail">
    <div class="modal-dialog" role="document">
        <div class="modal-content">
            <div class="modal-header">
                <button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</span>
                </button>
                <h4 class="modal-title">文章详情</h4>
            </div>
            <div class="modal-body">
            <#-- s 模态内容 -->
                <div class="form-group">
                    <label for="id_input_article_description_in_modal">对文章内容的描述</label>
                    <textarea type="text" class="form-control" id="id_input_article_description_in_modal" placeholder="Description"></textarea>
                </div>
                <div class="form-group">
                    <label for="id_input_article_tags_in_modal">为文章添加标签（以逗号分隔）</label>
                    <input type="text" class="form-control" id="id_input_article_tags_in_modal" placeholder="Tags">
                </div>
            <#-- e 模态内容 -->
            </div>
            <div class="modal-footer">
                <button type="button" class="btn btn-default" data-dismiss="modal">取消</button>
                <button type="button" class="btn btn-primary" id="id_btn_release_in_modal">确认发布</button>
            </div>
        </div><!-- /.modal-content -->
    </div><!-- /.modal-dialog -->
	</div><!-- /.modal -->
	<#-- e 文章描述内容填写模态框 -->
	
	<!-- jQuery -->
	<script src="../../vendor/admin/jquery/jquery.min.js"></script>
	
	<!-- Bootstrap Core JavaScript -->
	<script src="../../vendor/admin/bootstrap/js/bootstrap.min.js"></script>
	
	<!-- Metis Menu Plugin JavaScript -->
	<script src="../../vendor/admin/metisMenu/metisMenu.min.js"></script>
	
	<!-- Morris Charts JavaScript -->
	<script src="../../vendor/admin/raphael/raphael.min.js"></script>
	<script src="../../vendor/admin/morrisjs/morris.min.js"></script>
	<script src="../../data/morris-data.js"></script>
	
	<!-- Custom Theme JavaScript -->
	<script src="../../dist/admin/js/sb-admin-2.js"></script>
	<script src="../../vendor/editor/editormd.min.js"></script>
	
	<#-- 自定义 js -->
	<script src="../../js/b_blogadd.js"></script>
	<script src="../../js/public.js"></script>
	</body>
	
	</html>

此时页面显示为：
![](https://i.loli.net/2020/01/14/P3Epz9KqZBsRbMc.png)
当我们完成编辑后，按下提交按钮的一瞬间，我们在View端输入的内容，会被赋值给vo中的类，即BlogView。
		
		  

		@RequestMapping("/admin/blogadd.f")    
		public void addBlog(BlogView blogView){    
			blogService.addBlog(new Blog(blogView));  
		}  
为什么提交后会到上面那个链接呢，这里需要仔细看一下js文件里面的内容： 
![](https://i.loli.net/2020/01/15/LS2jhw3aJUsPD9M.png)  
文本框中圈中的js文件是实现blog提交页面活起来，并且点击提交按钮后弹出模态框的功能。接下来我们解释一下html和js文件是如何联动，实现blog的添加功能的。

首先我们来看一下js文件，最开头加载的是页面显示类似markdown输入框的脚本，是edit md开源项目提供的。  
![3.png](https://i.loli.net/2020/01/15/OuYn1oUqVhjQ4vp.png)  

写完博客，点击提交之后出现了模态框。以模态框中出现的“确认提交”按钮为例，说一下html和js是如何协作将输入的内容传递回controller。
![4.png](https://i.loli.net/2020/01/15/naADJU2dmKeI6tW.png)  


模态框中有“对内容的描述” 和 “为文章添加标签”两个小的文本框，即有两个文本框的内容。当我们点击确认发表的时候，“确认发表”这个按钮的id："id_btn_release_in_modal",在js里，其同id的代码，如下图中红色框圈起来的，这个XXX.bind('click'，function（){method1，method2}，代表绑定一个click事件，当**点击**的时候，对这个绑定的id，执行后面的function


![5.png](https://i.loli.net/2020/01/15/QNicO9ur3Jxkmp8.png)  


接下来我们看一下这两个方法做了什么，在js里搜索saveDetailText方法，和 submitBlogAddForm方法，如下图：  

![6.png](https://i.loli.net/2020/01/15/5mKF86SpPENOjXC.png)  

标出的1和2就是两个被执行的方法。其中1是通过'val'方法将后面的内容赋值给"id_input_article_description"，而这个参数是存在于html文件的form表单中的input参数。
 

# 3.queryById
## 3.1 我们在创建Service的时候，queryById的返回值是个Blog，但是js
    @RequestMapping("/blog/{id}")
	//modelAndView 是框架自动注入的，后面的@PathVariable是去url里的参数的
	public ModelAndView queryById(ModelAndView modelAndView, @PathVariable int id){
		BlogView blogView = blogService.queryById(id);
		modelAndView.addObject("article", blogView);
		modelAndView.setViewName("article");
		return modelAndView;
	}