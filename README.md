# 🚀id-server
一个基于**Spring Authorization Server**的开源的授权服务器，欢迎Star，如果有兴趣也可以对本项目发起贡献。
- gitee: [https://gitee.com/felord/id-server](https://gitee.com/felord/id-server)
- 文档建设中……
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
- 你可以通过`root`用户做这些事情：
  - 创建角色（角色管理）并为角色绑定权限。
  - 创建控制台管理用户（用户管理），并赋予他们角色。
> 退出功能还未完善，需要通过关闭浏览器来清除session。
## oauth2 测试方法
- 启动**Id Server**，默认情况下在客户端列表提供了一个内置的OAuth2客户端。
- 样例客户端在`samples`文件夹下，直接启动，浏览器配置文件下的`http://127.0.0.1:8082/foo/bar`，进入登录页，输入用户名`user`和密码`user`即可。
- 你也可以在Id Server中创建一个客户端并模仿DEMO中的配置，主要修改`client-id`,`client-secret`,`client-authentication-method`,`scope`，其它选项除非你比较了解OAuth2，否则先不要动，也可以通过issue咨询。
> `redirect-uri`必须在授权服务器Id Server注册客户端时声明。
## 环境
目前**Id Server**提供**H2**和**Mysql**两种数据库环境，分别对应`application-h2.yml`和`application-mysql.yml`两个配置文件。
- **H2**，默认数据库，在**H2**环境下，数据库DDL脚本和DML脚本会自动执行，无需开发者手动执行，该环境主要用来测试、研究、学习。
- **Mysql**，生产推荐，**首次启动时开发者手动执行初始化DML脚本**。
> 目前两种环境的效果是一致的，切换时务必在`pom.xml`中更换对应的数据库驱动程序依赖。
## 概念
一些概念
### OAuth2Client 

**客户端**指的是**OAuth2 Client**，但又不单单是一个**OAuth2 Client**，连**id server**本身都是一个**客户端**。

### `role`和`scope`的关系

`role`和`scope`其实是一个东西，只不过面向的对象不一样。`role`针对的是资源拥有者（Resource Owner），而`scope`针对的是**OAuth2客户端**。举个例子，`ROLE_email`是用户具有获取电子邮件信息的接口访问权限，`SCOPE_email`是拥有`ROLE_email`权限的用户授权OAuth2客户端访问获取电子邮件信息接口，用户如果没有这个权限，那他凭什么授权呢？
> 所以结论就是： `ROLE_email`=`SCOPE_email`=`email`。

