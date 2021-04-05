#Spring Security

##  目录
- [前言](#前言)
    - [社区](#社区)
    - [5.1新增功能](#5.1新增功能)
    - [获得SpringSecurity](#获得SpringSecurity)
    - [项目模块](#项目模块)
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
    

### 前言

#### 社区

###### 源代码

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

JSON Web 密钥(JWK)

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