# JavaWeb

## 1、基本概念

### 1.1、前言

web开发：

- web，网页的意思，www.baidu.com
- 静态web
  - html，css
  - 提供给所有人看的数据始终不会发生变化
- 动态web
  - 淘宝，几乎所有网站
  - 提供给所有人看的数据始终会发生变化，每个人在不同的时间，不同的地点看到的东西各不相同
  - 技术栈：Servlet/jsp，asp，php

在Java中，动态web资源开发的技术统称为javaweb

### 1.2、web应用程序

web应用程序：可以提供浏览器访问的程序；

- a.html、b.html。。。多个web资源，这些web资源可以被外界访问，对外界提供服务
- 能访问到的任何一个页面或资源，都存在于这个世界的某一个角落的计算机上
- url
- 这个统一的web资源会被放在同一个文件夹下，web应用程序--》tomcat：服务器
- 一个web应用由多个部分组成（静态web、动态web）
  - html、css、js
  - jsp、servlet
  - Java程序
  - jar包
  - 配置文件（prope'rties）

web应用程序编写完毕后，若想提供给外界访问：需要给一个服务器来统一管理；

### 1.3、静态web

- .htm、.html这些都是网页的后缀，如果服务器上一直存在这些东西，我们就可以直接进行读取

![image-20210801163951974](D:\Github\MyNotes\javaweb\image-20210801163951974.png)

- 静态web存在的缺点
  - web页面无法动态更新，所有用户看到的都是同一个页面
    - 轮播图，点击特效：伪动态
    - JavaScript【实际开发中，他用的最多】
    - VBScript
  - 他无法和数据库交互（数据无法持久化，用户无法交互）

### 1.4、动态web

页面会动态展示：“web的页面展示的效果因人而异”

![image-20210801170102022](D:\Github\MyNotes\javaweb\image-20210801170102022.png)

缺点：

- 假如服务器的动态web资源出现了错误，我们需要重新编写我们的**后台程序**，重新发布；
  - 停机维护

优点：

- web页面可以动态更新，所有用户看到的都不是同一个页面
- 他可以和数据库交互（数据持久化：注册，商品信息，用户信息）

## 2、web服务器

### 2.1、技术讲解

asp:

- 微软：国内最早流行的就是asp
- 在html中就嵌入了vb的脚本，asp+com；
- 在asp开发中，基本一个页面都有几千行的业务代码，页面极其混乱
- 维护成本高
- c#
- IIS服务器

php

- php开发速度很快，功能强大，跨平台，代码简单
- 无法承载大访问量情况（局限型）

**JSP/Servlet**

B/S：浏览器和服务器

C/S：客户端和服务器

- sun公司主推的B/S架构
- 基于java语言的（所有的大公司，或者一些开源的组件，都是用Java写的）
- 可以承载三高（高并发，高可用，高性能）问题带来的影响
- 语法像ASP，ASP-》JSP，加强市场的竞争度

### 2.2、web服务器

服务器是一种被动的操作，用来处理一些用户的请求和给用户一些响应信息

**IIS**

微软的，asp...windows中自带的

**Tomcat**

![image-20210803164027377](D:\Github\MyNotes\javaweb\image-20210803164027377.png)

Tomcat是Apache 软件基金会（Apache Software Foundation）的Jakarta 项目中的一个核心项目，最新的Servlet 和JSP 规范总是能在Tomcat 中得到体现。因为Tomcat 技术先进、性能稳定，而且**免费**，因而深受Java 爱好者的喜爱并得到了部分软件开发商的认可，成为目前比较流行的Web 应用服务器。

