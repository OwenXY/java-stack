#Spring Security

##  目录
- [前言](#前言)
    - [社区](#社区)
    - [5.1新增功能](#5.1新增功能)
    - [获得SpringSecurity](#获得SpringSecurity)
    - [项目模块](#项目模块)
    - [sampleApplication](#sampleApplication)
- [servlet应用程序](#servlet应用程序)
    - [java配置](#java配置)
    - [安全命令空间配置](#安全命令空间配置)
    - [架构与实施](#架构与实施)
        - [技术概述](#技术概述)
        - [核心服务](#核心服务)
    - [web应用程序安全](#web应用程序安全)
        - [安全赛选器链](#安全赛选器链)
        - [核心安全过滤器](#核心安全过滤器)
        - [servletAPi集成](#servletAPi集成)
        - [基本身份验证和摘要身份验证](#基本身份验证和摘要身份验证)
        - [记住我的身份](#记住我的身份)
        - [跨站请求伪造](#跨站请求伪造CSRF)
        - [CORS](#CORS)
        - [安全http响应Headers](#安全http响应Headers)
        - [会话Management](#会话Management)
        - [匿名身份验证](#匿名身份验证)
        - [WebSocket安全](#WebSocket安全)
    - [Authorization](#Authorization)
        - [授权架构](#授权架构)
        - [安全对象实现](#安全对象实现)
        - [基于表达式的访问控制](#基于表达式的访问控制)
    - [其他主题](#其他主题)
        - [域对象安全性ACL](#域对象安全性ACL)
        - [预身份验证方案](#预身份验证方案)
        - [LDAP](#LDAP)
        - [jsp标记库](#jsp标记库)
        - [Java身份验证和授权服务](#Java身份验证和授权服务)
        - [X.509身份验证](#509身份验证)
        - [运行身份验证](#运行身份验证)
        - [SpringSecurity加密模块](#SpringSecurity加密模块)
        - [并发支持](#并发支持)
        - [Java身份验证和授权服务](#Java身份验证和授权服务)
        - [SpringMVC集成](#SpringMVC集成)
    - [servlet环境webclient](#servlet环境webclient)
        - [webclientOauth2设置](#webclientOauth2设置)
        - [隐式OAuth2Authorization](#隐式OAuth2Authorization)
        - [显式OAuth2Authorization](#显式OAuth2Authorization)
        - [明确的OAuth2Authorization](#明确的OAuth2Authorization)
        - [clientRegistration](#clientRegistration)
        - [X.509身份验证](#509身份验证)
        - [运行身份验证](#运行身份验证)
        - [SpringSecurity加密模块](#SpringSecurity加密模块)
        - [并发支持](#并发支持)
        - [Java身份验证和授权服务](#Java身份验证和授权服务)
        - [SpringMVC集成](#SpringMVC集成)
    - [spring数据集成](#spring数据集成)
        - [spring数据和spring安全性](#spring数据和spring安全性)
        - [@Query中安全表达式](#Query中安全表达式)
    - [Appendix](#Appendix)
        - [安全数据库架构](#安全数据库架构)
        - [安全命名空间](#安全命名空间)
        - [spring安全性依存关系](#spring安全性依存关系)
        - [代理服务器配置](#代理服务器配置)
        - [SpringSecurity常见问题解答](#SpringSecurity常见问题解答)
        - [X.509身份验证](#509身份验证)
        - [运行身份验证](#运行身份验证)
        - [SpringSecurity加密模块](#SpringSecurity加密模块)
        - [并发支持](#并发支持)
        - [Java身份验证和授权服务](#Java身份验证和授权服务)
        - [SpringMVC集成](#SpringMVC集成)
- [ReactiveApplication](#ReactiveApplication)
    - [WebFluxSecurity](#WebFluxSecurity)
    - [DefaultSecurityHeaders](#DefaultSecurityHeaders)
    - [RedirectToHttps](#RedirectToHttps)
    - [OAuth2WebFlux](#OAuth2WebFlux)
    - [@RegisteredOAuth](#RegisteredOAuth)
    - [WebClient](#WebClient)  
    - [EnableReactiveMethodSecurity](#EnableReactiveMethodSecurity)
    - [ReactiveTestSupport](#ReactiveTestSupport)
    

# 前言

## 社区

### 源代码

Spring Security 为基于 Java EE 的企业软件应用程序提供了全面的安全解决方案。
应用程序安全性的两个主要方面是“**身份验证**”和“**授权**”(或“访问控制”)。
这是 Spring Security 的两个主要领域。
“**认证**”是构建委托人的过程，所谓委托人就是他们所宣称的身份(“主要”通常是指可以在您的应用程序中执行操作的用户，设备或其他系统)。
“**授权**”是指确定的过程是否允许委托人在您的应用程序中执行操作。为了到达需要授权决策的位置，主体的身份已经通过身份验证过程确定。这些概念是通用的，并非完全针对于 Spring Security。

##### 源码

    git clone https://github.com/spring-projects/spring-security.git


在身份验证级别，Spring Security 支持多种身份验证模型。
这些身份验证模型中的大多数要么由第三方提供，要么由相关的标准机构(例如 Internet 工程任务组)开发。
另外，Spring Security 提供了自己的一组身份验证功能。具体来说，Spring Security 当前支持与所有以下技术的身份验证集成：
HTTP BASIC 身份验证 Headers(基于 IETF RFC 的标准)
  - HTTP 摘要验证 Headers(基于 IETF RFC 的标准)

  - HTTP X.509Client 端证书交换(基于 IETF RFC 的标准)

  - LDAP(一种非常常见的跨平台身份验证方法，特别是在大型环境中)

  - 基于表单的身份验证(用于简单的用户界面需求)

  - OpenID authentication

  - 基于预先构建的请求 Headers 的身份验证(例如 Computer Associates Siteminder)

  - Jasig 中央认证服务(也称为 CAS，这是一种流行的开源单点登录系统)

  - 远程方法调用(RMI)和 HttpInvoker(Spring 远程协议)的透明身份验证上下文传播

  - 自动的“记住我”身份验证(因此您可以在方框中打勾，以避免在 sched 的时间段内进行重新身份验证)

  - 匿名身份验证(允许每个未经身份验证的调用自动采用特定的安全身份)

  - 运行身份验证(如果一个调用应以不同的安全身份进行则很有用)

  - Java 身份验证和授权服务(JAAS)

  - Java EE 容器身份验证(因此，如果需要，您仍然可以使用容器 Management 的身份验证)

  - Kerberos

  - Java 开源单一登录(JOSSO)*

  - OpenNMS 网络 Management 平台*

  - AppFuse *

  - AndroMDA *

  - ule 子 ESB *

  - 直接 Web 请求(DWR)*

  - Grails *

  - Tapestry *

  - JTrac *

  - Jasypt *

  - Roller *

  - 弹性路径*

  - Atlassian 人群*

  -您自己的身份验证系统(请参见下文)
  
#### 获取SpringSecurity

Spring Security 版本的格式为 MAJOR.MINOR.PATCH，这样

    主要版本可能包含重大更改。通常，这样做是为了提供改进的安全性以匹配现代安全性实践。
    
    MINOR 版本包含增强功能，但被视为被动更新
    
    PATCH 级别应完全兼容，向前和向后兼容，可能存在的 exception 是为了修复错误
    Maven用法
##### maven用法

###### 使用 Maven 进行 Spring Boot
```java

<dependencies>
    <!-- ... other dependency elements ... -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-security</artifactId>
    </dependency>
</dependencies>
```

由于 Spring Boot 提供了一个 Maven BOM 来 Management 依赖版本，因此无需指定版本。如果您想覆盖 Spring Security 版本，可以通过提供 Maven 属性来实现：

```java

<properties>
    <!-- ... -->
    <spring-security.version>5.1.2.RELEASE</spring-security.version>
</dependencies>
```

由于 Spring Security 仅在主要版本中进行重大更改，因此可以安全地在 Spring Boot 中使用更新版本的 Spring Security。但是，有时可能还需要更新 Spring Framework 的版本。
也可以通过添加 Maven 属性轻松完成此操作

```java
<properties>
    <!-- ... -->
    <spring.version>5.1.3.RELEASE</spring.version>
</dependencies>
```

###### 没有 Spring Boot 的 Maven

最小的SpringSecurity maven依赖
```java
    <dependencies>
    <!-- ... other dependency elements ... -->
    <dependency>
        <groupId>org.springframework.security</groupId>
        <artifactId>spring-security-web</artifactId>
        <version>4.2.10.RELEASE</version>
    </dependency>
    <dependency>
        <groupId>org.springframework.security</groupId>
        <artifactId>spring-security-config</artifactId>
        <version>4.2.10.RELEASE</version>
    </dependency>
    </dependencies>

```
###### Maven 存储库
所有的GA版本（即以.RELEASE结尾的版本），均已部署到MavenCentral，因此无需在pom中申明其他maven存储库

如果您使用的是 SNAPSHOT 版本，则需要确保已定义 Spring Snapshot 存储库，如下所示

```java
<repositories>
<!-- ... possibly other repository elements ... -->
<repository>
	<id>spring-snapshot</id>
	<name>Spring Snapshot Repository</name>
	<url>http://repo.spring.io/snapshot</url>
</repository>
</repositories>

```

如果您使用的是里程碑版本或候选版本，则需要确保定义了 Spring Milestone 存储库，如下所示：
```java

<repositories>
<!-- ... possibly other repository elements ... -->
<repository>
	<id>spring-milestone</id>
	<name>Spring Milestone Repository</name>
	<url>http://repo.spring.io/milestone</url>
</repository>
</repositories>
```
Spring Framework Bom
Spring Security 是基于 Spring Framework 4.3.21.RELEASE 构建的，但应与 4.0.x 一起使用。许多用户将遇到的问题是 Spring Security 的可传递依赖项解决了 Spring Framework 4.3.21RELEASE，这可能会导致奇怪的 Classpath 问题。

解决该问题的一种(乏味的)方法是将所有 Spring Framework 模块包含在 pom 的<dependencyManagement>部分中。另一种方法是将spring-framework-bom包含在pom.xml的<dependencyManagement>部分中，如下所示：

```java

<dependencyManagement>
	<dependencies>
	<dependency>
		<groupId>org.springframework</groupId>
		<artifactId>spring-framework-bom</artifactId>
		<version>4.3.21.RELEASE</version>
		<type>pom</type>
		<scope>import</scope>
	</dependency>
	</dependencies>
</dependencyManagement>
```

这将确保 Spring Security 的所有传递依赖项都使用 Spring 4.3.21RELEASE 模块。

Note

    此方法使用 Maven 的“物料 Lists”(BOM)概念，并且仅在 Maven 2.0.9 中可用。有关如何解决依赖关系的其他详细信息，请参见Maven 的依赖机制简介文档。

#### 项目模块

核心包：spring-security-core.jar
    
    包含核心身份验证和访问控制类和接口，远程支持和基本配置 API。
    使用 Spring Security 的任何应用程序都需要。
    支持独立的应用程序，远程 Client 端，方法(服务层)安全性和 JDBC 用户配置。

远程处理：spring-security-remoting.jar

        提供与 Spring Remoting 的集成。除非您正在编写使用 Spring Remoting 的远程 Client 端，否则您不需要这样做。
        主要包是org.springframework.security.remoting。

网络：spring-security-web.jar

    包含过滤器和相关的 Web 安全基础结构代码。任何与 servlet API 依赖的东西。
    如果您需要 Spring Security Web 认证服务和基于 URL 的访问控制，则将需要它。
    主要包是org.springframework.security.web。

配置：spring-security-config.jar

    包含安全名称空间解析代码和 Java 配置代码。
    如果您使用 Spring Security XML 名称空间进行配置或 Spring Security 的 Java 配置支持，则需要它。
    主要包是org.springframework.security.config。这些类都不打算直接在应用程序中使用。

LDAP：spring-security-ldap.jar

    LDAP 身份验证和配置代码。如果您需要使用 LDAP 身份验证或 ManagementLDAP 用户条目，则为必需。
    顶级软件包是org.springframework.security.ldap。

OAuth 2.0 核心:spring-security-oauth2-core.jar

        spring-security-oauth2-core.jar包含核心类和接口，这些类和接口提供对* OAuth 2.0 授权框架和 OpenID Connect Core 1.0 的支持。
        使用 OAuth 2.0 或 OpenID Connect Core 1.0 *的应用程序(例如 Client 端，资源服务器和授权服务器)需要它。
        顶级软件包是org.springframework.security.oauth2.core。

OAuth 2.0Client:spring-security-oauth2-client.jar

    spring-security-oauth2-client.jar是 Spring Security 对* OAuth 2.0 Authorization Framework 和 OpenID Connect Core 1.0 *的 Client 端支持。
    利用 OAuth 2.0 登录 和/或 OAuthClient 端支持的应用程序需要。顶级软件包是org.springframework.security.oauth2.client。

OAuth 2.0:JOSE-spring-security-oauth2-jose.jar
    
    spring-security-oauth2-jose.jar包含 Spring Security 对* JOSE *(Javascript 对象签名和加密)框架的支持。 
    * JOSE *框架旨在提供一种在各方之间安全转移索赔的方法。它是根据一系列规范构建的：
        JSON Web 令牌(JWT)

        JSON Web 签名(JWS)
        
        JSON Web 加密(JWE)
        
        JSON Web 密钥(JWK)
        
        JSON Web 令牌(JWT)
        
        JSON Web 签名(JWS)
        
        JSON Web 加密(JWE)

    它包含顶级软件包：

        org.springframework.security.oauth2.jwt
        
        org.springframework.security.oauth2.jose

ACL：spring-security-acl.jar 

    专门的域对象 ACL 实现。用于将安全性应用于应用程序中的特定域对象实例。
    顶级软件包是org.springframework.security.acls。

CAS：spring-security-cas.jar

    Spring Security 的 CASClient 端集成。
    如果您想将 Spring Security Web 认证与 CAS 单一登录服务器一起使用。顶级软件包是org.springframework.security.cas。

OpenID：spring-security-openid.jar

    OpenID Web 身份验证支持。
    用于根据外部 OpenID 服务器对用户进行身份验证。
    org.springframework.security.openid。需要 OpenID4Java。

测试：spring-security-test.jar
    
    支持使用 Spring Security 进行测试。


#### sampleApplication

该项目提供了几个示例 Web 应用程序。

    https://github.com/spring-projects/spring-security.git

教程 samples

    教程 samples 是一个入门的不错的基本示例。它始终使用简单的名称空间配置。编译后的应用程序包含在分发 zip 文件中，可以立即部署到您的 Web 容器(spring-security-samples-tutorial-3.1.x.war)中。 form-based身份验证机制与常用的remember-me身份验证提供程序结合使用，可以使用 cookie 自动记住登录信息。
    
    我们建议您从教程示例开始，因为 XML 最少且易于遵循。最重要的是，您可以轻松地将此 XML 文件(及其相应的web.xml条目)添加到现有应用程序中。建议仅在实现这种基本集成时，才尝试添加方法授权或域对象安全性。

Contacts

    联系人示例是一个高级示例，它说明了域对象访问控制列表(ACL)除了基本的应用程序安全性之外，还具有更强大的功能。该应用程序提供了一个界面，用户可以使用该界面来 Management 联系人(域对象)的简单数据库。

    要进行部署，只需将 WAR 文件从 Spring Security 发行版复制到容器的webapps目录中。War 应称为spring-security-samples-contacts-3.1.x.war(附加的版本号将根据您使用的发行版而有所不同)。
    
    启动容器后，检查应用程序是否可以加载。访问http://localhost:8080/contacts(或适用于您的 Web 容器和所部署的 WAR 的 URL)。
    
    接下来，单击“调试”。系统将提示您进行身份验证，并在该页面上建议一系列用户名和密码。只需使用其中任何一个进行身份验证，然后查看结果页面。它应包含类似于以下内容的成功消息：
```java

Security Debug Information

Authentication object is of type:
org.springframework.security.authentication.UsernamePasswordAuthenticationToken

Authentication object as a String:

org.springframew[emailprotected]1f127853:
Principal: [emailprotected]: Username: rod; \
Password: [PROTECTED]; Enabled: true; AccountNonExpired: true;
credentialsNonExpired: true; AccountNonLocked: true; \
Granted Authorities: ROLE_SUPERVISOR, ROLE_USER; \
Password: [PROTECTED]; Authenticated: true; \
Details: org.sprin[emailprotected]0: \
RemoteIpAddress: 127.0.0.1; SessionId: 8fkp8t83ohar; \
Granted Authorities: ROLE_SUPERVISOR, ROLE_USER

Authentication object holds the following granted authorities:

ROLE_SUPERVISOR (getAuthority(): ROLE_SUPERVISOR)
ROLE_USER (getAuthority(): ROLE_USER)

Success! Your web filters appear to be properly configured!
```
成功收到上述消息后，请返回示例应用程序的主页，然后单击“Management”。然后，您可以尝试该应用程序。请注意，仅显示当前登录用户可用的联系人，并且只有具有ROLE_SUPERVISOR的用户才有权删除其联系人。在幕后，MethodSecurityInterceptor正在保护业务对象。

该应用程序允许您修改与不同联系人关联的访问控制列表。请务必尝试一下，并通过查看应用程序上下文 XML 文件来了解其工作原理。

LDAP 示例

    LDAP 示例应用程序提供了基本配置，并使用传统 Bean 在同一个应用程序上下文文件中设置了名称空间配置和等效配置。这意味着实际上在此应用程序中配置了两个相同的身份验证提供程序

OpenID 示例
    
    OpenID 示例演示了如何使用名称空间配置 OpenID 以及如何为 Google，Yahoo 和 MyOpenID 身份提供程序设置attribute exchange配置(可以根据需要尝试添加其他名称)。它使用基于 JQuery 的openid-selector项目来提供用户友好的登录页面，该页面使用户可以轻松选择提供程序，而无需 Importing 完整的 OpenID 标识符。

    该应用程序与普通身份验证方案的不同之处在于，它允许任何用户访问该站点(前提是他们的 OpenID 身份验证成功)。首次登录时，您将收到“ Welcome [您的名字]”消息。如果您注销并重新登录(使用相同的 OpenID 身份)，则应更改为“ Welcome Back”。这可以通过使用自定义UserDetailsService，它将标准角色分配给任何用户，并将身份存储在内部 Map 中。显然，实际的应用程序将使用数据库来代替。查看源表单中的更多信息。此类还考虑到以下事实：不同的属性可能会从不同的提供者处返回，并构建相应的用户名称。

CASsamples

    CAS 示例要求您同时运行 CAS 服务器和 CASClient 端。它不包含在发行版中，因此您应按照the introduction所述检出项目代码。您将在sample/cas目录下找到相关文件。那里还有一个Readme.txt文件，该文件说明了如何直接从源树运行服务器和 Client 端，并带有 SSL 支持。

JAAS 示例

    JAAS 示例是一个非常简单的示例，说明如何在 Spring Security 中使用 JAAS LoginModule。如果用户名等于密码，则提供的 LoginModule 将成功验证用户身份，否则将引发 LoginException。在此示例中使用的 AuthorityGranter 始终授予角色 ROLE_USER。该示例应用程序还演示了如何通过将jaas-api-provision设置为“ true”来作为 LoginModule 返回的 JAAS 主题来运行。

身份验证前 samples

    此示例应用程序演示了如何从pre-authentication框架连接 bean，以利用 Java EE 容器中的登录信息。用户名和角色是容器设置的用户名和角色。

### servlet应用程序

#### java配置

 
第一步是创建我们的 Spring Security Java 配置。该配置将创建一个称为**springSecurityFilterChain的 Servlet 过滤器**，该过滤器负责应用程序中的所有安全性(保护应用程序 URL，验证提交的用户名和密码，重定向到登录表单等)。
 
 ```java

import org.springframework.beans.factory.annotation.Autowired;

import org.springframework.context.annotation.*;
import org.springframework.security.config.annotation.authentication.builders.*;
import org.springframework.security.config.annotation.web.configuration.*;

@EnableWebSecurity
public class WebSecurityConfig implements WebMvcConfigurer {

    @Bean
    public UserDetailsService userDetailsService() throws Exception {
        InMemoryUserDetailsManager manager = new InMemoryUserDetailsManager();
        manager.createUser(User.withDefaultPasswordEncoder().username("user").password("password").roles("USER").build());
        return manager;
    }
}
```

此配置的确没有太多，但是它做了很多。您可以找到以下功能的摘要：

要求对应用程序中的每个 URL 进行身份验证

为您生成一个登录表单

允许具有 Username * user *和 Password * password *的用户使用基于表单的身份验证进行身份验证

允许用户注销

CSRF attack prevention

Session Fixation protection

安全标题集成

HTTP 严格传输安全安全请求

X-Content-Type-Options integration

缓存控制(以后可以由您的应用程序覆盖以允许缓存您的静态资源)

X-XSS-Protection integration

X-Frame-Options 集成有助于防止Clickjacking

与以下 Servlet API 方法集成

HttpServletRequest#getRemoteUser()

HttpServletRequest.html#getUserPrincipal()

HttpServletRequest.html#isUserInRole(java.lang.String)

HttpServletRequest.html#login(java.lang.String, java.lang.String)

HttpServletRequest.html#logout()

第二步：向 War 注册springSecurityFilterChain
    
    可以在 Servlet 3.0 环境中使用Spring 的 WebApplicationInitializer 支持在 Java 配置中完成此操作。毫不奇怪，Spring Security 提供了一个 Base ClassAbstractSecurityWebApplicationInitializer，它将确保springSecurityFilterChain为您注册。使用AbstractSecurityWebApplicationInitializer的方式因我们是否已经在使用 Spring 或 Spring Security 是应用程序中唯一的 Spring 组件而异。
    
    第 6.1.2 节“不存在 Spring 的 AbstractSecurityWebApplicationInitializer”-如果您尚未使用 Spring，请按照以下说明进行操作
    
    第 6.1.3 节“带有 Spring MVC 的 AbstractSecurityWebApplicationInitializer”-如果您已经在使用 Spring，请按照以下说明进行操作


不存在 Spring 的 AbstractSecurityWebApplicationInitializer
    如果您不使用 Spring 或 Spring MVC，则需要将WebSecurityConfig传递到超类中，以确保配置被接受。您可以在下面找到一个示例
```java
    import org.springframework.security.web.context.*;
    
public class SecurityWebApplicationInitializer
    extends AbstractSecurityWebApplicationInitializer {

    public SecurityWebApplicationInitializer() {
        super(WebSecurityConfig.class);
    }
}
```
    
    SecurityWebApplicationInitializer将执行以下操作：
    
    为应用程序中的每个 URL 自动注册 springSecurityFilterChain 过滤器
    
    添加一个加载WebSecurityConfig的 ContextLoaderListener。

使用 Spring MVC 的 AbstractSecurityWebApplicationInitializer

如果我们在应用程序的其他地方使用 Spring，则可能已经有一个WebApplicationInitializer用来加载 Spring 配置。如果我们使用以前的配置，将会得到一个错误。相反，我们应该使用现有的ApplicationContext注册 Spring Security。例如，如果我们使用 Spring MVC，则SecurityWebApplicationInitializer如下所示：
```java

import org.springframework.security.web.context.*;

public class SecurityWebApplicationInitializer
    extends AbstractSecurityWebApplicationInitializer {

}
```
这只会为应用程序中的每个 URL 仅注册 springSecurityFilterChain 过滤器。之后，我们将确保WebSecurityConfig已加载到我们现有的 ApplicationInitializer 中。例如，如果我们使用的是 Spring MVC，则将其添加到getRootConfigClasses()
```java
public class MvcWebApplicationInitializer extends
        AbstractAnnotationConfigDispatcherServletInitializer {

    @Override
    protected Class<?>[] getRootConfigClasses() {
        return new Class[] { WebSecurityConfig.class };
    }

    // ... other overrides ...
}
```

