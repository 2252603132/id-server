# 🚀id-server

一个基于**Spring Authorization Server**的开源的授权服务器。


## 简单用法

- 初始化数据脚本自行执行`init.sql`，自行修改数据库链接。
- 管理后台登录 `http://localhost:9000/system/login`，默认管理用户`felord`、默认密码`123456`。
- 目前客户端功能初步完成，授权确认页面（未完成），因此建立客户端时需要关闭授权确认选项。
- 自行建立一个客户端，选择`client_secret_basic`或者`client_secret_post`，除非你看过我的教程，知道其它的怎么玩。
- 授权测试账号密码分别为`user`和`user`，暂时这个还没有对接数据库先弄个临时账号能跑通。
- 搞一个客户端应用，参考 [spring-security-oauth2-tutorial](https://gitee.com/felord/spring-security-oauth2-tutorial)中的客户端应用，配置改成自己刚创建的客户端信息。

## 概念
一些概念
### OAuth2Client 

**客户端**指的是**OAuth2 Client**，但又不单单是一个**OAuth2 Client**，连**id server**本身都是一个**客户端**。
#### role

角色必须依附于客户端的存在，本项目的根本就在于管理客户端，所以角色必须有客户端的属性，这样和**SCOPE**的设计才是一致的。

> `role`和`scope`的关系是怎样的？

`role`和`scope`其实是一个东西，只不过面向的对象不一样。`role`针对的是资源拥有者（Resource Owner），而`scope`针对的是**OAuth2客户端**。举个例子，`ROLE_email`是用户具有获取电子邮件信息的接口访问权限，`SCOPE_email`是拥有`ROLE_email`权限的用户授权OAuth2客户端访问获取电子邮件信息接口，用户如果没有这个权限，那他凭什么授权呢？
> 所以结论就是： `ROLE_email`=`SCOPE_email`=`email`。