Tomcat 服务器是一个免费的开放源代码的Web 应用服务器，属于轻量级应用[服务器](https://baike.baidu.com/item/服务器)，在中小型系统和并发访问用户不是很多的场合下被普遍使用，是开发和调试JSP 程序的首选。对于一个java初学web来说，是最佳选择。

Tomcat 实际上运行JSP 页面和Servlet。目前Tomcat最新版本为10.0.5**。**

**工作3-5年可以尝试手写tomcat服务器**

下载 tomcat：

1. 安装or解压
2. 了解配置文件及项目目录
3. 这个东西的作用

## 3、Tomcat

### 3.1、安装Tomcat

![image-20210803165340561](D:\Github\MyNotes\javaweb\image-20210803165340561.png)

### 3.2、Tomcat启动和配置

文件夹作用

![image-20210803165813800](D:\Github\MyNotes\javaweb\image-20210803165813800.png)

启动、关闭 tomcat

![image-20210803171137215](D:\Github\MyNotes\javaweb\image-20210803171137215.png)

访问测试：localhost:8080

1. java环境没有配置
2. 闪退问题：需要配置兼容性
3. 乱码问题：配置文件中设置

### 3.3、配置

![image-20210803171442116](D:\Github\MyNotes\javaweb\image-20210803171442116.png)

可以配置启动的端口号

- tomcat默认端口号：8080
- mysql默认端口号：3306
- http：80
- https：443

<Connector port="8080" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443" />

配置主机名称

- 默认的主机名为：localhost-》127.0.0.1
- 默认的网站应用存放的位置为：webapps

<Host name="localhost"  appBase="webapps"
            unpackWARs="true" autoDeploy="true">

### 3.4、发布一个web网站

不会就先模仿

- 将自己写的网站，放到服务器（tomcat）中指定的web应用的文件夹（webapps）下，就可以访问了

网站应该有的结构

```java
--webapps：Tomcat服务器的web目录
    -ROOT
    -money：网站的目录名
    	- WEB-INF
    		-classes：Java 程序
    		-lib：web应用所依赖的jar包
    		-web.xml 网站的配置文件
    	-index.html/index.jsp 默认的首页
    	-static
    		-css
    			-style.css
    		-js
    		-img
    	-...
```

## 4、HTTP

### 4.1、什么是http

超文本传输协议（Hyper Text Transfer Protocol，HTTP）是一个简单的请求-响应协议，它通常运行在[TCP](https://baike.baidu.com/item/TCP/33012)之上。

- 文本：html、字符串。。。
- 超文本：图片、文本、视频、定位、地图。。。
- 80

HTTPS：安全的

- 443

### 4.2、两个时代

- http1.0
  - http/1.0：客户端可以与web服务器连接，只能获得一个web资源，断开连接
- http2.0
  - http/1.1：客户端可以与web服务器连接，可以获得多个web资源

### 4.3、Http请求

- 客户端---发请求(request)---服务器

百度：

```java
请求 URL: https://www.baidu.com/   请求地址
请求方法: GET   get方法/post方法
状态代码: 200 OK  状态码：200
远程地址: 220.181.38.150:443  
引用站点策略: unsafe-url
```

```java
Accept: text/html
Accept-Encoding: gzip, deflate, br
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8,en-GB;q=0.7,en-US;q=0.6   语言
Cache-Control: max-age=0
Connection: keep-alive
```

#### 4.3.1、请求行

- 请求行中的请求方式：GET
- 请求方式：**GET,POST**,HEAD,DELETE,PUT,TRACT......
  - get：请求能够携带的参数比较少，大小有限制，会在浏览器的URL地址栏显示数据内容，不安全，但是高效
  - post：请求能够携带的参数没有限制，大小没有限制，不会在浏览器的URL地址栏显示数据内容，安全，但不高效

#### 4.3.2、消息头

```java
Accept：告诉浏览器，他所支持的数据类型
Accept-Encoding：支持那种编码格式   GBK  UTF-8  GB3212  ISO8859-1
Accept-Language: 告诉浏览器，他的语言环境
Cache-Control：缓测控制（浏览器存在缓存，经常登录的网页不用每次都登录）
Connection：告诉浏览器，请求完成是断开还是保持连接
HOST：主机
```



### 4.4、http响应

- 服务器---响应---客户端

百度：

```java
Cache-Control: private   缓测控制
Connection: keep-alive   连接
Content-Encoding: gzip   编码
Content-Type: text/html;charset=utf-8   类型
```

#### 4.4.1、响应体

```java
Accept：告诉浏览器，他所支持的数据类型
Accept-Encoding：支持那种编码格式   GBK  UTF-8  GB3212  ISO8859-1
Accept-Language: 告诉浏览器，他的语言环境
Cache-Control：缓测控制（浏览器存在缓存，经常登录的网页不用每次都登录）
Connection：告诉浏览器，请求完成是断开还是保持连接
HOST：主机
Refresh:刷新，告诉客户端，多久刷新一次
Location：让网页重新定位
```

#### 4.4.2、响应状态码

200：请求响应成功

3xx：请求重定向

- 重定向：你重新到我给你的新位置去

4xx：找不到资源  404

- 资源不存在

5xx：服务器代码错误  500  502：网关错误

## 5、Maven

**我为什么要学习这个技术？**

1. 在Javaweb开发中，需要使用大量的jar包，我们需要手动去导入
2. 如何能够让一个东西自动帮我导入和配置这个jar包

由此，Maven诞生了！

pom.xml修改之后要重启idea

### 5.1、Maven项目架构管理工具

我们目前用来就是方便导入jar包的！

Maven的核心思想：**约定大于配置**

- 有约束，不要去违反

Maven会规定好你该如何去编写我们的java代码，必须要按照这个规范来

### 5.2、下载安装Maven

官网：[Maven – Welcome to Apache Maven](https://maven.apache.org/)

![image-20210807172747188](D:\Github\MyNotes\javaweb\image-20210807172747188.png)

下载完解压

电脑上所有环境放在一个文件夹下方便管理

### 5.3、配置环境变量

在我们的系统环境变量中

配置如下配置：

- M2_HOME  maven目录下的bin目录
- MAVEN_HOME  maven的目录
- 在系统的path中配置MAVEN_HOME\bin

### 5.4、阿里云镜像

- 镜像：mirrors
  - 作用：加速我们的下载
- 国内建议使用阿里云镜像

```xml
<mirror>
        <id>nexus-aliyun</id>
        <mirrorOf>*,!jeecg,!jeecg-snapshots</mirrorOf>
        <name>Nexus aliyun</name>
        <url>http://maven.aliyun.com/nexus/content/groups/public</url> 
    </mirror> 
```

### 5.5、本地仓库

在本地的仓库，远程仓库；

**建立一个本地仓库:**localRepository

```xml
<localRepository>D:\JavaTools\apache-maven-3.6.3-bin\apache-maven-3.6.3\maven-repo</localRepository>
```

### 5.6、在idea中使用maven

1. 启动idea
2. 创建一个mavenWeb项目

![image-20210813100033506](D:\Github\MyNotes\javaweb\image-20210813100033506.png)

![image-20210813100226303](D:\Github\MyNotes\javaweb\image-20210813100226303.png)

![image-20210813100845835](D:\Github\MyNotes\javaweb\image-20210813100845835.png)

![image-20210813100926194](D:\Github\MyNotes\javaweb\image-20210813100926194.png)

3. 等待项目初始化完毕

![image-20210813101256848](D:\Github\MyNotes\javaweb\image-20210813101256848.png)

![image-20210813101602403](D:\Github\MyNotes\javaweb\image-20210813101602403.png)

4. 观察maven仓库中多了什么东西

5. idea中的maven设置

   注意：idea创建成功后，看一眼maven配置

![image-20210813102641805](D:\Github\MyNotes\javaweb\image-20210813102641805.png)

![image-20210813103054856](D:\Github\MyNotes\javaweb\image-20210813103054856.png)

6. 到这里maven在idea的配置和使用就完成了

### 5.7、创建 一个普通的maven项目

![image-20210813103706318](D:\Github\MyNotes\javaweb\image-20210813103706318.png)

![image-20210813103847810](D:\Github\MyNotes\javaweb\image-20210813103847810.png)

![image-20210813132010322](D:\Github\MyNotes\javaweb\image-20210813132010322.png)

这个只有web项目才会有

![image-20210813131825892](D:\Github\MyNotes\javaweb\image-20210813131825892.png)

### 5.8、标记文件夹功能

**第一种方式 ：**

![image-20210813132510255](D:\Github\MyNotes\javaweb\image-20210813132510255.png)

![image-20210813132700752](D:\Github\MyNotes\javaweb\image-20210813132700752.png)

**第二种方式：根据需要选择文件夹类型**

![image-20210813133005976](D:\Github\MyNotes\javaweb\image-20210813133005976.png)

![image-20210813133217560](D:\Github\MyNotes\javaweb\image-20210813133217560.png)

### 5.9、在idea中配置Tomcat

![image-20210813133418802](D:\Github\MyNotes\javaweb\image-20210813133418802.png)

![image-20210813133508712](D:\Github\MyNotes\javaweb\image-20210813133508712.png)

![image-20210813133709769](D:\Github\MyNotes\javaweb\image-20210813133709769.png)

![image-20210813134420212](D:\Github\MyNotes\javaweb\image-20210813134420212.png)

新建一个artifacts

![image-20210813134608054](D:\Github\MyNotes\javaweb\image-20210813134608054.png)

解决警告问题（必须配置）

**为什么会有这个问题：我们访问一个网站，需要指定一个文件夹名字**

![image-20210813134649759](D:\Github\MyNotes\javaweb\image-20210813134649759.png)

![image-20210813135246101](D:\Github\MyNotes\javaweb\image-20210813135246101.png)

![image-20210813135349196](D:\Github\MyNotes\javaweb\image-20210813135349196.png)

![image-20210813135945205](D:\Github\MyNotes\javaweb\image-20210813135945205.png)

### 5.10、pom文件

pom.xml是maven的核心配置文件

![image-20210813140503576](D:\Github\MyNotes\javaweb\image-20210813140503576.png)

```xml
<?xml version="1.0" encoding="UTF-8"?>

<!--maven的版本和头文件-->
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

<!--这里就是我们刚才配置的GAV-->
  <groupId>com.kuang</groupId>
  <artifactId>javaweb-01-maven</artifactId>
  <version>1.0-SNAPSHOT</version>
<!--  packaging：项目的打包方式
jar：Java应用
war：javaWeb应用
-->
  <packaging>war</packaging>

<!--  可以删除，就是一些名称-->
  <name>javaweb-01-maven Maven Webapp</name>
  <!-- FIXME change it to the project's website -->
  <url>http://www.example.com</url>

<!--  配置-->
  <properties>
<!--    项目的默认构建编码-->
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
<!--    编译输出的目标版本-->
    <maven.compiler.source>1.8</maven.compiler.source>
    <maven.compiler.target>1.8</maven.compiler.target>
  </properties>

<!--  项目依赖-->
  <dependencies>
<!--    具体依赖的jar包配置文件-->
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.11</version>
      <scope>test</scope>
    </dependency>
  </dependencies>

<!--  项目构建用的东西-->
  <build>
    <finalName>javaweb-01-maven</finalName>
    <pluginManagement><!-- lock down plugins versions to avoid using Maven defaults (may be moved to parent pom) -->
      <plugins>
        <plugin>
          <artifactId>maven-clean-plugin</artifactId>
          <version>3.1.0</version>
        </plugin>
        <!-- see http://maven.apache.org/ref/current/maven-core/default-bindings.html#Plugin_bindings_for_war_packaging -->
        <plugin>
          <artifactId>maven-resources-plugin</artifactId>
          <version>3.0.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-compiler-plugin</artifactId>
          <version>3.8.0</version>
        </plugin>
        <plugin>
          <artifactId>maven-surefire-plugin</artifactId>
          <version>2.22.1</version>
        </plugin>
        <plugin>
          <artifactId>maven-war-plugin</artifactId>
          <version>3.2.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-install-plugin</artifactId>
          <version>2.5.2</version>
        </plugin>
        <plugin>
          <artifactId>maven-deploy-plugin</artifactId>
          <version>2.8.2</version>
        </plugin>
      </plugins>
    </pluginManagement>
  </build>
</project>

```

干净的maven：没有dependencies

![image-20210813142043668](D:\Github\MyNotes\javaweb\image-20210813142043668.png)

![image-20210813142912815](D:\Github\MyNotes\javaweb\image-20210813142912815.png)

![image-20210813143027687](D:\Github\MyNotes\javaweb\image-20210813143027687.png)

maven由于他的约定大于配置，我们之后可能遇到我们写的配置文件，无法被导出或者生效的问题，解决方案：

```xml
<!--在build中配置resources，来防止我们资源导出失败的问题-->
    <build>
        <resources>
            <resource>
                <directory>src/main/resources</directory>
                <excludes>
                    <exclude>**/*.properties</exclude>
                    <exclude>**/*.xml</exclude>
                </excludes>
                <filtering>false</filtering>
            </resource>
            <resource>
                <directory>src/main/java</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>false</filtering>
            </resource>
        </resources>
    </build>
```

### 5.11、idea目录树

![image-20210813144538116](D:\Github\MyNotes\javaweb\image-20210813144538116.png)

### 5.12、解决遇到的问题

1. maven 3.6.2

Unable to import maven project：版本不兼容

解决方法：降级为3.6.1

2. Tomcat闪退

   解决方法：观察startup.bat文件，里面有个卡特琳娜文件，打开此文件，查看到javahome和jrehome，如果目录不一样就会闪退，不建议修改，否则idea的tomcat可能无法使用。

3. IDEA中每次都要重复配置maven

   在idea中的全局默认配置中去配置

   ![image-20210813150443070](D:\Github\MyNotes\javaweb\image-20210813150443070.png)

   ![image-20210813150555855](D:\Github\MyNotes\javaweb\image-20210813150555855.png)

   

4. maven项目中tomcat无法配置

5. maven默认web项目中的web.xml版本问题

版本太老

![image-20210813151303389](D:\Github\MyNotes\javaweb\image-20210813151303389.png)

替换为webapp4.0版本和tomcat一致

```xml
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
                      http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
  version="4.0"
  metadata-complete="true">

  <display-name>Welcome to Tomcat</display-name>
  <description>
     Welcome to Tomcat
  </description>

</web-app>

```

6. maven仓库的使用

地址：[Maven Repository: Search/Browse/Explore (mvnrepository.com)](https://mvnrepository.com/)

![image-20210813152351857](D:\Github\MyNotes\javaweb\image-20210813152351857.png)

找servlet-api，使用最多的

![image-20210813152631996](D:\Github\MyNotes\javaweb\image-20210813152631996.png)

![image-20210813152824330](D:\Github\MyNotes\javaweb\image-20210813152824330.png)

![image-20210813152940079](D:\Github\MyNotes\javaweb\image-20210813152940079.png)

```xml
<!-- https://mvnrepository.com/artifact/javax.servlet/javax.servlet-api -->
<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>javax.servlet-api</artifactId>
    <version>4.0.1</version>
    作用域：生产，删除，用于所有
    <scope>provided</scope>
</dependency>
```



## 6、Servlet

### 6.1、serlet简介

- servlet就是sun公司开发动态web的一门技术
- sun在这些API中提供一个接口叫做：Servlet，如果你想开发一个servlet程序，需要完成两个步骤：
  - 编写一个类，实现Servlet接口
  - 把开发好的Java类部署到web服务器中

**把现实了Servlet接口的Java程序叫做servlet**

### 6.2、hello servlet

Servlet接口sun公司有两个默认的实现类：HttpServlet、GenericServlet

1. 构建一个普通的maven项目，删掉里面的src目录，以后的学习就在这个项目里面建立Moudel；这个空的工程就是maven的主工程；

![image-20210905194420015](D:\Github\MyNotes\javaweb\image-20210905194420015.png)

![image-20210905214101615](D:\Github\MyNotes\javaweb\image-20210905214101615.png)

2. 关于Maven父子工程的理解

在父项目中会有

```xml
	<modules>
        <module>servlet-01</module>
    </modules>
```

子项目中会有：

```xml
    <parent>
        <artifactId>javaweb-02-servlet</artifactId>
        <groupId>com.kuang</groupId>
        <version>1.0-SNAPSHOT</version>
    </parent>
```

父项目中的Java子项目可以直接使用

```java
son extends father
```

3. Maven环境优化

   1. 修改web.xml为最新的
   2. 将maven的结构搭建完整

   ![image-20210905202132993](D:\Github\MyNotes\javaweb\image-20210905202132993.png)

4. 编写一个Servlet程序

   1. 编写一个普通类
   2. 实现Servlet接口，这里直接继承HttpServlet

   ```java
   public class HelloWorld extends HttpServlet {
   
       //由于get或者post知识请求实现的不同方式，可以相互调用，业务逻辑都一样
       @Override
       protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
   //        ServletOutputStream outputStream = resp.getOutputStream();输出流
   //        ServletInputStream inputStream = req.getInputStream();输入流
           PrintWriter printWriter = resp.getWriter(); //响应流
           printWriter.print("Hello,Servlet");
       }
   
       @Override
       protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
           super.doPost(req, resp);
       }
   }
   ```

5. 编写servlet的映射

   为什么需要映射：我们写的是Java程序，但是要通过浏览器访问。而浏览器需要连接web服务器，所以我们需要在web服务中注册我们写的Servlet，还需要给他一个浏览器能够访问的路径；

   ```xml
       <!--注册servlet-->
       <servlet>
           <servlet-name>hello</servlet-name>
           <servlet-class>com.kuang.servlet.HelloServlet</servlet-class>
       </servlet>
       <!--Servlet的请求路径-->
       <servlet-mapping>
           <servlet-name>hello</servlet-name>
           <url-pattern>/hello</url-pattern>
       </servlet-mapping>
   ```

6. 配置tomcat

   注意：配置项目

7. 启动测试

### 6.3、Servlet原理

servlet是由web服务器调用，web服务器在收到浏览器请求之后，会:

![image-20210906111850420](D:\Github\MyNotes\javaweb\image-20210906111850420.png)

### 6.4、mapping问题

1. 一个servlet可以指定一个映射路径

   ```xml
   <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello</url-pattern>
    </servlet-mapping>
   ```

2. 一个servlet可以指定多个映射路径

   ```xml
   <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello</url-pattern>
    </servlet-mapping>
   <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello1</url-pattern>
    </servlet-mapping>
   <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello2</url-pattern>
    </servlet-mapping>
   <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello3</url-pattern>
    </servlet-mapping>
   ```

3. 一个servlet可以指定通用映射路径

   ```xml
   <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello/*</url-pattern>
    </servlet-mapping>
   ```

4. 默认请求路径(屏蔽index.jsp，优先级最高)

   ```xml
   <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/*</url-pattern>
    </servlet-mapping>
   ```

5. 指定一些后缀和前缀

   注意点：*前面不能加映射的路径/

   ```xml
   <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>*.fuchaoran</url-pattern>
    </servlet-mapping>
   ```

6. 优先级问题

   指定了固有的映射路径优先级最高，如果找不到就会找默认请求路径

```xml
<servlet>
        <servlet-name>error</servlet-name>
        <servlet-class>com.kuang.servlet.ErrorServlet</servlet-class>
</servlet>
<servlet-mapping>
        <servlet-name>error</servlet-name>
        <url-pattern>/*</url-pattern>
</servlet-mapping>
```

### 6.5、ServletContext

web容器在启动的时候，它会为每个web程序都创建一个对应的ServletContext对象，它代表了当前的web应用；

#### 6.5.1、共享数据

我在这个servlet中保存的数据，可以在另外一个servlet中得到

![image-20210906211850582](D:\Github\MyNotes\javaweb\image-20210906211850582.png)

放置数据的类：

```java
public class HelloServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("Hello");
        //this.getInitParameter(); 初始化参数
        //this.getServletConfig(); serlevt配置
        //this.getServletContext(); servlet上下文
        ServletContext context = this.getServletContext();

        String username = "fuchaoran"; //数据
        context.setAttribute("username",username); //将一个数据保存在ServletContext中。名字为username。值为username
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.doPost(req, resp);
    }
}
```

读取数据的类：

```java
public class GetServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        ServletContext context = this.getServletContext();
        String username = (String) context.getAttribute("username");

        resp.setContentType("text/html");
        resp.setCharacterEncoding("utf-8");
        resp.getWriter().print("名字："+username);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

    }
}
```

配置xml：

```xml
<servlet>
        <servlet-name>hello</servlet-name>
        <servlet-class>com.kuang.servlet.HelloServlet</servlet-class>
    </servlet>
    <servlet>
        <servlet-name>getc</servlet-name>
        <servlet-class>com.kuang.servlet.GetServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>hello</servlet-name>
        <url-pattern>/hello</url-pattern>
    </servlet-mapping>
    <servlet-mapping>
        <servlet-name>getc</servlet-name>
        <url-pattern>/getc</url-pattern>
    </servlet-mapping>
```

#### 6.5.2、获取初始化参数

```xml
    <!--配置一些web应用的初始化参数-->
    <context-param>
        <param-name>url</param-name>
        <param-value>jdbc:musql://localhost:3306/mybatis</param-value>
    </context-param>
```

```java
@Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        ServletContext context = this.getServletContext();
        String url = context.getInitParameter("url");
        resp.getWriter().print(url);
    }
```

#### 6.5.3、请求转发

![image-20210906212308262](D:\Github\MyNotes\javaweb\image-20210906212308262.png)

```java
@Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        ServletContext context = this.getServletContext();
        //RequestDispatcher requestDispatcher = context.getRequestDispatcher("/gp");//转发的请求路径
        //requestDispatcher.forward(req,resp); //调用forward实现请求转发
        context.getRequestDispatcher("/gp").forward(req,resp);
    }
```

#### 6.5.4、读取资源文件

Properties

- 在Java目录下新建properties
- 在resources目录下新建properties

发现：都打包在同一目录下：classes，我们俗称这个路径为classpath

![image-20210906214456248](D:\Github\MyNotes\javaweb\image-20210906214456248.png)

思路：需要一个文件流

```xml
username=root
password=123456
```



```java
public class ServletDemo05 extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        InputStream is = this.getServletContext().getResourceAsStream("/WEB-INF/classes/db.properties");
        Properties prop = new Properties();
        prop.load(is);
        String username = prop.getProperty("username");
        String password = prop.getProperty("password");

        resp.getWriter().print(username+":"+password);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.doPost(req, resp);
    }
}
```

### 6.6、HttpServletResponse

web服务器接收到客户端的http请求，针对这个请求，分别创建一个代表请求的HttpServletResquest对象，代表响应的一个HttpServletResponse；

- 如果要获取客户端请求过来的参数：找HttpServletResquest
- 如果要给客户端相应一些信息：找HttpServletResponse

#### 6.6.1、简单分类

**负责向浏览器发送数据的方法：**

- ```java
  ServletOutputStream getOutputStream() throws IOException;
  PrintWriter getWriter() throws IOException;
  ```

- 

### 6.7、HttpServletResquest

#  面试题



1、tomcat里面修改配置文件夹中的server.xml文件的localhost为其他浏览器是否能访问到8080端口？

答：不能访问到，需要去修改windows系统中的hosts文件

2、网站是如何进行访问的？

答：

1. 输入一个域名；回车

2. 检查本机的C:\Windows\System32\drivers\etc\hosts配置文件有没有这个域名的映射

   1. 有：直接返回对应的ip地址，这个地址中，有我们需要访问的web程序，可以直接访问

      ```java 
      127.0.0.1       localhost
      ```

   2. 没有：去DNS服务器上找，找到的话就返回，找不到就显示找不到

![image-20210803213155508](D:\Github\MyNotes\javaweb\image-20210803213155508.png)

3、当你的浏览器中地址栏输入地址并回车的一瞬间到页面能够展示回来，经历了什么？

