# Spring Framework 翻译试水
##翻译内容基于Spring Framework 4.3.5.RELEASE

##第一部分 Spring Framework 概览
  Spring Framework是一个轻量级的，一站式的用于创建企业级应用的解决方案。并且Spring是模块化的，你可以只使用你需要的模块，并非必须全部引用。你可以把任何web framework放在IOC容器之上，也可以只使用hibernate集成或JDBC抽象层这样的代码。Spring Framework支持声明式的事务管理，通过RMI(即Remote Method Invoke 远程方法调用)或web service来访问你的业务逻辑，并提供了几种方式用于保存数据。Spring Framework提供了一个全功能的MVC框架，这样就可以将AOP显示的集成在你的代码中。

  Spring是非侵入式，这就意味着在你的业务代码中通常并不依赖于framework本身。在你的封装层（比如数据访问层），在数据访问技术上一些dependencies和Spring libraries 还是存在的，但这些dependencies可以很容易的与你的基础代码分离。

###   1. Spring 起步
  本文提供了Spring Framework 所有特性的说明文档，也包含了一些诸如“依赖注入”之类的习惯性说法。

  如果你是刚开始使用Spring，你也许可以通过创建一个Spring Boot的基础应用来使用Spring。Spring Boot提供了一个快捷简便的方式来创建可以用于生产环境的Spring 基本应用。它基于Spring Framework，遵循习惯优于配置，并设计成让你能更快的运行起来。

  你可以通过spring.io指导来集成一个基本的工程或采用像“构建RESTful Web Service起步”的方式。这样的方式更加容易理解，同时这些指导内容都非常注重功能本身，他们大部分都是以Spring Boot为基础构建的。这些指导内容同样包含了一些其他的Spring项目，这样当你要解决一个特殊问题的时候就可以考虑这些项目。
### 2. Spring Framework介绍

  Spring Framework 是一个java框架，用来为开发java应用提供多方面的底层支持。Spring负责处理底层问题，让你可以专注于业务本身的逻辑。

  Spring允许通过POJO（简单的java对象）来构建应用，并对其应用非侵入式的企业服务。该功能用于标准的java程序模型，以及整体或部分的JavaEE。

  作为一个应用程序的开发者，你可以通过Spring框架得到如下便利：

 - 掉用Java方法用于数据库事务时，不需要非得通过事务API来解决；
 - 使一个本地的Java方法变为一个远程的程序，而无需处理远程API;
 - 使一个本地的Java方法变为一个管理操作，而无需处理JMX API;
 - 是一个本地的Java方法变为一个消息处理器，而无需处理JMS APS;

#### 2.1. 依赖注入和控制反转
一个java应用：不太标准的说法是一个运行范围从嵌入式程序到N层的大型服务器端企业级的应用程序，通常由很多对象协调来构成一个完整的应用程序。应用程序中的这些对象彼此依赖。

尽管Java平台提供了非常丰富的应用开发功能，但对一个整体而言，缺乏基础构建模块的整合，把这些工作留给了架构师和开发者。尽管你可以使用一些设计模式，比如工厂模式、抽象工厂、生成器模式、装饰模式以及服务定位模式等将不多的类和对象实例来组合成一个应用程序。这些模式都很简单：最佳的命名方式，模式用途的描述、在哪使用、问题的标记等等。模式以最佳的方式被形式化，这就意味着你必须的在你的应用中自己实现这些模式。

Spring Framework的IOC组件针对这一问题，通过在完整的工作应用中使用不同的组件构成的方法来解决该问题。同时将形式化的设计模式编码成可以整合到你自己的应用中的高级对象。许多组织机构使用Spring Framework的这种方法来构建稳定，可维护的应用程序。
  

背景

  2004年Martin Fowler在他的个人网站上提出了一个关于IOC的问题--“到底是哪方面被反转了”。他建议重新命名这个概念的名称（IOC），使其更加一目了然，随后Fowler给他起了一个名字“Dependency Injection”（DI,依赖注入）。

#### 2.2. 模块化

Spring Framework 由很多特性组成，并放到了20个模块中。这些模块被组合进核心容器、数据访问/集成、Web、AOP(面向切面编程)、设备、消息以及测试，如下图所示。

