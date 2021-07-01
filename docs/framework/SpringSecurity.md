#Spring Security

##  目录
- [架构设计](#架构设计)
    - [技术概述](#技术概述)
    - [核心服务](#核心服务)


# 架构设计


spring security 整体架构

![img.png](images/springSecurity_整体架构.png)

## 技术概述

核心组件 SecurityContextHolder,SecurityContext和Authentication

    最基本的对象是SecurityContextHolder，它是我们存储当前应用程序安全上下文的详细信息，其中包括当前应用程序的主题详细信息。如当前操作用户是谁，该用户是否已经被认证，他拥有哪些角色权限等。

    默认情况下，SecurityContextHolder 使用ThreadLocal来存储这些详细信息，这意味着SecurityContext始终可用于同一执行线程中的方法，即使这些SecurityContext未作为这些方法的参数显示传递。

获取当前用户信息

    因为身份信息与当前执行线程已绑定，所以可以使用一下代码块在应用程序中获取当前已验证的用户的用户名

```java
Object principal = SecurityContextHolder.getContext()
  .getAuthentication().getPrincipal();

if (principal instanceof UserDetails) {
  String username = ((UserDetails)principal).getUsername();
} else {
  String username = principal.toString();
}
```
    调用getContext()返回的是SecurityContext接口的一个实例，对应SecurityContext接口定义如下：

```java
public interface SecurityContext extends Serializable {
	Authentication getAuthentication();
	void setAuthentication(Authentication authentication);
}
```

Authentication

    在SecurityContext接口中定义了getAuthentication()和setAuthentication()两个抽象方法，当调用getAuthentication()方法后，会返回一个Authentication类型的对象
    这里的Authentication也是一个接口，它的定义如下：

```java
// org/springframework/security/core/Authentication.java
public interface Authentication extends Principal, Serializable {
  // 权限信息列表，默认是GrantedAuthority接口的一些实现类，通常是代表权限信息的一系列字符串。
	Collection<? extends GrantedAuthority> getAuthorities();
  // 密码信息，用户输入的密码字符串，在认证过后通常会被移除，用于保障安全。
	Object getCredentials();
	Object getDetails();
  // 最重要的身份信息，大部分情况下返回的是UserDetails接口的实现类，也是框架中的常用接口之一。
	Object getPrincipal();
	boolean isAuthenticated();
	void setAuthenticated(boolean isAuthenticated) throws IllegalArgumentException;
}
```
    以上的Authentication接口是spring-security-core.jar包下的接口，直接继承自Principal类，而Principal位于Java.security包中，
    由此可知Authentication是spring security中的核心接口。
    通过这个Authentication接口的实现类，我们可以得到用户拥有的权限信息列表，密码用户细节信息，用户身份信息，认证信息等

**小结**

    