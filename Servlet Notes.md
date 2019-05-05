# Servlet Notes

标签（空格分隔）： jsp&servlet

---
<h1>一.servlet请求处理代码流程</h1>
<h2>1.设置响应编码格式</h2>
```
resp.setContextType("text/html;charset=utf-8");
```
<h2>2.获取请求数据:request对象</h2>
* **获取请求头**
```
req.getMethod();//获取请求方式
		req.getRequestURL();//获取URL
		req.getRequestURI();//获取URI
		req.getScheme();//获取协议
```
* **获取请求行**
```
req.getHeader("键名");//返回指定请求头信息
		req.getHeaderNames();//返回指定请求头集合
		
```
```
Enumeration e=req.getHeaderNames();
		while(e.hasMoreElements()){
			String name=(String) e.nextElement();//获取每个键名
			String value=req.getHeader(name);//获取每个键名对应的值
			System.out.println("value:"+value);
		}
```
* **获取用户数据**
```

		req.getParameter("键名");//返回指定的用户数据
		req.getParameterValues("键名");//返回同键不同值的请求数据，数组
		req.getParameterNames();//返回所有用户数据请求的枚举集合，即键名
		//若请求数据不存在，不会报错，返回null;
```
* **request作用域**
```
req.setAttribute(Object name,Object value);
req.getAttribute(Object name);
```
> ####解决一次请求不同Servlet数据共享问题

<h2>3.处理请求数据</h2>
<h2>4.响应处理结果:response对象</h2>
* <h3>设置响应头</h3>
```
setHeader(String name,String value);//在响应头中添加响应信息，同键覆盖
addHeader(String name,String value);//在响应头中添加响应信息，不覆盖
```
* <h3>设置响应状态</h3>
```
resp.sendError(int num,String msg);//自定义响应状态码
```
* <h3>设置响应实体</h3>
```
resp.getWrite().write(String str);//响应具体数据给浏览器
```
<h1>二.生命周期</h1>
> * 从第一次调用到服务器关闭
> * 若配置了load-on-startup,则从服务器启动到服务器关闭

<h1>三.servlet常见错误总结</h1>
> * 404:资源未找到
  * servlet别名拼写错误
  * 虚拟项目名拼写错误
> * 500:内部服务器错误
 * web.xml路径拼写错误
 * servlet方法体代码错误
> * 405:请求方式不支持
  * 请求方式和servlet方法不匹配

<h1>四.请求中文乱码解决</h1>
<h2>1.使用String进行数据重新编码</h2>
```
uname=new String(uname.getBytes("iso8859-1"),"utf-8");
```

<h2>2.使用公共配置</h2>
> *get方式
```
req.setCharacterEncoding("utf-8");
在tomcat中修改server.xml文件，在Connector标签中添加属性useBodyEncodingForURI("utf-8");
```
> *post方式
```
req.setCharacterEncoding("utf-8");
```

<h1>五.客户端与服务端跳转</h1>
* 客户端

```
response.sendRedirect("url");客户端跳转，重定向
```

```
  req.setAttribute("requestkey", "request值");
		  HttpSession session=req.getSession();//获取session
		  session.setAttribute("sessionkey","session值");
		  ServletContext application=this.getServletContext();
		  application.setAttribute("applicationkey","application值");//获取application值

```
* 服务器端
> ####转发特点： 一次请求，浏览器地址不改变；请求转发后直接return即可
```
RequestDispatcher rs=req.getRequestDispatcher("url");
		  rs.forward(req, resp);
```		  
> ###跳转与重定向选择
* 1.请求中有表单数据，而数据比较重要
* 2.请求被Servlet接受后，无法进行处理

<h1>六.session技术</h1>
<h2>1.原理</h2>
> ####用户第一次访问浏览器，浏览器会创建一个session对象给此用户，并将该对象的JSESSIONID使用Cookie技术存储在浏览器中，保证用户的其他请求能够获取同一个对象，也保证了不同的请求能够获取同一个数据

<h2>2.特点</h2>
* 存储在服浏览器端
* 由浏览器创建
* 依赖Cookie技术
* 一次会话
* 默认有限时间30分钟

<h2>3.使用</h2>
*  创建session对象
```
HttpSession hs=req.getSession
```

* 设置session时间
```
hs.setMaxInactiveInterval(int seconds)
```

* 设置session强制失效
```
hs.invalidate();
```
<h2>4.注意</h2>
> ####JSESSIONI存储在Cookie的临时存储空间中，浏览器关闭即失效

