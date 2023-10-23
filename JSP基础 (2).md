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
## JSP内置对象（自带的，不需要new也能使用的对象）
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
**get**：method =“get”和地址栏、超链接（<a href="xx"）请求方式，默认都属于get提交方式
**二者区别**：a:get方式在地址栏上显示请求信息（但是地址栏能够容纳的信息有限4-5kb，如果请求数据过载，则会报错）；post不会显示，Post方式更加安全。
b:文件上传方式，必须是Post。
**统一请求方式request的编码格式**

- get方式如果出现乱码的解决方案：

a:统一每一个变量的编码方式（不推荐）
b：修改server.xml，一次性的更改tomcat默认get提交方式（建议使用tomcat时首先在server.xml中统一get方式的编码）

- post

request.setCharacterEncoding（“utf-8（编码格式）”）
### reponse
响应对象
![](https://cdn.nlark.com/yuque/0/2023/jpeg/34532958/1697425143264-c41cccd4-e876-467f-85b5-9c4ef1a0b290.jpeg)
response：响应对象
#### 常用的方法
 void addCookie(Cookie cookie);服务端向客户端增加cookie
void sendRedirect(String location)：页面跳转的一种方式（重定向）(可能会导致数据丢失）
使用请求转发方式，可以获取到数据，并且地址栏没有改变（仍然保留转发时的页面check.jsp）
void setContetType（String type）：设置服务端响应编码（设置服务端的contentType类型）
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
#### 请求转发、重定向的区别（常考）
|  | 请求转发 | 重定向 |
| --- | --- | --- |
| 
1. 地址栏是否改变
 | 不变 | 改变 |
| 
2. 是否保留第一次请求时的数据
 | 保留 | 不保留 |
| 
3. 请求次数
 | 1 | 2 |
| 
4. 跳转时
 |  |  |

![](https://cdn.nlark.com/yuque/0/2023/jpeg/34532958/1697424205691-ef9eef71-4c46-4657-91cc-7e861bea66a3.jpeg)
#### 转发、重定向
**转发**：  
![](https://cdn.nlark.com/yuque/0/2023/jpeg/34532958/1697425400494-c9f028a2-8160-44c6-b70a-37edd08dbee9.jpeg)
**重定向**
![](https://cdn.nlark.com/yuque/0/2023/jpeg/34532958/1697438667026-c00003db-9067-46d4-8c55-d322fd06c03b.jpeg)
两次请求两次响应
### pageContext
### 

### session
[JSP基础](https://www.yuque.com/u33055369/dk932e/tlh0bnlft4wsnx2b)先看Cookie再看session
#### 机制
![](https://cdn.nlark.com/yuque/0/2023/jpeg/34532958/1697943864226-e2e4ed15-ddbf-4d3b-b495-3f371a48379b.jpeg)
客户端第一次请求服务端时，服务端会产生一个session对象（用于保存该客户的信息）；
每个session对象都会有一个唯一的sessionID（用于区分其他session）；
服务端会产生一个Cookie，并且该Cookie的name为JSESSIONID，value为服务端sessionID的值；
然后服务端会在响应客户端的同时，将该Cookie发送给客户端，至此，客户端有了一个cookie（JSEEIONID）；
因此客户端的Cookie就可以和服务端的session一一对应（JSESSION-sessionID）。
而当客户端第二/n次请求服务端时：服务端会先根据客户端Cookie中的JSESSION去服务端中的session中匹配sessionID，如果匹配成功，说明此用户不是第一次访问，无需登录 
#### 常用方法
String getID（）：获取sessionID
boolean isNEW（）：判断是否是新用户（第一次访问）
void invalidate（）：使session失效（退出登录、注销）
setAttribute（）

void setMaxInactiveInterval(秒):设置最大有效非活动时间
int getMaxInactiveInterval（）：获取最大有效活动时间
### Cookie（客户端，不是内置对象）
Cookie是由服务端产生，再发送给客户端保存
相当于本地缓存的作用：客户端->服务端（hello.mp4）
作用：提高访问服务端的效率，但是安全性较差
#### 常用方法：
产生Cookie：

- public Cookie(String key,String value)
- String getName()：获取name
- String getValue():获取value
- void setMaxAge(int expiry):设置最大有效期（秒）

服务端发送给客户端:
response.addCookie(Cookie cookie)
客户端获取Cookie：
request.getCookies()
a.服务端增减Cookie：response对象；客户端获取对象：request对象
b.不能直接获取某一个单独对象，只能一次性将全部的cookie拿到
