# 🚀id-server

一个基于**Spring Authorization Server**的开源的授权服务器，欢迎Star。
## 主要功能
- 创建OAuth2客户端，并对OAuth2客户端进行管理。
- UI控制台，可动态调整管理员的用户角色。
## 主要技术
- Spring Boot
- Spring Security
- Spring Authorization Server
- Spring Data JPA
- H2 数据库
- layui

## 简单用法

- 拉取主分支最新代码到本地。
- 通过`IdServerApplication`来启动授权服务器。管理控制台本地登录路径为`http://localhost:9000/system/login`，最高权限用户为`root`，密码为`idserver`。
- 你可以通过`root`用户创建管理其它控制台管理员用户，并赋予他们角色。
## oauth2 测试方法
- 在**Id Server**中创建一个OAuth2客户端，自己记住密码，密码功能还不够完善。
- 样例客户端在`samples`文件夹下，根据创建的OAuth2客户端信息修改配置，主要是`client-id`,`client-secret`,`client-authentication-method`,`scope`，其它选项除非你比较了解OAuth2，否则先不要动，也可以通过issue咨询。
- 调用`redirect-uri`，进入登录页，输入用户名`user`和密码`user`即可。
> `redirect-uri`必须在授权服务器Id Server注册客户端时声明。

## 概念
一些概念
### OAuth2Client 

**客户端**指的是**OAuth2 Client**，但又不单单是一个**OAuth2 Client**，连**id server**本身都是一个**客户端**。

### `role`和`scope`的关系

`role`和`scope`其实是一个东西，只不过面向的对象不一样。`role`针对的是资源拥有者（Resource Owner），而`scope`针对的是**OAuth2客户端**。举个例子，`ROLE_email`是用户具有获取电子邮件信息的接口访问权限，`SCOPE_email`是拥有`ROLE_email`权限的用户授权OAuth2客户端访问获取电子邮件信息接口，用户如果没有这个权限，那他凭什么授权呢？
> 所以结论就是： `ROLE_email`=`SCOPE_email`=`email`。

