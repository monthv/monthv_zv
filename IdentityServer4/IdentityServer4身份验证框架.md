# IdentityServer4身份验证框架

[好处]()：IdentityServer4是一个中间件，它将兼容[OpenID Connect]()和[OAuth2.0]()的端点添加到任意的一个ASP.NET CORE上面去。是为.NET CORE量身定做的。

## 概念

#### IdentityServer4基本

1. IdentityServer4是基于OpenID协议标准的身份认证和授权程序，它实现了[OpenID Connect]()和[OAuth2.0]()协议
2. 组成：Identity [身份]()、Server [服务器]()、4 [版本]()
3. 一个中间件服务框架，集成[OIDC]()与[OAuth2.0]()
4. 方便搭建任意多个项目
5. Github地址：https://github.com/IdentityServer
6. DEMO：https://demo.identityserver.io/

#### 知识点总结

##### 1、常见术语解析

- 身份认证服务器（[IdentityServer]()）

- 用户（[User]()）——资源所有者

- 客户端应用（[Client]()）——1、是一个应用，不是浏览器

  ​                                            2、WPF、MVC、SPA

- 受保护资源（[Resources]()）——1、资源服务器——API

  ​                                                    2、授权服务器——Identity Data（[身份数据]()）

- 访问令牌（[Access Token]()）——1、令牌和密码是类似的

  ​                                                    2、但是令牌是短期的，可撤销的，具有一定范围的

- 刷新令牌（[Refresh Token]()）——1、获取 Access Token

  ​                                                      2、可以随时控制访问权限，因为是新的 Access Token

- Scope（[范围]()）——在简单的情况下，API只需一个作用域。但是，在某些情况下，您可能希望细分APl功能，并允许不同客户端访问不同的部分。

- Bearer（[认证]()）

- Claims（[声明]()）

##### 3、JWT与OAuth2.0

- JWT是一种具体的，自身包含特定声明逻辑的，Token实现框架——账号密码登陆
- OAuth一种授权协议，是规范，不是实现——QQ授权机制

##### 2、OAuth2.0简介

- 是一种关于【授权】的协议——只能做授权，不能做认证

- 允许用户让第三方来访问某一个网站的资源而且不会泄露用户名密码，下边的2个场景——是代表而不是假冒

- 被同意授权后，发放Access Token

- 然后根据access token 获取资源——1、授权服务器的资源

  ​                                                            2、受保护的资源服务器的资源

- 场景一：简书的QQ注册与登录——1、资源拥有者（Resource Owner）-这里是Tom

  ​                                                           2、客户端应用（Client）-这里是某App

  ​                                                           3、授权服务器（Authorization Server）-这里当然还是QQ，因为QQ有相关数据

  ​                                                           4、资源服务器（Resource Server）-这里是QQ比如我们的【头像api】

- 场景二：vue项目的Idp登陆——1、用户：测试账号

​                                                              2、客户端：vue

​                                                              3、授权服务器：IdentityServer

​                                                              4、资源服务器：1、.NET CORE WebAPI项目 ？

​                                                                                            2、受保护的资源：Idp信息 ？                         

- 四种方式

  ###### 1、授权码

  A网站——B网站

  A——1、请求授权码——>>B

  A<<——2、返回授权码——B

  A——2、请求令牌——>>B		[后端处理]()，比如微信登陆

  A<<——2、返回令牌——B

  ###### 2、简洁模式

  A网站——B网站

  A——2、请求令牌——>>B

  A<<——2、返回令牌——B		比如我们的vue请求Ids4

  ###### 3、密码模式

  ###### 4、凭证模式——WPF调用

##### 4、OpenID、OIDC和OAuth的区别

- [OpenID]()是[认证]()，[OAuth2.0]()是[授权]()——1、Authentication、Authorization

  ​                                                                  2、一个是登陆，一个是授权

  ​                                                                  3、认证=【是不是】，授权=【给不给】

- OpenID更简单，只提供一个认证和字符串，去中心化的登陆认证，只需识别URL和OpenID即可，方便——【数字身份识别框架】

- OAuth是OpenID的一个补充，但是完全不同的服务，完全不需要提供任何信息个第三方，包括用户名

- Open'ID Connect兼容OAuth2.0+OpenID

5、常见的几种Ids4模式

- [客户端授权模式]()（Client Credentials，WPF调用）
- [密码授权模式]()（Resource Owner Password Credentials）
- [授权码授权模式]()（Authorization Code Flow，MVC调用）
- [简化授权模式]()-OpenlD（Implicit Flow，JS/Vue客户端调用）
- 混合模式-OpenID&OAuth（Hybrid Flow，角色+策略授权）
- 集成ASP.NET Core Identity and EntityFramework Core

6、其他登陆

- 单点登录
- 外部登录（比如QQ、Google、Github、Azure等）

#### 框架包含的内容

1、核心的IdentityServer[对象模型]()

2、服务和中间件

3、配置和中间件

4、自定义扩展用户数据

5、Quickstart UI

