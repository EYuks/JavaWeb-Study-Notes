# 绪论
## JSP：动态网页
动态网页（根据用户操作不同而不同）
动态网页：需要使用到服务端脚本语言（JSP）
JSP：在html中嵌套Java语句
在项目/web.xml中设置初始页面
ps:一般而言，修改web.xml

## CS架构
不足：

- 如果软件升级，那么所有软件都需要升级
- 维护麻烦
- 每一台客户机都需要安装客户端软件

优点：

- 美观，响应快
## BS架构
![](https://cdn.nlark.com/yuque/0/2023/jpeg/34532958/1695817197430-3e287ce4-8ebf-4b1a-9d82-ca6bdac1105d.jpeg)
## 常见状态码
404：资源不存在
200：一切正常
403：权限不足
500：代码有误
## 虚拟主机和虚拟路径
虚拟路径：将web项目配置到webpps以外的目录
docBase：实际路径

## JSP的执行流程
![](https://cdn.nlark.com/yuque/0/2023/jpeg/34532958/1695817238918-cebe9982-dd1a-4521-b85a-ed035aa5c188.jpeg)
## JSP页面元素
### a.脚本Scriptlet
#### i. 
<%  
局部变量，Java语句
%>常用于定义变量
#### ii.
<%!
全局变量，定义方法 
  %>常用于定义方法
#### iii.
<%=输出表达式 %>
### b.指令
#### page指令
<%@ …… %>
##### 属性：

- language：JSP页面使用的脚本语言
- import：导入包
- pageEncoding：文件自身编码 JSP—>Java
- contentType：浏览器解析JSP的编码
#### include指令
### c.注释
#### html注释
<!-- -->可以被客户查看源代码所观察到
#### Java注释
// 
/*  */
#### JSP注释
<%-- --%>
## JSP内置对象（自带的，不需要new，也能使用的对象）
### out
输出对象，向客户端输出内容
### request
请求对象，存储客户端向服务端发送的请求信息
![](https://cdn.nlark.com/yuque/0/2023/jpeg/34532958/1695822378079-5940a144-7a74-47a5-a223-5566daeaeadf.jpeg)
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
#### get方式和post方式
get：metho=“get”和地址栏、超链接（<a href="xx"）请求方式，默认都属于get提交方式
二者区别：a:get方式在地址栏上显示请求信息（但是地址栏能够容纳的信息有限4-5kb，如果请求数据过载，则会报错）；post不会显示，Post方式更加安全。
b:文件上传方式，必须是Post。
统一请求方式request的编码格式
get方式如果出现乱码的解决方案：
a:统一每一个变量的编码方式（不推荐）
b：修改server.xml，一次性的更改tomcat默认get提交方式（建议使用tomcat时首先在server.xml中统一get方式的编码）
post
request.setC
### pageContext
### 

### reponse
### session