##### 图 2.1 Spring Framework概览

  ![Spring Framework概览](http://docs.spring.io/spring/docs/current/spring-framework-reference/htmlsingle/images/xspring-overview.png.pagespeed.ic.r3l2HohxPQ.webp)

  下面列出了各个特性可供使用的模块以及各模块的artifact名称。Artifact名称在依赖管理工具中与artifact id相关联。

##### 2.2.1 核心容器

  核心容器包括几个模块：spring-core,spring-beans,spring-context,spring-context-support以及spring-expression(Spring表达式语言)。

  spring-core和spring-beans模块提供了框架中一些基础的部分，包括IOC和DI功能。BeanFactory是工厂模式的一个更高级的实现。它去除了程序对单例模式的需要，并且允许你解耦配置，然后根据你实际的编码逻辑设置依赖关系。

  Context(spring-context)模块以Core和Beans模块为基础构建：他是一个类似于JNDI注册表式的框架风格的访问对象的方式。Context模块继承了Beans模块的功能，并增加了对国际化的（比如 resource bundles的使用）,事件传播，资源加载，以及Context的透明创造，例如一个Servlet容器。Context模块同样支持像EJB,JMX或基本的远程处理的支持。ApplicationContext接口是Context模块的核心。spring-context-support为Spring应用上下文整合了通用的三方库，比如缓存（EhCache,Guava,JCache）,邮件（JavaMail）,定时任务（CommonJ,Quartz），以及末班引擎（FreeMarker,JasperReports,Velocity）。

  spring-expression模块为runtime时的查询和操作对象图提供了一个强大的EL语言，在JSP 2.1规范中，它作为统一表达式语言规范的一个扩展。该表达式语言支持属性值的setting和gettting，属性分配，方法调用，访问数组，集合，索引器的内容，逻辑和算术运算，变量命名，在IOC中根据名称查找对象。同时也支持列表投影，选择以及通用列表的聚合。

##### 2.2.2. AOP和工具

  spring-aop模块提供了AOP联盟标准的一个面向切面编程的实现，允许你自定义拦截器和切点来干净的解耦应该被分离的代码。使用源码级的元数据功能，同样可以将行为信息放到你的代码中，类似于.NET的属性值。

  独立的spring-aspects模块提供了对AspectJ的整合。

  spring-instrument模块提供了类工具的支持和类加载器的实现，用于某些应用服务中。spring-instrument-tomcat模块包括了Spring对tomcat的代理工具。

##### 2.2.3. 消息

  Spring Framework 4包括了一个spring-messaging模块，这是对Spring集成项目中的像消息，消息通道，消息处理器进行了关键性的抽象。该模块也提供了类似于编程模式spring MVC注解的一系列为方法映射消息的注解。

##### 2.2.4 数据访问/集成

数据访问/集成层包括JDBC、ORM、OXM、JMS以及事物模块。

spring-jdbc模块提供了一个jdbc的抽象层，移除了乏味的JDBC代码，以及对数据库厂商特殊错误代码的转换。

spring-tx模块为实现特殊接口的类提供了编程示和声明式的事物管理，并且可以用于所有的POJO。

spring-orm模块为流行的对象-关系映射API（包括JPA,JDO,hibernate）提供了整合层。使用spring-orm模块你可以将所有这些O/R映射的框架与Spring提供的其他特性整合到一块，比如前面提到的事物管理功能。

spring-oxm模块提供了一个O/X映射的实现，比如JAXB，Castor,XMLBeans,JiBX,XStream的抽象层。

spring-jms模块（java消息服务）包括生产和处理消息的功能。从Spring Framework 4.1开始，使用spring-messaging模块提供了集成。

##### 2.2.5 Web

Web层包括了spring-web,spring-webmvc,spring-websocket以及spring-webmvc-portlet几个模块。

spring-web模块提供了基础的面向web的集成功能，例如文件上传功能，以及通过servlet监听器和一个面向web的应用上下文初始化IOC容器。也包括了一个HTTP客户端和Spring提供的远程支持部分中网络相关的内容。

spring-webmvc模块（也叫web-servlet模块）模块，包括为web应用实现的Spring的模型-视图-控制器（MVC）和REST Web Service。

Spring MVC在domain代码，web表单之间提供了一个干净的隔离，并且和所有Spring Framework的其他功能进行了集成。

spring-webmvc-portlet模块（也叫Web门户组件模块）提供了MVC的实现，用于门户组件环境中，体现了spring-mvc模块的功能。

##### 2.2.6 测试

spring-test模块通过JUnit或TestNG提供了unit测试和集成测试。提供了Spring ApplicationContext和这些context的缓存的一致的加载方式。也提供了模拟对象，这样你就可以在隔离的情况下测试你的代码了。

#### 2.3 使用场景

前面说的构建模块通过使用Spring的事物管理功能和web框架整合让Spring在很多场景中都有一个适合的选择，不论是运行在资源受限的设备的嵌入式应用还是成熟的企业级的应用。

##### 图2.2 典型的成熟Spring Web Application

![Spring Web Application](http://docs.spring.io/spring/docs/current/spring-framework-reference/htmlsingle/images/overview-full.png.pagespeed.ce.sC26wirtWB.png)

Spring声明式事物管理功能让web应用布满事物，就像你使用EJB的容器管理事物的样子。你所有自定义的业务逻辑代码都可以通过简单的POJO来实现，并通过Spring的IOC事物管理来管理。其他的服务包括对发邮件的支持，校验（依赖于web层，这样可以让来选择在哪执行校验规则），和JPA、hibernate、JDO集成了的Spring ORM；比如，当用到hibernate，你可以继续使用你已经在的映射文件和标准的hibernate SessionFactory配置。表单控制器通过业务模型与web层无缝集成，并移除了对ActionForm或其他的类（用于将HTTP的参数转换为你的业务模型）的需要。

#####  图 2.3 使用一个第三方web framework的Spring中间层

![Figure 2.3](http://docs.spring.io/spring/docs/current/spring-framework-reference/htmlsingle/images/overview-thirdparty-web.png.pagespeed.ce.1lJso2G8WP.png)

有时候并不允许你完全的去选择一个不同的框架。Spring Framework不会强迫你使用它的所有功能，她不是一个“除非全用否则全不用”的方案。目前像Struts,Tapestry,JSF或其他前端UI框架都可以通过一个Spring的基础中间层来集成，这样你就可以使用Spring的事物功能了。你需要使用一个ApplicationContexthe和一个WebApplicatinContext来简单的把你的业务逻辑集成到你的web层。

##### 图 2.4. 远程处理使用环境

![Figure 2.4](http://docs.spring.io/spring/docs/current/spring-framework-reference/htmlsingle/images/overview-remoting.png.pagespeed.ce.HIMsJb_Xya.png)

当你需要通过web service来访问已经存在代码，你可以使用Spring的Hessian-,Burlap-,Rmi-或JaxRpcProxyFactory的类。可以无区别的访问存在的应用。

##### 图 2.5. EJB 包装已有的POJO

![Figure 2.5](http://docs.spring.io/spring/docs/current/spring-framework-reference/htmlsingle/images/overview-ejb.png.pagespeed.ce.VN88UiKUhA.png)

Spring Framework 同样为企业级JavaBean提供了一个访问和抽象层，可以使你能复用你已有的POJO，并把他们包装在无状态的session bean中以用在可扩展性，以及需要声明安全的不安全的web应用中。

##### 2.3.1 依赖管理和命名规范

依赖管理和依赖注入是两个不同的东西。为了将Spring那些nice的功能用在你的应用中（比如依赖注入），你需要将所有需要的类库（jar包）集中，并将他们放在你的运行时（也可能在编译时）的classpath中，这些依赖并不是被注入的虚拟组件，而是在文件系统中（通常来说）的真实的资源。以来管理的过程涉及加载那些资源，并存储，然后加到classpath
中。可以是直接依赖（比如我的应用在运行时直接依赖于Spring）或者间接依赖（比如我的应用直接依赖于commons-dbcp，而commons-dbcp直接依赖于commons-pool）。间接依赖也叫“依赖传递”，他是那些特别不容易定义和管理的依赖。

如果你将使用Spring，你需要复制一份你需要用到的Spring的部分的jar包。为了让这件事更容易，Spring被打包成很一系列的模块，尽可能的隔离依赖关系，比如如果你不想写一个web应用，你就不需要spring-web相关的模块。本文中的Spring模块，我们使用一个简短的命名方式spring-* 或spring-\*.jar, \*代表模块的简称（比如spring-core,spring-webmvc,spring-jms等等）实际上你用的jar文件命名一般是模块名加版本号（比如spring-core-4.3.5.RELEASE.jar）。

Spring Framework 每个发行版都会将artifact放到下面地方：

- Maven中央仓库，Maven查找的默认的仓库，并且使用时不要求任何特殊的配置。许多Spring依赖的一般库也可以从Maven中央库中获得，很多Spring社区都是用maven作为依赖管理，对他们来说这很方便。这里的jar包的命名使用spring-\*-< version >.jar的形式，maven的groupid是org.springframework。

- 把Spring托管在一个具体的公共Maven库中。除了最终的GA版（General Availability，最终版），该库中也有开发版的快照和里程碑。jar包的命名与Maven中央库的命名形式相同，因此这是一个很有用的地方，来获取Spring的开发版本，并与部署在Maven中央库的其他类库一块使用。该仓库也包括了一些分发的Zip文件，包括了Spring所有的jar包，以方便下载。

因此，你首先要想的是怎么管理依赖：我们一般推荐使用自动化系统，比如Maven，Gradle或者lvy，当然你也可以手动下载所有的jar包。

下面是Spring artifact的列表，想了解各个模块的具体信息，可以看第2.2章 “模块”。

##### 2.1 Spring Framework Artifacts

| GroupId            | ArtifactId    | Description           |
|:------------------:|:--------------|:----------------------|
|org.springframework | spring-aop    | 基于代理的AOP支持|
|org.springframework | spring-aspects    | 基于AspectJ的aspect|
|org.springframework | spring-beans    | Bean支持，包括Groovy|
|org.springframework | spring-context    | 应用上下文运行时，包括调度和远程的抽象|
|org.springframework | spring-context-support    | 用于支持将第三方库整合进Spring应用上下文的支持类|
|org.springframework | spring-core    | 核心工具，许多其他Spring模块都有用到|
|org.springframework | spring-expression    | Spring表达式语言|
|org.springframework | spring-instrument    | 为JVM引导启动用的代理工具|
|org.springframework | spring-instrument-tomcat    | tomcat的代理工具|
|org.springframework | spring-jdbc    | jdbc支持包，包括数据库加载和jdbc访问支持|
|org.springframework | spring-jms    | JMS支持包，包括收发JMS消息的帮助类|
|org.springframework | spring-messaging    | 提供消息架构和协议的支持|
|org.springframework | spring-orm    | 对象关系映射，包括JPA和hibernate的支持|
|org.springframework | spring-oxm    | 对象XML映射|
|org.springframework | spring-test    | 为单元测试提供支持，并整合Spring组件测试|
|org.springframework | spring-tx    | 事务基础组件，包括DAO支持和JCA集成|
|org.springframework | spring-web    | web支持包包括客户端和web远程|
|org.springframework | spring-webmvc    | 为web应用提供的REST Web Service和模型-视图-控制器的实现|
|org.springframework | spring-webmvc-portlet    | 用于Porlet环境的MVC实现|
|org.springframework | spring-websocket    | WebSocket和SockJS实现，包括STOMP的支持|

##### Spring依赖和在Spring中依赖

尽管Spring提供了集成，也对大量企业级和其他扩展工具提供了支持，但他有意的保持了对一个最小限度的抽象的强制性依赖：你不必去查找并下载（甚至是自动下载）大量的jar包类库，到最后只是为了一个很简单的原因使用Spring。对于基础的依赖注入，只有一个强制性的外部依赖，而且他还是为了记录日志（看下面，可以获取更多的有关日志的描述）。

下一步，我们脱离基础的步骤，需要在Spring上配置应用的依赖。首先使用Maven，然后使用Gradle，最后使用lvy。如果有什么不清楚的，可以看看你使用的依赖工具的文档，或者看看一些简单的代码-Spring本身使用Gradle作为依赖管理工具来构建，并且我们的示例代码大都使用Gradle或者Maven。

##### Maven依赖管理

如果你使用Maven作为依赖工具，你甚至不需要直接的获取日志依赖。比如创建一个应用上下文，并且使用依赖注入来配置一个应用，你的Maven依赖将会是这样：

    <dependencies>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>4.3.5.RELEASE</version>
            <scope>runtime</scope>
       </dependency>
    </dependencies>

这样就可以了。需要说明的是“scope”，如果不需要使用Spring的API来编译代码，可以声明成runtime，在基础的依赖注入使用案例中，这算是一个典型的例子了。

上面是使用Maven中央库的例子。要是使用Spring Maven库的话（比如里程碑或者开发者快照），你需要在你的Maven配置中配置仓库的位置。获取全部发行版：

    <repositories>
        <repository>
            <id>io.spring.repo.maven.release</id>
            <url>http://repo.spring.io/release/</url>
            <snapshots><enabled>false</enabled></snapshots>
        </repository>
    </repositories>

获取里程碑：

    <repositories>
      <repository>
        <id>io.spring.repo.maven.milestone</id>
          <url>http://repo.spring.io/milestone/</url>
        <snapshots><enabled>false</enabled></snapshots>
      </repository>
    </repositories>

获取快照：

    <repositories>
      <repository>
          <id>io.spring.repo.maven.snapshot</id>
          <url>http://repo.spring.io/snapshot/</url>
          <snapshots><enabled>true</enabled></snapshots>
      </repository>
    </repositories>

##### Maven“材料清单”依赖

使用Maven的时候，可能会意外的将各版本Spring的jar包混合使用。比如，你可能从一个第三方库或另一个Spring项目中找到jar包，，然后在一个老版本中把他拉进一个传递依赖中。如果你忘了明确的声明一个直接依赖，那么各种各样的问题将会接憧而至。

为了解决这类问题，Maven支持一个“材料清单”（BOM）依赖的概念
。你可以在你的依赖管理中引入springframework-bom来确保所有的spring依赖（不论直接还是间接依赖）都是相同的版本。

    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>org.springframework</groupId>
                <artifactId>spring-framework-bom</artifactId>
                <version>4.3.5.RELEASE</version>
                <type>pom</type>
                <scope>import</scope>
           </dependency>
        </dependencies>
    </dependencyManagement>

使用BOM的另一个好处是你不再需要在依赖中为Spring Framework配置 < version >属性了。

##### Gradle依赖管理

通过Gradle构建工具来使用Spring仓库，在仓库部分加入适当的URL：

    repositories {
        mavenCentral()
        // and optionally...
        maven { url "http://repo.spring.io/release" }
    }

你也可以更换仓库URL，把“/release”换成“/milestone”或者“/snapshot”都可以。一旦仓库配置完，你就可以按照通常的Gradle方法来声明依赖。

    dependencies {
        compile("org.springframework:spring-context:4.3.5.RELEASE")
        testCompile("org.springframework:spring-test:4.3.5.RELEASE")
    }

lvy依赖管理

如果你准备用lvy来管理依赖，配置项差不多。

配置lvy指向Spring的仓库，需要在ivysettings.xml里加上下面的解析器：

    <resolvers>
        <ibiblio name="io.spring.repo.maven.release"
                  m2compatible="true"
                  root="http://repo.spring.io/release/"/>
    </resolvers>

你可以将“root”里“/release”url更换为“/milestone”或“/snapshot”

配置完后，你就可以按照通常的方式添加依赖了。比如（在ivy.xml里）：

      <dependency org="org.springframework"
            name="spring-core"
            rev="4.3.5.RELEASE"
            conf="compile->runtime"/>

##### Zip文件分发

尽管使用依赖管理构建工具来获取Spring Framework是一种推荐的做法，但是仍然可以直接下载一个分发的压缩文件。

分发压缩包已经发行到Spring的Maven仓库（这只是为了我们自己方便，你不需要为了下载这些文件使用Maven获取其他的构建工具）。

下载压缩包的话，打开浏览器访问 http://repo.spring.io/release/org/springframework/spring ，然后根据你的需要选择适合的版本子目录。分发包以“-dist.zip”结尾，比如spring-framework-{spring-version}-RELEASE-dist.zip。在里程碑和快照中也发布了分发包。

##### 2.3.2 日志

日志是Spring中一个非常重要的依赖，因为：
  a) 这是唯一一个强制性的外部依赖；
  b) 每个人都想看看他们正在用的工具输出了哪些东西；
  c) Spring集成了许多其他的工具，这些工具也会用到日志依赖。

应用开发人员的一个期望往往是在整个应用中有一个统一的日志配置，包括所有外部的组件。由于有很多日志框架可供选择，所以这变得更难了。

在Spring中使用Jakarta Commons Logging(JCL)作为强制性的日志依赖。我们编译JCL并使JCL的Log对象对类可见，这样就扩展了Spring Framework。所有的Spring使用相同的日志库（便于迁移），即使应用扩展了Spring，但向后兼容一直保留着，这对用户来说是很重要的。我们的解决方法是使其中一个模块对common-loggging（JCL规范的实现）有明确的依赖，然后让所有其他的模块在编译时依赖。比如，如果你正在使用Maven，会很疑惑你在哪依赖了common-logging，它是在Spring的中心模块叫spring-core的地方被明确的。

好消息是对于commons-logging，你不再需要其他任何东西，就可以让你的应用正常工作。它有个运行时的发现算法，用来在classpath里众所周知的地方查找其他的日志框架，并使用它认为合适（或者你可以告诉他你需要哪个）的框架。如果没有你觉得不错可以用的日志，就会到JDK里去找（java.util.logging或JUL）。你要找一个可以在大多数情况可以让你的Spring应用正常工作并输出日志的框架，这个很重要。

##### 不使用通用的日志

不幸的是commons-logging的运行时发现算法，方便的是最终用户，这是个问题。如果我们能回到过去，并且把Spring作为一个新的项目，那么就会使用一个不同的日志依赖。首选的应该是Simple Facade For Java（SLF4J），用户也将自己的Spring应用中许多其他的工具使用了这个框架。

下面是两个基本的方法来切换commons-logging：

1. 从spring-core从移除依赖（因为他是唯一一个对commons-logging明确依赖的一个模块）
2. 依赖一个特殊的commons-logging，这个包是一个空的jar（详情的话可以去看看SLF4J）

移除commons-logging，需要在依赖管理中添加以下内容：

    <dependencies>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-core</artifactId>
            <version>4.3.5.RELEASE</version>
            <exclusions>
                <exclusion>
                    <groupId>commons-logging</groupId>
                    <artifactId>commons-logging</artifactId>
                </exclusion>
            </exclusions>
        </dependency>
    </dependencies>

现在应用程序可能由于在classpath中没有JCL的实现而崩溃，因此要修复这个问题，必须提供一个新的日志。下一节中，我们会以SLF4J为例说明如何添加一个可用的JCL实现。

##### 使用SLF4J

SLF4J是一个干净的依赖，并且比commons-logging运行时效率更高，这是因为它使用了编译时绑定来代替他所集成其他日志框架运行时的发现算法。这也意味了在运行时或声明时，又或是配置时你必须更清晰的表达你所希望的结果。SLF4J提供了对很多常见日志框架的绑定，这样通常情况下，你就可以选择你已经在用的日志框架，然后绑定配置和管理。

SLF4J提供了很多常用日志框架的绑定，包括JCL，它同时也做了与之相反的事：在他自己和其他日志框架之间建立桥梁。因此，在Spring中使用SLF4J你需要使用SLF4J的JCL桥替换commons-logging依赖。这样做完之后，Spring内的日志响应就会被转移到SLF4J的之日响应中。因此如果你的应用中有其他的类库使用的这个API，那么你只需要在一个地方配置和管理日志就可以了。

通常的做法应该是将Spring桥接到SLF4J，并显示的将SLF4J绑定到Log4J。你需要有4个依赖（不算已经存在commons-logging）:桥接包，SLF4J包，桥接Log4J包，以及Log4J自己的实现。在Maven里你可以这么干：
```
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-core</artifactId>
        <version>4.3.5.RELEASE</version>
        <exclusions>
            <exclusion>
                <groupId>commons-logging</groupId>
                <artifactId>commons-logging</artifactId>
            </exclusion>
        </exclusions>
    </dependency>
    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>jcl-over-slf4j</artifactId>
        <version>1.5.8</version>
    </dependency>
    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-api</artifactId>
        <version>1.5.8</version>
    </dependency>
    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-log4j12</artifactId>
        <version>1.5.8</version>
    </dependency>
    <dependency>
        <groupId>log4j</groupId>
        <artifactId>log4j</artifactId>
        <version>1.2.14</version>
    </dependency>
</dependencies>
```

可能看起来只是为了获取一些日志，却引了这么多依赖。确实如此，但这是可以选择的。而且他比普通的commons-loggging在解决类加载问题上表现更好，尤其是你在一个很严格的容器中，比如OSGi平台。可能这里也有一个性能上的提升，因为绑定操作是在编译时进行的而非运行时。

在SLF4J用户中一个更常见的做法是在更少的步骤下和更少的依赖集中来明确的绑定以获取Logback。这个方法移除了已经存在的绑定步骤，这是因为Logback显示的实现了SLF4J。因此，你只需要依赖两个类库而不是四个了（jcl-over-slf4j和logback）。如果你这么做，那么你也要把slf4j-api依赖从其他外部的依赖（不包括Spring）移除，因为你只是向在classpath中看到一个版本的日志API。

##### 使用Log4J

很多人使用Log4J作为日志框架来达到配置和管理的目的。这是很高效也很好建立的方式，而且实际上这也是我们在运行时构建和测试Spring所使用的方法。Spring也对Log4J提供了一些统一的配置和初始化，因此在一些模块中有有一个编译时依赖的选项。

使用默认的JCL依赖（commons-logging）让Log4J工作，你需要做的只是把Log4j放到classpath中，并在classpath的根路径添加一个配置文件（log4j.properties或者log4j.xml）。下面是Maven用户需要的依赖声明。

```
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-core</artifactId>
        <version>4.3.5.RELEASE</version>
    </dependency>
    <dependency>
        <groupId>log4j</groupId>
        <artifactId>log4j</artifactId>
        <version>1.2.14</version>
    </dependency>
</dependencies>
```

下面是一个简单的log4j.properties例子，用来把日志输出到控制台：
```
log4j.rootCategory=INFO, stdout

log4j.appender.stdout=org.apache.log4j.ConsoleAppender
log4j.appender.stdout.layout=org.apache.log4j.PatternLayout
log4j.appender.stdout.layout.ConversionPattern=%d{ABSOLUTE} %5p %t %c{2}:%L - %m%n

log4j.category.org.springframework.beans.factory=DEBUG
```

##### 运行时容器和原生JCL

很多人在一个容器中运行他们的Spring应用，而且这个应用本身也提供对JCL的实现。IBM Websphere Application Server(WAS)就是这个原型。这经常会引发一些问题，但糟糕的是并没有一个一劳永逸的解决方案；在大多数方案中，简单的从你的应用中移除commons-logging并不够。

这样说的话，应该会清晰点：报告的问题本质上通常与JCL不相关，甚至commons-logging：相反，他们通常把commons-logging绑定到其他框架（经常是Log4j）。这样做的话是会失败的，这是因为commons-logging修改了运行时的发现算法，包括在一些容器中运行的旧版本（1.0）以及现在人们使用的最新版（1.1）。Spring不使用非常用的JCL API，这样就不会出现问题,但只要Spring或你的应用尝试使用任何你找到的绑定到Log4J的日志框架，就会停止工作。

这时候使用WAS，最容易做的是转换类加载的优先级（IBM叫它“parent last”），以便应用程序控制JCL依赖而非控制容器。这个方法并非总是可用的，但在公共领域有很多其他的方法作为替代方案。你的里程可能会因容器的特定版本和特性而异。

## 第二部分 Spring Framework 4.x的新内容

### Spring Framework 4.0的新功能和增强

Spring Framework 在2004年发布了第一个版本；自从那之后，比较重要的主要版本有：Spring2.0，增加了XML命名空间和对AspectJ的支持；Spring2.5，加入了注解驱动的配置；Spring3.0通过一个强大的JAVA 5.0功能访问框架的基础代码以及特性，比如基于java的@Configuration模块。

4.0版本是Spring Framework最新的一个主要版本，并且第一个完全支持Java8.0特性。你当然可以继续在Spring中使用老版本的java，然而， 现在最低的要求已经提升到Java SE 6了。我们也在一个主要版本的适当时候移除了许多过时的类和方法。

在Spring Framework GitHb Wiki上可以获取一个升级到Spring4.0的迁移指导。

#### 3.1 改善上手体验

新的spring.io网站提供了全部系列的上手指导来帮你学习Spring。你可以在本文档第一章Spring起步里看到更多的指导。对于其他在Spring下发布的项目，新网站也给出了综合性的概览。

如果你是个Maven用户，那你可能对“材料清单”POM文件会感兴趣，他很有用处，并且在Spring Framework各个发行版上发布。

#### 3.2移除过时的包和方法

所有过时的包，很多过时的类和方法在4.0版本已经被移除了。如果你正在从Spring原来的版本升级，你应该确认你已经在过时的API中修复了所有过时的调用。

获取完整的变更，查看API Differences Report。

要注意的是可选择的三方依赖已经升到最小2010/2011（就是说Spring4集成仅支持2010年及之后的发行版本）：尤其是hibernate 3.6+，EhCache 2.1+，Quartz 1.8+， Groovy 1.8+以及Joda-Time 2.0+。规则中有一个例外，Spring 4.0要求当前的Hibernate Validator的版本为4.3+，同时对Jackson的支持现在集中在2.0+版本（对Jackson 1.8/1.9的支持到Spring 3.2都有保留；现在只是设置成了过时形式）。

#### 3.3 Java 8（以及6和7）

Spring 4.0 支持Java 8 的一些特性。你可以在Spring的回调接口里使用lambda表达式和方法引用。这是对java.time(JSR)最优先的支持。一些已有的注解已经改成了@Repeatable。你也可以使用Java 8 的参数名发现作为一个替代方案来在调试信息可用的时候来编译你的代码。

Spring保留对老版本的Java和JDK的兼容：具体包括Java SE 6(需要说的是JDK 6 的最小版本为2010年一月份发布的update18) 及以上都仍在全部支持。但是对于新开始的基于Spring 4 的开发项目，我们建议使用Java 7 或 8。

#### 3.4 Java EE 6和7

Java EE 6及以上正在被考虑和其有特殊关联的JDA 2.0、Servlet 3.0规范作为Spring Framework 4的基础。为了保持对Google App Engine和较老的应用服务的兼容性，允许在Servlet 2.5中部署Spring 4.0 的应用。但还是强烈建议使用Servlet 3.0+，同时也是开发环境中为了测试而安装Spring测试和模拟包的首要条件。

如果你是一个WebSphere7用户，请确认安装了JPA2.0功能包。WebLogic 10.3.4及以上版本需要安装JPA2.0的补丁包。这些服务器的改变都集成到了Spring4的兼容部署环境中。

一个更前瞻性的点是现在Spring Framework 4.0支持适用于JavaEE7的的规范：特别是JMS 2.0，JTA 1.2，JPA 2.1，Bean Validtion 1.1以及JSR-236 Concurrency Utilities。一般来说这些支持致力于这些规范的单独使用，比如在tomcat或一个独立的环境中。但是当Spring应用被部署到Java EE 7的服务器上时，它工作的同样很好。

要注意的是hibernate4.3是JPA 2.1的实现，因此只在Spring 4.0中被支持。一样的是hibernate 5.0是 Bean Validtion 1.1的实现。以上两个都没有在Spring Framework 3.2上正式支持。

#### 3.5 Groovy Bean Definition DSL

从Spring Framework 4.0开始，可以使用Groovy DSL来定义bean配置。概念上有点像使用XML bean定义，但Groovy DSL使用的语法更简洁。使用Groovy可以很轻松的把bean的定义直接嵌入到引导代码中。比如：
```
def reader = new GroovyBeanDefinitionReader(myApplicationContext)
reader.beans {
    dataSource(BasicDataSource) {
        driverClassName = "org.hsqldb.jdbcDriver"
        url = "jdbc:hsqldb:mem:grailsDB"
        username = "sa"
        password = ""
        settings = [mynew:"setting"]
    }
    sessionFactory(SessionFactory) {
        dataSource = dataSource
    }
    myService(MyService) {
        nestedBean = { AnotherBean bean ->
            dataSource = dataSource
        }
    }
}

```

要了解更多信息查看GroovyBeanDefinitionReader的javadoc。

#### 3.6 核心容器的改进

下面是核心容器的一些改进：

- Spring现在在注入Bean时会将通用的类型作为预选（qualifier）形式。比如你正在使用 Spring Data Repository，这时候你可以很容易的注入一个特定的实现:

```
@Autowired Repository<Customer> customerRepository. 
```

- 如果你使用Spring的meta-annotation，那你现在就可以开发自定义的注解， 从原始的注解中暴露特定的属性。

- Bean现在只有在被装配到集合和数组中的时候才能被订阅。同时支持@Order注解和Ordered接口。

- 注解@Lazy现在可以在注入点和@Bean定义上使用了。

- 使用基于Java的配置开发时引入了注解@Description。

- 通过@Conditional注解加入了条件过滤bean的粗糙模型。这很像@Profile，但@Confidition允许以编程的方式来开发用户自定义的策略。

- 基于CGLIB的代理类不再要求默认的构造方法。这是通过objenesis类库提供支持的，该类库已经作为Spring Framework的一部分以内联的方式重新打包并发布。使用该策略，就不再为代理实例调用任何构造方法。

- 现在可以通过框架来管理时区了，比如在LocaleContext上。

#### 3.7 Web改进概况

部署Servlet 2.5服务器保留了一个选择，但在Spring Framework 4.0中，已经以部署Servlet 3.0环境为主。如果你正在使用Spring MVC Test Framework 你需要确认在你的测试classpath中已经有了一个Servlet 3.0的兼容jar包。

除了后面提到的WebSocket支持，其他的改进情况已经加入到了Spring的Web模块中：

- 你可以在Spring MVCY应用中使用新的@RestController注解，已经不需要在你的每个@RequestMapping方法上加上@ResponseBody了。

- 加入了AsyncRestTemplate类，提供了在开发REST客户端时的非阻塞异步支持。

- 在开发Spring MVC应用时，Spring提供了完整的时区支持。

#### 3.8 WebSocket, SockJS,and STOMP Messaging

web应用中基于WebSocket的客户端与服务端的双向交流，在新模块spring-websocket提供了全面的支持。它兼容JSR-356，Java WebSocket API。此外，提供了基于SocketJS的回退选择（即WebSocket模拟），用于尚未支持WebSocket协议的浏览器（比如 IE 10之前的的版本）。

新模块spring-messaging对STOMP提供了支持，在应用中作为WebSocket的子协议与一个用于路由的注解编程模型和处理来自WebSocket客户端的STOMP消息一起使用。因此，现在一个@Controller可以包含@RequestMapping和@MessageMapping两种方法，用于处理在联的WebSocket客户端的HTTP请求和消息。新模块也包含了原来的重要抽象，比如Spring集合项目中的Message,MessageCannel，MessageHandler以及其他作为基础服务用于基于消息的应用。

要进一步了解细节，包括更多的介绍，查看第26章WebSocket支持。

#### 3.9 测试改进

除了在spring-test模块中整理过时的代码，Spring Framework 4.0在单元测试和集成化测试中引入了一些新的特性。

- 几乎所有的注解在spring-test模块中（比如@ContextConfiguration,@WebAppConfiguration,@ContextHierarchy,@ActiveProfiles等等）都能当做meta-annotation使用，来创建自定义的组合注解，并通过一套测试来减少重复配置。

- 现在可以以编程的方式来管理活动bean的定义配置文件，实现一个自定义的ActiveProfilesResolver，并通过@ActiveProfiles的resolver属性来注册就可以了。

- 在spring-core模块中新引入了一个SocketUtils类，它可以让你扫描本机上空闲的TCP和UDP服务端口。该功能不是在具体的测试，但在编写需要用到sockets的集成测试时，可以很有帮助，比如测试启动一个SMTP存储服务器,FTP服务器，Servlet容器等等。

- 在Spring 4.0中，org.springframework.mock.web包内的模拟集合现在已经基于Servlet 3.0了。同时一些Servlet API 的模拟测试（比如MockHttpServletRequest，MockServletContext等等）进行了一些增强性的更新以及改进了可配置性。

### 4. Spring Framework 4.1新特性及增强

#### 4.1 JMS改进

Spring 4.1引入了一个很简单的基础结构，使用@JmsListener注解bean的方法来注册JMS监听器端。增加了XML命名空间来支持这种新的风格（jms:annotation-driven），并且可以使用Java配置（@EnableJms，JmsListenerContainerFactory）配置全部的基础结构。也可以使用JmsListenerConfigurer以编程化的方式注册监听端。

Spring 4.1也整理了自己的JMS支持，让你可以与 4.0引入的spring-messaging抽象相适应，就像下面这样：

- 消息监听端点签名会更加灵活，并且可以从诸如@Payload，@Header，@Headers，@SendTo的标准消息注解中受益。使用标准的消息代替javax.jms.Message作为方法参数会更适合。

- 可以获取一个新接口JmsMessageOperations，并且允许像使用Message抽象操作一样使用JmsTemplate。

最后，Spring 4.1的一些其他的改进：

- 同步请求-回复操作支持JmsTemplate

- 监听优先级可以在每个<jms:listener>标签中说明。

- 消息监听容器的恢复操作通过使用一个BackOff实现来配置。

- JMS 2.0 支持分享消费者。

#### 4.2 缓存改进

Spring 4.1使用Spring已有的缓存配置和基础层抽象可以支持JCache(JSR-107)注解；使用标准的注解没有任何变化。

Spring 4.1 显著的改善了自已的缓存抽象：

- 运行时可以使用CacheResolver来解析缓存。这样就不再需要强制性的定义缓存名称的参数value。

- 更加自定义的操作级别：缓存解析器，缓存管理器，密钥生成

- 新的类级别注解@CacheConfig允许在没有任何可用缓存操作的类级别分享通用配置。

- 使用CacheErrorHandler处理被缓存的方法可以获取更好的体验。

在Spring 4.1的缓存接口中加入了putIfAbsent方法，这是一个突破性的变化。

#### 4.3 Web改进概况

- 将已有的以ResourceHttpRequestHandler为基础的资源处理，通过新的抽象类ResourceResolver，ResourceTransformer和ResourceUrlProvider进行了扩展。许多内置的实现都支持版本化的URL（为了有效的HTTP缓存），gzip压缩资源定位，生成一个HTML5的AppCache体现，等等。查看第22.16.9节，“资源服务”。

- 为@RequestParam，@RequestHeader，@MatrixVariable的控制器方法参数增加了JDK1.8的java.util.Optional的支持。

- 在目前已经返回ListenableFuture了的基础服务（也可能是调用AsyncRestTemplate）中增加了ListenableFuture来代替DeferredResult作为返回值。

- 现在带有@ModelAttribute注解的方法的调用已经遵循内部相互依赖的顺序。查看 SPR-6299。

- 在@ResponseBody和ResponseEntity的控制器方法中支持了Jackson的@JsonView注解，用于为相同的POJO(比如简介和详情页的比较)序列化大量不同的详细信息。同时增加序列化视图类型，作为一个特殊属性下的model属性，用于支持基于视图的渲染。查看 “Jackson序列化视图”的张杰。

- 通过Jackson来支持JSONP。查看“Jackson JSONP支持”章节。

- 新增了一个生命周日，用来在控制器的方法返回值之后和写入相应之前拦截@Responsebody和ResponseEntity注解了的方法。声明一个实现ResponseBodyAdvice的注解了@ControllerAdvice的bean。内置的对@JsonView和JSONP的支持就是使用的该方法。查看第22.4.1章“使用HandlerInterceptor拦截请求”。

- 新增三个HttpMessageConverter选择：

    - Gson：比Jackson更轻量级；已经应用在Spring Android中了。

    - Google Protocol Buffers ：企业级高效的内部服务数据交换协议，也可公开后作为JSON和XML用于浏览器。

    - 基于XML序列化的Jackson可通过jackson-dataformat-xml扩展获取支持。如果classpath中有jackson-dataformat-xml，那么就会默认使用Jackson来代替JAXB2。

- 诸如JSP的视图层现在可以将名字引用到controller的映射中来构建与controller的链接了。每个@RequestMapping都有一个默认的名字。比如FooController中有一个方法handleFoo，那它的名字就是“FC#handleFoo”。命名规则是可以插入的，可以使用它的name属性来显示的命名。在Spring JSP标签库中新增了一个mvcUrl函数，可以让这种方法在JSP页面中更容易使用。查看 22.7.2章，“从视图层构建URI链接到控制器和方法”。

- @ResponseEntity提供了一个构建方式的API来引导控制器的方法指向已经准备好的服务器端相应，比如ResponseEntity.ok()。

- RequestEntity是一个新的类型，提供了构建方式的API，用于引导客户端REST代码指向已经准备好的HTTP请求。

- MVC java 配置和XML命名空间：

    - 视图解析器现在可以进行包括支持内容协商在内的配置了。

    - 视图控制器现在内置了重定向支持以及设置相应状态。应用可以在视图中使用视图控制器配置重定向URL，渲染404，发送“no content”的相应等等。

    - 更友好的内置自定义路径匹配。

- Groovy构建模板支持（基于Groovy 2.3）。查看GroovyMakeupConfigure和各自的ViewResolver以及“View”的实现。

### 4.4 WebSocket Messaging Improvements

- SocketJS(java) 客户端支持。看SocketJsClient和相同包下的类。

- 新的应用程序上下文事件SessionSubscribeEvent和SessionUnscribeEvent在STOMP客户端订阅和非订阅时发生。

- 新的“websocket”scope。看第26.4.15节“WebSocket Scope”

- @SendToUser可以仅定位一个session并且不需要授权用户.

- @MessageMapping方法可以使用“.”来代替“/”作为路径分割。看SPR-11660。

- STOMP/WebSocket监控信息的收集和日志记录。查看第26.4.17节“运行时监控”。

- 显著优化和改善了日志，即使在调试级别也应该保持高可读性和紧凑性。

- 优化了消息的创建，包括支持可变性临时消息，避免自动生成的消息ID以及时间戳生成。查看MessageHeaderAccessor的Javadoc。

- WebSocket session建立60秒内没有活动，关闭STOMP/WebSocket session。查看SPR-11884。

### 4.5 Testing Improvements

- 在TestContext framework中可以使用Groovy脚本配置集成测试的ApplicationContext加载。

    - 查看“Context configruration with Groovy script”章节了解详情。

- 通过新的API TestTransaction，测试管理的事务在事务化的测试方法中可以以编程的方式启动和结束。

    - 查看“Programmactic transaction management”了解详情。

- 使用新的注解@Sql和@SqlConfig可以在每个类或者每个方法的基础上声明式的配置SQL脚本执行。

    - 查看第15.5.8节“执行SQL脚本”了解详情。

- 自动重写系统的测试属性源和应用属性源可以通过新注解@TestPropertySource进行配置。

    - 查看“COntext configuration with test property source”了解详情。

- 现在可以自动发现默认的TestExecutionListener。

    - 查看“Automatic discovery of default TestExecutionListeners”了解详情。

- 自定义的TestExecuteListener现在可以自动的合并到默认的监听器了。

    - 查看“TestExecutionListener合并”章节了解详情。

- TestContext framework里的事务测试支持的文档进行了更充分的解释，同时增加了更多的示例。

    - 查看第 15.5.7节“事务管理”了解详情。

- 改进了一些MockServletContext，MockHttpServletRequest以及其他Servlet API的模拟。

- 重构了AssertThrows用于支持Trowable替换Exception。

- 在Spring MVC Test中， 可以JSON Assert来断言JSON响应，作为额外的选择来使用JSONPath，就像使用XMLUnit为XML做的那样。

- 可以在MockMvcConfigurer的帮助下创建McokMvcBuilder。加入这个的目的是在应用Spring Security设置的时候使其更容易，同时可以用于为第三方框架或在一个项目里封装通用的配置。

- MockRestServiceServer现在为客户端测试增加了AsyncRestTmeplate支持。


### 5. Spring 4.2中的新特性和增强

#### 5.1 Core Container Improvements

- 诸如@Bean的注解通过检测，并且默认使用Java8的方法处理，允许使用默认的@Bean方法从接口创建一个配置类。

- 配置类可以使用规范的组件类来声明@Import，允许导入混合的配置类和组件类。

- 配置类可以声明一个@Order value，即使通过classpath扫描检测，也可以按照相应的顺序进行处理（比如根据名字重写bean）。

- @Resource注入点支持@Lazy声明，类似@Autowired为请求目标bean接收懒初始化代理。

- 应用的事件基础层现在提供了一个基于注解的模型以及发布任何任意事件的功能。

    - 任何受管理的bean的public方法都可以使用@EventListener进行注解。

    - @TransactionEventListener提供了事物绑定事件的支持。

- Spring Framework 4.2 为声明和查找注解属性的别名引入了非常好的支持。新的注解@AliasFor可以用一个注解声明一对别名属性，或者将一个自定义组合注解的属性声明为一个元注解属性的别名。

    - 下列注解已经用@AliasFor进行了重新修改，用于为他们的值属性提供有意义的别名：@Cacheable, @CacheEvict, @CachePut, @ComponentScan, @ComponentScan.Filter, @ImportResource, @Scope, @ManagedResource, @Header, @Payload, @SendToUser, @ActiveProfiles, @ContextConfiguration, @Sql, @TestExecutionListeners, @TestPropertySource, @Transactional,@ControllerAdvice, @CookieValue, @CrossOrigin, @MatrixVariable, @RequestHeader, @RequestMapping, @RequestParam, @RequestPart, @ResponseStatus, @SessionAttributes, @ActionMapping, @RenderMapping, @EventListener, @TransactionalEventListener。

    - 比如，spring-test模块中的@ContextConfiguration现在可以按下面的方式声明：

    ```
    public @interface ContextConfiguration {

        @AliasFor("locations")
        String[] value() default {};

        @AliasFor("value")
        String[] locations() default {};

        // ...
    }
    ```

    - 同样，组合注解重写元注解的属性现在可以使用@AliasFor进行细粒度的精确控制，这样属性会在注解层的内部被重写。实际上，现在可以为元注解的value属性声明一个别名。

    - 比如，现在可以编写一个带有自定义属性的组合注解，并按照下面的方式重写。

    ```
    @ContextConfiguration
    public @interface MyTestConfig {

        @AliasFor(annotation = ContextConfiguration.class, attribute = "value")
        String[] xmlFiles();

        // ...
    }

    ```

    - 查看Spring Annotation Programming Model。

- 改进了Spring的一些用于查找原注解的搜索算法。比如，声明局部组合注解现在更倾向于继承注解。

- 重写元注解属性的组合注解现在可以从interface，abstract，bridge模式，@interface以及类里，标准的方法里，构造方法里，成员变量里找到。

- 可以将多个注解属性合并（转换）表示在同一个注解中，（和AnnotationAttributes实例）。

- 基于成员变量的数据绑定（DirectFieldAccessor）功能已经与当前基于属性的数据绑定（BeanWrapper）保持一致。特别是现在基于field的绑定支持对Collections，Arrays，Maps的导航。

- DefaultConversionService现在为Stream，Charset，Currency以及TimeZone提供快捷的转换功能。此类转换也可以单独添加到任何任意的ConversionService中。

- DefaultFormattingConversionService为JSR-354 Money以及Currency(classpath中已经存在“javax.money”API）的值类型：命名，MonetaryAmount以及CurrencyUnit提供了很好的支持。该功能包括对应用@NumberFormat的支持。

- @NumberFormat现在可以当做meta-annotation来使用。

- JavaMailSenderImpl新增了一个方法testConnection()，用来检测连接服务器。

- ScheduledTaskRegistrar暴露了计划任务。

- Apache commons-pool2已支持AOP池CommonsPool2TargetSource。

- 通过在XML里暴露lang:std，为脚本化的bean引入了StandardScriptFactory作为基于JSR-223的机制。支持JavaScript和JRuby等等。（注意：JRubyScriptFactory和lang:jruby现在已经过时了，建议使用JSR-223）。

#### 5.2 Data Access Improvements

- 通过AspectJ提供javax.transaction.Transactional支持。

- SimpleJdbcCallOperations现在支持命名绑定。

- 完全支持Hibernate ORM 5.0：作为JPA提供者，以及访问Hibernate原生API(已用新的包org.springframework.orm.hibernate5覆盖)。

- 嵌入式数据库现在可以自动分配唯一的名字，并且<jdbc:embedded-database>增加支持了一个新的属性database=name。查看下面的“Testing Improvments” 进一步了解详情。

#### 5.3 JMS Improvements

- 可以通过JmsListenerContainerFactory控制autoStartup属性。

- Destination回复的类型现在可以在每个监听容器中配置。

- @SendTo注解的值现在可以使用Spring的EL表达式了。

- 相应地址现在可以在运行时使用JmsResponse进行计算。

- @JmsListener已是一个可重复的注解了，可以在同一个方法上声明几个JMS容器（如果你还没在用Java8，就要引用新的@JmsListeners）。

#### 5.4 Web Improvements

- HTTP流和Server-Sent Event支持，查看“HTTP Streaming”章节。

- 内建CORS支持，包括全局（MVC Java 配置和XML命名空间）和本地（比如@CrossOrigin）的配置，查看第27章“CORS支持”了解详情。

- HTTP缓存升级：

    - 新的CacheControl builder；加在了ResponseEntity，WebContentGenerator，ResourceHttpRequestHandler。

    - 在WebRequest里改进了ETag/Last-Modified支持。

- 自定义映射注解，将@RequestMapping作为元注解。

- 在运行时注册和注销AbstractionHandlerMethodMapping中的public方法。

- AbstractDispatcherServletInitializer中的protected方法createDispatcherServlet进一步自定义DispatcherServlet实例来使用。

- HandlerMethod作为@ExceptionHandler方法的一个方法参数，特别是在@ControllerAdvice组件中方便。

- java.util.concurrent.CompletableFuture成为@Controller方法的返回值类型。

- HttpHeaders字节范围请求支持，以及静态资源服务。

- 嵌套exception的@Response检测。

- RestTemplate中的UriTemplateHandler扩展点。

    - DefaultUriTemplate暴露了baseUrl属性和路径段编码选项。

    - 扩展点同样可以用于插入到任何URI模板库。

- 在RestTemplate中集成了OkHTTP。

 - 自定义的baseUrl，用于在MvcUriComponentsBuilder的方法中替换。

 - 序列化/反序列化的异常消息现在记录为WARN级别。

- 默认的JSON前缀已经从“{}&&” 改为更阿奴按的“)]}',”。

