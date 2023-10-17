<a name="qWYCK"></a>
# 绪论
<a name="NmfgX"></a>
## JSP：动态网页
动态网页（根据用户操作不同而不同）<br />动态网页：需要使用到服务端脚本语言（JSP）<br />JSP：在html中嵌套Java语句<br />在项目/web.xml中设置初始页面<br />ps:一般而言，修改web.xml

<a name="X82v4"></a>
## CS架构
不足：

- 如果软件升级，那么所有软件都需要升级
- 维护麻烦
- 每一台客户机都需要安装客户端软件

优点：

- 美观，响应快
<a name="UAue2"></a>
## BS架构
![](https://cdn.nlark.com/yuque/0/2023/jpeg/34532958/1695817197430-3e287ce4-8ebf-4b1a-9d82-ca6bdac1105d.jpeg)
<a name="YQcKx"></a>
## 常见状态码
404：资源不存在<br />200：一切正常<br />403：权限不足<br />500：代码有误
<a name="edDpb"></a>
## 虚拟主机和虚拟路径
虚拟路径：将web项目配置到webpps以外的目录<br />docBase：实际路径

<a name="CL8cw"></a>
## JSP的执行流程
![](https://cdn.nlark.com/yuque/0/2023/jpeg/34532958/1695817238918-cebe9982-dd1a-4521-b85a-ed035aa5c188.jpeg)
<a name="y3ziC"></a>
## JSP页面元素
<a name="JvU9t"></a>
### a.脚本Scriptlet
<a name="QHTOO"></a>
#### i. 
<%  <br />局部变量，Java语句<br />%>常用于定义变量
<a name="wb2R8"></a>
#### ii.
<%!<br />全局变量，定义方法 <br />  %>常用于定义方法
<a name="ev2Xw"></a>
#### iii.
<%=输出表达式 %>
<a name="CHvb7"></a>
### b.指令
<a name="caI7y"></a>
#### page指令
<%@ …… %>
<a name="ksLro"></a>
##### 属性：

- language：JSP页面使用的脚本语言
- import：导入包
- pageEncoding：文件自身编码 JSP—>Java
- contentType：浏览器解析JSP的编码
<a name="TSGPS"></a>
#### include指令
<a name="sKa9b"></a>
### c.注释
<a name="On8bI"></a>
#### html注释
<!-- -->可以被客户查看源代码所观察到
<a name="J64or"></a>
#### Java注释
// <br />/*  */
<a name="hJcjf"></a>
#### JSP注释
<%-- --%>
<a name="IXGdG"></a>
## JSP内置对象（自带的，不需要new也能使用的对象）
<a name="QLts3"></a>
### out
输出对象，向客户端输出内容
<a name="nOoTQ"></a>
### request
请求对象，存储客户端向服务端发送的请求信息<br />![](https://cdn.nlark.com/yuque/0/2023/jpeg/34532958/1695822378079-5940a144-7a74-47a5-a223-5566daeaeadf.jpeg)
<a name="p1oL9"></a>
#### 常见方法

- String getparamater(String name):根据请求的字段名Key，返回字段值value
- String[ ] getParameterValues(String name):根据请求的字段名Key，返回多个字段值value（checkbox）（根据name返回value值）
- setCharacterEncoding（“编码格式”）:设置请求编码（默认编码为iso-8859-1）
- getRequestDispatcher("b.jap").forward(request,response):请求转发的方式跳转页面 
- getServerContext() :获取项目的ServletContext对象
```html
<form>
  用户名：<input type="text" name="uname" /><br/>
  密码：<input type="password" name="upwd"/><br/>
  年龄：<input type="text" name="uage"/><br/>
  爱好：<br/>:
  <input type="checkbox" name="uhobbies" value="足球"/>足球
  <input type="checkbox" name="uhobbies" value="篮球"/>篮球
  <input type="checkbox" name="uhobbies"value="乒乓球"/>乒乓球<br/>
  <input type="submit" value="注册"/>
```
```html
<%
  request.setCharacterterEcoding("utf-8");
  String name=request.getParameter("uname");
  int age=request.getParameter("uage");
  String pwd=request.getParameter("upwd");
  String[] hobbies=resquest.getParameterValues("uhobbies");
%>
  注册成功，信息如下：<br/>
  姓名：<%=name%><br/>
  年龄：<%=age%><br/>
  密码：<%=pwd%><br/>
  爱好：<br/>
    <%
      for(String hobby:hobbies)
      {
      	out.print(hobby+"%nbsp"//out打印页面
      }
    %><br/>
  
```
<a name="EordJ"></a>
#### get方式和post方式
**get**：method =“get”和地址栏、超链接（<a href="xx"）请求方式，默认都属于get提交方式<br />**二者区别**：a:get方式在地址栏上显示请求信息（但是地址栏能够容纳的信息有限4-5kb，如果请求数据过载，则会报错）；post不会显示，Post方式更加安全。<br />b:文件上传方式，必须是Post。<br />**统一请求方式request的编码格式**

- get方式如果出现乱码的解决方案：

a:统一每一个变量的编码方式（不推荐）<br />b：修改server.xml，一次性的更改tomcat默认get提交方式（建议使用tomcat时首先在server.xml中统一get方式的编码）

- post

request.setCharacterEncoding（“utf-8（编码格式）”）
<a name="V4Hla"></a>
### reponse
响应对象<br />![](https://cdn.nlark.com/yuque/0/2023/jpeg/34532958/1697425143264-c41cccd4-e876-467f-85b5-9c4ef1a0b290.jpeg)<br />response：响应对象
<a name="SxqBq"></a>
#### 常用的方法
 void addCookie(Cookie cookie);服务端向客户端增加cookie<br />void sendRedirect(String location)：页面跳转的一种方式（重定向）(可能会导致数据丢失）<br />使用请求转发方式，可以获取到数据，并且地址栏没有改变（仍然保留转发时的页面check.jsp）<br />void setContetType（String type）：设置服务端响应编码（设置服务端的contentType类型）
```html
<body>
  <form>
    
  </form>
</body>
```
```html
<body>
  <%
    request.setCharacterEncoding("utf-8");
    String name =request.getParamater("uname");
    String pwd=request.getParameter("upwd");
    if()(name.equals("zs")&&pwd.equals("abc")){//假设用户名为zs，密码为abc
      request.getRequestDispatcher("success.jsp").forward();//请求转发
     //response.sendRedirect("success.jsp");
    }else{//登录失败
      out.print("用户名或密码有误！"):
    }
  %>
</body>
```
```html
<body>
  登录成功！<br/>
  欢迎<%
    String name =request.getParameter("uname");
    out.print(name);
</body>
```
<a name="jICEq"></a>
#### 请求转发、重定向的区别（常考）
|  | 请求转发 | 重定向 |
| --- | --- | --- |
| <br />1. 地址栏是否改变<br /> | 不变 | 改变 |
| <br />2. 是否保留第一次请求时的数据<br /> | 保留 | 不保留 |
| <br />3. 请求次数<br /> | 1 | 2 |
| <br />4. 跳转时<br /> |  |  |

![](https://cdn.nlark.com/yuque/0/2023/jpeg/34532958/1697424205691-ef9eef71-4c46-4657-91cc-7e861bea66a3.jpeg)
<a name="xQFc1"></a>
#### 转发、重定向
**转发**：  <br />![](https://cdn.nlark.com/yuque/0/2023/jpeg/34532958/1697425400494-c9f028a2-8160-44c6-b70a-37edd08dbee9.jpeg)<br />**重定向**<br />![](https://cdn.nlark.com/yuque/0/2023/jpeg/34532958/1697438667026-c00003db-9067-46d4-8c55-d322fd06c03b.jpeg)<br />两次请求两次响应
<a name="YlASM"></a>
### pageContext
<a name="uRphq"></a>
### <br />
<a name="KlrIO"></a>
### session
[JSP基础](https://www.yuque.com/u33055369/dk932e/tlh0bnlft4wsnx2b)先看Cookie再看session
<a name="EIJd2"></a>
### Cookie（客户端，不是内置对象）
Cookie是由服务端产生，再发送给客户端保存<br />相当于本地缓存的作用：客户端->服务端（hello.mp4）<br />作用：提高访问服务端的效率，但是安全性较差
<a name="wNVki"></a>
#### 常用方法：
产生Cookie：

- public Cookie(String key,String value)
- String getName()：获取name
- String getValue():获取value
- void setMaxAge(int expiry):设置最大有效期（秒）

服务端发送给客户端:<br />response.addCookie(Cookie cookie)<br />客户端获取Cookie：<br />request.getCookies()<br />a.服务端增减Cookie：response对象；客户端获取对象：request对象<br />b.不能直接获取某一个单独对象，只能一次性将全部的cookie拿到
