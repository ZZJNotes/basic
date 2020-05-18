[toc]

## 1. 服务器

### 1.1 什么是服务器？服务器应该具有哪些功能？

服务器具有三种基本功能：

- 监听端口
- 分析请求
- 返回响应

不管什么Web资源，想要被远程计算机访问，都必须有一个与之对应的网络通信程序，当用户来访问时，这个网络通信程序读取Web资源数据，并把数据发送给来访者。

Web服务器就是这样一个程序，他用于完成底层网络通讯。使用这些服务器，用户只需要关注Web资源怎么编写，而不需要关心资源如何发送到客户端手中，从而极大地减轻了开发者的开发工作量。

### 1.2 常见的服务器类型

- JavaEE 服务器：Jboss、WebSphere、weblogic
  - 实现了JavaEE的13种规范
- Web服务器：Tomcat
  - 实现了servlet、jsp

### 1.3 Tomcat

> Tomcat是在SUN公司推出的小型Servlet/JSP调试工具的基础上发展起来的一个优秀的Servlet容器，Tomcat本身完全用Java语言编写。
>
> Tomcat之所以大受欢迎原因主要有以下五点：
>
> 1、Tomcat是Apache的核心项目之一，也被 [SUN](http://www.baike.com/sowiki/SUN?prd=content_doc_search) 视作 Servlet/JSP 容器的一个重要参考实现而加以支持。因此 SUN 最新的Servlet/JSP规范，往往能够很快地在Tomcat的新版本中得到体现；
>
> 2、Tomcat是一个小巧精致的web应用服务器，配置、安装、运行、部署web应用都很简单，这让用户能够很快地上手使用；
>
> 3、[开源软件](http://www.baike.com/sowiki/开源软件?prd=content_doc_search)的生命力，往往与其社区的状况有紧密的联系。在一个[健康](http://www.baike.com/sowiki/健康?prd=content_doc_search)、活跃的社区，用户的疑问通常能够及时地解决，用户的反馈往往能够得到有效地处理，这样会吸引更多的用户加入到社区中来；反过来，不断扩大的用户群，也会促进社区的发展。Tomcat所拥有的优秀社区，对开发者而言，无论用什么标准来评价，都是充满吸引力的；
>
> 4、编写良好的文档，是开发者在开发中最好的帮手之一。Apache在开源社区中，无疑是撰写文档方面的佼佼者；
>
> 5、因为开源和免费的特性，使得用户可以自由无障碍地下载、安装、使用Tomcat。这也是 Tomcat 能够被广泛使用的重要原因之一。



#### 1.3.1 安装和启动

**两种安装方法**

- 解压安装（推荐）
- exe安装

**用法**

- 双击 bin 目录下的 startup.bat 文件

  - 如果出现一闪而过的现象，说明没有配置**JAVA_HOME**环境变量
  - 只要在setclasspath.bat批处理文件第一次使用JAVA_HOME环境变量之前的任何地方，将JAVA_HOME环境变量设置为JDK的主目录，就可以使用startup.bat文件启动Tomcat了

- 输入 http://localhost:8080/，显示如下界面代表安装成功

  ![image-20200514233021211](C:%5CUsers%5Cheihei%5CDesktop%5CTypora%5C%E5%AD%A6%E4%B9%A0%5C%E7%8E%8B%E9%81%93%5C%E5%89%8D%E7%AB%AF%5Cimage-20200514233021211.png)

  - 如果出现端口占用问题，更改默认端口

- shutdown.bat关闭服务器

  #### 1.3.2 目录结构

![image-20200514233031449](C:%5CUsers%5Cheihei%5CDesktop%5CTypora%5C%E5%AD%A6%E4%B9%A0%5C%E7%8E%8B%E9%81%93%5C%E5%89%8D%E7%AB%AF%5Cimage-20200514233031449.png)

- Bin: binary 二进制文件 (启动关闭tomcat命令都在里面)
- Conf: 配置文件
- Lib: tomcat依赖的第三方jar
- Logs: 日志
- Temp:  临时文件
- Webapps: 主要存放应用的地方(web应用)
- Work: 工作空间

#### 1.3.3 项目部署

将项目放到webapps目录下，代表你在这个Tomcat新加了一个应用，然后就可以在浏览器中通过`http://ip:端口/目录名`访问

- root是默认加载路径
- ![image-20200514233340679](C:%5CUsers%5Cheihei%5CDesktop%5CTypora%5C%E5%AD%A6%E4%B9%A0%5C%E7%8E%8B%E9%81%93%5C%E5%89%8D%E7%AB%AF%5Cimage-20200514233340679.png)

##### 1.3.4 Vue项目部署

- **打包**

![image-20200514233410441](C:%5CUsers%5Cheihei%5CDesktop%5CTypora%5C%E5%AD%A6%E4%B9%A0%5C%E7%8E%8B%E9%81%93%5C%E5%89%8D%E7%AB%AF%5Cimage-20200514233410441.png)

![image-20200514233424455](C:%5CUsers%5Cheihei%5CDesktop%5CTypora%5C%E5%AD%A6%E4%B9%A0%5C%E7%8E%8B%E9%81%93%5C%E5%89%8D%E7%AB%AF%5Cimage-20200514233424455.png)



然后会在Vue的项目下生成一个dist文件夹，将里面的内容拷贝到Tomcat的webapps目录下就可以了

##### 1.3.5 Java项目部署

- 把项目打包成war包
- 把war包放到Tomcat的webapps目录下
- 重启Tomcat，war包会自动解压

然后就可以运行了，解压之后的项目对应的目录

![image-20200514233742893](C:%5CUsers%5Cheihei%5CDesktop%5CTypora%5C%E5%AD%A6%E4%B9%A0%5C%E7%8E%8B%E9%81%93%5C%E5%89%8D%E7%AB%AF%5Cimage-20200514233742893.png)

## 2. Tomcat

### 2.1 Tomcat的组成结构

![image-20200514233825018](C:%5CUsers%5Cheihei%5CDesktop%5CTypora%5C%E5%AD%A6%E4%B9%A0%5C%E7%8E%8B%E9%81%93%5C%E5%89%8D%E7%AB%AF%5Cimage-20200514233825018.png)

- Server: 代表整个tomcat代表着整个servlet容器,是最顶级的元素可以包含多个service
- Service:  代表一个服务 可以监听多个端口, 监听到的请求, 都交给engine处理了
- Engine: 引擎,  可以包含多个虚拟主机 host 
- Connector: 监听端口的  
- Host   代表虚拟主机, 包含多个web应用
- Context: 代表单个的应用 

其中，conf目录下的server.xml是重要的核心，我们要实现的就是context : 具体的应用

![image-20200514233855952](C:%5CUsers%5Cheihei%5CDesktop%5CTypora%5C%E5%AD%A6%E4%B9%A0%5C%E7%8E%8B%E9%81%93%5C%E5%89%8D%E7%AB%AF%5Cimage-20200514233855952.png)



Tomcat**的体系架构**

![image-20200514234716263](C:%5CUsers%5Cheihei%5CDesktop%5CTypora%5C%E5%AD%A6%E4%B9%A0%5C%E7%8E%8B%E9%81%93%5C%E5%89%8D%E7%AB%AF%5Cimage-20200514234716263.png)

![image-20200514234723433](C:%5CUsers%5Cheihei%5CDesktop%5CTypora%5C%E5%AD%A6%E4%B9%A0%5C%E7%8E%8B%E9%81%93%5C%E5%89%8D%E7%AB%AF%5Cimage-20200514234723433.png)



>Tomcat处理HTTP请求的过程localhost/test/index.jsp：
>
>1.用户发送一个请求，被发送到当前机器的80端口号，被正在监听80端口号的coyote HTTP／1.1获得
>
>2.Connector组件将收到的请求传递给Engine组件
>
>3.Engine获得了请求地址为localhost/test/index.jsp，匹配虚拟主机
>
>4.匹配到名为localhost的host，如果没匹配到，也将请求交给它处理，它被定义为Engine的默认虚拟主机，该host获得/test/index.jsp，匹配它所拥有的全部Context
>
>5.匹配/test应用名对应的Context节点，Context节点获得index.jsp，它再去寻找响应的servlet
>
>6.Servlet处理完逻辑
>
>7.Context节点把执行完的结果返回给Host
>
>8.Host将结果返回给Engine
>
>9.Engine将结果返回给Connector组件
>
>10.Connector将最终的响应结果返回给客户端

### 2.2 虚拟映射

- 方式一：修改server.xml里的Context

  配置 conf 下的 server.xml  配置host下的context

  <Context path="/bb" docBase="C:\Users\WLoongLee\Desktop\img" />

  Path 标识应用名   docbase标识路径

  ![image-20200514234038343](C:%5CUsers%5Cheihei%5CDesktop%5CTypora%5C%E5%AD%A6%E4%B9%A0%5C%E7%8E%8B%E9%81%93%5C%E5%89%8D%E7%AB%AF%5Cimage-20200514234038343.png)

- 方式二：在conf下的catalina下的localhost配置一个xml文件

  该xml文件的名字，就是对应的应用名

  ![image-20200514234206795](C:%5CUsers%5Cheihei%5CDesktop%5CTypora%5C%E5%AD%A6%E4%B9%A0%5C%E7%8E%8B%E9%81%93%5C%E5%89%8D%E7%AB%AF%5Cimage-20200514234206795.png)

  ![image-20200514234216729](C:%5CUsers%5Cheihei%5CDesktop%5CTypora%5C%E5%AD%A6%E4%B9%A0%5C%E7%8E%8B%E9%81%93%5C%E5%89%8D%E7%AB%AF%5Cimage-20200514234216729.png)

### 2.3 首页问题

修改conf目录下的web.xml文件里的welcome标签

![image-20200514234305028](C:%5CUsers%5Cheihei%5CDesktop%5CTypora%5C%E5%AD%A6%E4%B9%A0%5C%E7%8E%8B%E9%81%93%5C%E5%89%8D%E7%AB%AF%5Cimage-20200514234305028.png)

![image-20200514234310699](C:%5CUsers%5Cheihei%5CDesktop%5CTypora%5C%E5%AD%A6%E4%B9%A0%5C%E7%8E%8B%E9%81%93%5C%E5%89%8D%E7%AB%AF%5Cimage-20200514234310699.png)

### 2.4 服务器的默认端口80

服务器对外的默认端口就是80端口

如果将server.xml中的默认端口设置为80，则在浏览器只输入'localhost'，就可以访问到root里的内容

![image-20200514234434681](C:%5CUsers%5Cheihei%5CDesktop%5CTypora%5C%E5%AD%A6%E4%B9%A0%5C%E7%8E%8B%E9%81%93%5C%E5%89%8D%E7%AB%AF%5Cimage-20200514234434681.png)



## 3. b/s 和 c/s

- c/s 客户端/服务器

  ![image-20200514234945890](C:%5CUsers%5Cheihei%5CDesktop%5CTypora%5C%E5%AD%A6%E4%B9%A0%5C%E7%8E%8B%E9%81%93%5C%E5%89%8D%E7%AB%AF%5Cimage-20200514234945890.png)

- b/s 浏览器/服务器

![image-20200514234950554](C:%5CUsers%5Cheihei%5CDesktop%5CTypora%5C%E5%AD%A6%E4%B9%A0%5C%E7%8E%8B%E9%81%93%5C%E5%89%8D%E7%AB%AF%5Cimage-20200514234950554.png)