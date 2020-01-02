# Tomcat

## 简介
&nbsp; &nbsp; &nbsp; &nbsp; Tomcat 服务器是一个免费的开放源代码的Web 应用服务器，属于轻量级应用服务器，在中小型系统和并发访问用户不是很多的场合下被普遍使用，是开发和调试JSP 程序的首选。对于一个初学者来说，可以这样认为，当在一台机器上配置好Apache 服务器，可利用它响应HTML页面的访问请求。实际上Tomcat 部分是Apache 服务器的扩展，但它是独立运行的，所以当你运行tomcat 时，它实际上作为一个与Apache 独立的进程单独运行的。<br>
&nbsp; &nbsp; &nbsp; &nbsp; 尽管Tomcat也可以作为独立的Java Web服务器，但在对静态资源(HTML、图像文件等)的处理速度，Web服务器管理等方面都不如Apache、IIS服务器等其他专业的HTTP服务器，因此在实际应用中，常常把Tomcat与其他的HTTP服务器集成使用。对于不支持Servlet/JSP的HTTP服务器，可以通过Tomcat服务器来运行Servlet/JSP组件。<br>
&nbsp; &nbsp; &nbsp; &nbsp; 当Tomcat与其他HTTP服务器集成时，Tomcat服务器的工作模式通常为进程外的Servlet容器，Tomcat服务器与其他HTTP服务器之间通过专门的插件来通信。

## 解压目录简介
Tomcat的目录结构如下：<br>
bin：可执行文件（如启动和关闭Tomcat，有Windows和Linux脚本） <br>
conf：存放各种配置文件 <br>
lib：依赖的所有的jar包 <br>
logs：日志文件 <br>
temp：临时文件 <br>
webapps：存放web应用（默认的两个web应用，admin和manager，用来管理Tomcat的web服务）。<br>
work：工作目录（jsp经过编译后生成的servlet）

## 配置文件简介
server.xml——Tomcat中最重要的配置文件。定义了Tomcat的体系结构，包括连接器端口、连接数、集群、虚拟目录、访问日志等 <br>
web.xml——默认文件的设置 <br>
context.xml——全局context的配置文件，包括JNDI（Java Naming and Directory Interface,Java命名和目录接口）等信息的配置 <br>
tomcat-user.xml——Tomcat管理员身份配置文件，关键是设置管理员的账户和密码 <br>
logging.properties——Tomcat日志配置文件，可以修改默认Tomcat日志路径和名称

## Tomcat工作原理
&nbsp; &nbsp; &nbsp; &nbsp; 当客户请求某个资源时，Servlet 容器使用 ServletRequest 对象把客户的请求信息封装起 来，然后调用 Java Servlet API 中定义的 Servlet 的一些生命周期方法，完成 Servlet 的执行， 接着把 Servlet 执行的要返回给客户的结果封装到 ServletResponse 对象中，最后 Servlet 容 器把客户的请求发送给客户，完成为客户的一次服务过程。

## Tomcat工作模式
（1）：独立的Servlet容器（默认）<br>
（2）：进程内的Servlet容器（基于JNI）<br>
（3）：进程外的Servlet容器（基于IPC）<br>
  JNI:Java Native Interface，本地通信接口，通过这个接口，Java 程序可以和其他语言编写的本地程序进行通信。<br>
  IPC:Inter Process Communication,进程间通信<br>
  Tomcat既可以作为独立的容器，又可以和其他Web服务器集成（例如IIS，Apache）作为进程内、进程间Servlet容器<br>
  Servlet容器分为：<br>
  1.&nbsp; Web服务器插件：在其他的WEB服务器内部地址空间打开一个JVM，Java容器在这个开辟的JVM上运行Servlet<br>
  2.&nbsp; Java容器

## Tomcat组织结构

```
<Server>顶层类元素，可包含多个 Service
	<Service>顶层类元素，可包含一个 Engine 和多个 Connector，本身并不能处理客户请求
		<Connector/>连接器元素，代表通信接口，本身并不能处理客户请求
		<Engine>容器元素，为 Service 处理客户请求，可包含多个 Host
			<Host>容器元素，为 Host 处理客户请求，可包含多个 Context
				<Context/>容器元素，为 Web 应用处理客户请求
			</Host>
		</Engine>
	</Service>
</Server>
```
Connector 组件表示一个接口，通过这个接口接收客户的请求，然后发送给其他的容器组件，最后再把服务器的响应结果传递给客户。 <br>

容器类元素：<br>
上面介绍的 3 个组件：server,service,connector本身并不能处理客户请求，也不能生成响应。在 Tomcat 中只有 3 个组件是可以处理客户请求并生成响应的，这 3 个组件分别是 Engine、Host 和 Context。这 3 个组件分别代表了不同的服务范围，通过嵌套关系可以知道 3 个组件的范围有如下的关 系:<br>Engine>Host>Context。<br>
Engine 组件下可以包含多个 Host 组件，它为特定的 Service 组件处理所有客户请求。
一个 Host 组件代表一个虚拟主机，一个虚拟主机中可以包含多个 Web 应用(Context 组件)。
Context 组件代表一个 Web 应用。<br>

WEB服务器种类：<br>
Java Web 服务器软件按照规模从小到大依次有:JSWDK、JServ、Resin、Tomcat、JRun、JBoss、WebLogic、WebSphere 等，其中 JSWDK、JServ、Resin、Tomcat、JRun、JBoss 是完全免费的软件。
