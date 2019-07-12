## 一、Spring 整体架构和环境搭建

### （一）Spring 的整体架构

​	`Spring` 框架是一个分层架构，它包含一系列的功能要素，并被分为大约20个模块，如下图：

![](C:\Users\jonas\Desktop\读书笔记\images\微信截图_20190620174448.png)

这些模块可以总结为以下几个部分：

- `Core Container` ：**核心容器，包含有 `Core、Beans、Context、Expression Language` 模块。**其中，`Core` 和 `Beans` 模块是框架的基础部分，提供 `IoC` 和依赖注入特性。这里的基础概念是 `BeanFactory` ，它提供对 `Factory` 模式的经典实现来消除对程序性单例模式的需要，并真正允许你从逻辑中分离出依赖关系和配置。
  - `Core` 模块主要包含 `Spring` 框架基本的核心工具类，是其他组件的基本核心。
  - `Beans` 模块是所有应用都要用到的，包含访问配置文件、创建和管理 `bean` 以及进行 `IoC` 操作相关的所有类。
  - `Context` 模块构建于 `Core` 和 `Beans` 模块基础之上，提供了一种注册器的框架式的对象访问方法。它继承了 `Beans` 的特性，为 `Spring` 核心提供了大量扩展，添加了对国家化、事件传播、资源和对 `Context` 的透明创建的支持。`ApplicationContext` 是它的关键。
  - `Expression Language` 模块提供了强大的表达式语言，用于在运行时查询和操纵对象。它是 `JSP` 的扩展。

- `Data Access` ：**包含 `JDBC、ORM、OXM、JMS 和 Transaction` 模块。**
  - `JDBC` 模块提供了一个 `JDBC` 抽象层，它可以消除冗长的 `JDBC` 编码和解析数据库厂商特有的错误代码。这个模块包含了 `Spring` 对 `JDBC` 数据访问进行封装的所有类。
  - `ORM` 模块为对象-关系映射API，如 `JPA、JDO、Hibernate、iBatis`，提供了一个交互层。利用 `ORM` 封装包，可以混合使用所有 `Spring` 提供的特性进行 `O/R` 映射。
  - `OXM` 模块提供了一个对 `Object/XML` 映射实现的抽象层，`Object/XML` 映射实现包括 `JAXB、Castor、XMLBeans、JiBX、XStream` 。
  - `JMS` 模块主要包含了一些制造和消费信息的特性。
  - `Transaction` 模块支持编程和声明性的事务管理，这些事务类必须实现特定的接口，并且对所有的 `POJO` 都适用。

- `Web` ：`Web` 模块建立在应用程序上下文模块之上，为基于 `Web` 的应用程序提供上下文。`Web` 层包括 `Web、Web-Servlet、Web-Porlet` 。
  - `Web` 模块，提供了基础的面向 `Web` 的集成特性。例如，多文件上传、使用 `servlet listeners` 初始化 `IoC` 容器以及一个面向 `Web` 的应用上下文。
  - `Web-Servlet` 模块包含 `Spring` 的 `model-view-controller（MVC）` 实现。
  - `Web-Porlet` 模块：提供了用于 `Porlet` 环境和 `Web-Servlet` 模块的 `MVC` 的实现。

- `AOP`：`AOP` 模块提供了一个符合 `AOP` 联盟标准的面向切面编程的实现，它让你可以定义方法拦截器和切点，从而将逻辑代码分开，降低他们之间的耦合性。
- `Aspects` 模块提供了对 `AspectJ` 的集成支持。
- `Instrumentation` 模块提供了 `class instrumentation` 支持和 `classloader` 实现，使得可以在特定的应用服务器上使用。
- `Test` 模块支持使用 `JUnit` 和 `TestNG` 对 `Spring` 组件进行测试。

---

### （二）容器的基本实现









