- 新的RequestBodyAdvice扩展点；支持Jackson的内置实现，用于@RequestBody方法参数上的@JsonView。

- 使用GSON或者Jackson2.6以上的时候，处理方法的返回类型用于如List<Foo>的序列化的参数类型。

- 为脚本话的web视图引入ScriptTemplateView作为基于JSR-223的机制，重点引入了Nashorn(JDK8)的JavaScript视图模板。

#### 5.5 WebSocket Messaging Improvments

- 暴露存在的已连接的用户和订阅的信息：

    - 新暴露了一个叫“userRegistry”的SimpUserRegistry bean。

    - 使用集群服务共享实时信息（查看代理中继配置选项）。

- 使用集群服务解析用户地址（查看代理中继配置选项）。

- StompSubProtocolErrorHandler扩展点对客户端进行自定义化及控制其STOMP ERROR帧。

- 通过@ControllerAdvice组件实现全局@MessageExceptionHandler方法。

- 使用SimpleBrokemrMessageHandler支持订阅心跳和SpEL表达式“selector” heador。

- 在TCP和WebSocket上使用STOMP客户端。查看第26.4.14章“STOMP Client”。

- @SendTo和@SendToUser可以包含地址变量占位符。

- 在@MessageMapping和@SubscribeMapping方法使用Jackson的@JsonView为返回值提供支持。

- @MessageMapping和@SubscribeMapping方法中ListenableFuture和CompletableFuture作为返回值类型。

- 为XML有效负荷提供MarshallingMessageConverter。

#### 5.6 Test Improvements

- 基于JUnit的单元测试可以使用JUnit规则代替SpringJUnit4ClassRunner执行。基于Spring的集成测试可以替换运行的runner，诸如JUnit的Parameterized或第三方的runners（比如MockitoJUnitRunner）。

    - 查看“Spring JUnit 4 Rules”章节了解详情。

-  Spring MVC Test框架对HtmlUnit提供很好的支持，包括集成Selenium的WebDriver，运行基于页面的web应用测试，而不需要部署到Servlet容器中。

    - 查看第15.6.2章“HtmlUnit Integration”了解更多。

- AopTestUtils，一个新的测试工具，允许开发者获取一个潜藏对象的引用，这些对象隐藏在一个或多个Spring代理后面。

    - 查看第14.2.1章“General testing utilities”了解更多。

- ReflectionTestUtils现在支持设置获取static字段（包括常量）。

- 使用@ActiveProfiles保留了bean定义声明配置文件的原始顺序，用以支持一些情况，比如Spring Boot中基于活动配置文件的名字来加载配置文件的的ConfigFileApplicationListener。

- @DirtiesContext支持新的BEAORE_METHOD,BEFORE_CLASS以及BEFORE_EACH_TEST_METHOD模式，用来在测试前关闭ApplicationContext——比如一些垃圾测试（还没有确定的）有大量的测试，破坏了ApplicationContext原始的配置。

- 新注解@Commit，用于直接替换@Rollback(false)。

- @Rollback现在用于配置类级别的默认回滚语义。

    - 因此，@TransactionConfiguration已经过时了，并会在之后的版本中去掉。

- 使用一个新的statements属性，@Sql支持执行内嵌SQL声明。

- ContextCache现在是一个public API，用于测试中缓存ApplicationContext。这是一个默认的实现，可以根据实际自定义的缓存需要进行替换。

- DefaultTestContext,DefaultBootstrapContext和DefaultCacheAwareContextLoaderDelegate在support子包中为public类，允许自定义扩展。

- TestContextBootstrapper负责构建TestContext。

- 在Spring MVC Test框架中，MvcResult的详细情况可以被记录为DEBUG级别或者写到自定义的OutputStream或Writer。查看MockMvcResultHandlers中新的log()，print(OutputStream)和print(Writer)方法了解详情。

- 在JDBC XML命名空间 <jdbc:embedded-database>中增加支持了一个新的database-name属性。允许开发者为嵌入式数据库设置唯一的名字--比如使用SpEL表达式或属性占位符就可以配当前活动bean定义配置文件感应到。

- 嵌入式数据库可以自动的调整为一个唯一的名字，允许在不同的ApplicationContext中使用一个测试组合复用通用的数据库测试配置。

    - 查看第19.8.6节“Generating unique names for embedded databases”了解更多。

- MockHttpServletRequest和MockHttpServletResponse通过getDateHeader和setDateHeader方法对数据头格式化提供了更好的支持。


### 6 Spring Framework 4.3新特性及增强

#### 6.1 Core Container Improvements

- 核心容器异常提供更丰富的元数据，以便程式化的评估。

- Java 8 默认方法作为bean属性getter/setter来检测。

- 如果注入一个主bean，就不会创建惰性候选bean。

- 如果目标bean只定义了一个构造方法，就不再需要再指定@Autowired注解。

- @Configuration类支持构造注入。

- 