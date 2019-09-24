# IdentityServer4 中文文档

[TOC]



# 一、背景

------

现代应用程序看上去大都是这样的:

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%B8%80%E3%80%81%E7%AE%80%E4%BB%8B/1%E3%80%81%E6%A6%82%E8%A7%88/%E7%8E%B0%E4%BB%A3%E5%BA%94%E7%94%A8%E7%A8%8B%E5%BA%8F%E7%BD%91%E7%BB%9C%E6%9E%B6%E6%9E%84.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/一、简介/1、概览/现代应用程序网络架构.png)

常见的交互方式包括：

- 浏览器 与 Web应用程序 通信；
- Web应用程序 与 Web API 通信（Web应用程序自身 或 代表用户 与 Web API 通信）；
- 基于浏览器的应用程序 与 Web API 通信；
- 本地应用程序 与 Web API 通信；
- 基于服务器的应用程序 与 Web API 通信；
- Web API 与 Web API 通信（WebAPI自身 或 代表用户与另一个WebAPI 通信）；

将基础安全功能外包给一个安全令牌服务（STS,Security Token Service），能够避免这些应用程序以及端点之间的功能性重复。

重组应用程序以支持一个安全令牌服务，能够导出以下架构和协议：

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%B8%80%E3%80%81%E7%AE%80%E4%BB%8B/1%E3%80%81%E6%A6%82%E8%A7%88/%E5%AE%89%E5%85%A8%E4%BB%A4%E7%89%8C%E6%9C%8D%E5%8A%A1%E4%BD%93%E7%B3%BB%E7%BB%93%E6%9E%84%E5%92%8C%E5%8D%8F%E8%AE%AE.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/一、简介/1、概览/安全令牌服务体系结构和协议.png)

这样的设计把安全问题分成了两个部分：

### 身份认证

当一个应用程序需要知道当前用户的身份（Identity）的时候就要用到身份认证（Authentication）。通常情况下这些应用程序托管着代表该用户的数据，并且必须确保该用户只能访问被允许访问的数据。最常见的例子就是传统的web应用程序 —— 但是本地应用程序和基于JS的应用程序也同样需要身份认证。

最常见的身份认证协议是 SAML2p、WS-Federation 和 OpenID Connect——SAML2p 是最受欢迎的，也是部署得最广泛的。

OpenID Connect 是三种协议中最新的一种，但它却被认为是未来的趋势，因为它对于现代应用程序来说最具潜力。它从一开始就是为移动应用场景而构建的，并且被设计成了友好的API。

### API访问

应用程序有两种基础的方式与API通信 —— 使用应用程序身份，或者使用代表用户的身份。有时候需要联合使用这两种方式。

OAuth2 是一个通信协议，它允许应用程序向安全令牌服务请求访问令牌，然后通过访问令牌与API通信。这同时减少了客户应用程序和API的复杂性，因为认证和授权可以是集中式的。

### OpenID Connect和OAuth2 —— 结合使用更好

OpenID Connect和OAuth2非常相似 —— 实际上前者是后者的顶级扩展。它们把两个基础安全问题（身份认证和 API 访问）合并成了一个单一的协议 —— 通常这只是与安全令牌服务的一个往返交互。

我们坚信，将 OpenID Connect 和 OAuth2 结合以保护现代应用程序，在可预见的未来，肯定会是最佳实践。IdentityServer4 是这两种协议的实现，并且它已经被高度优化以解决当今 移动应用程序、本地应用程序 和 Web应用程序 的典型安全问题。

### IdentityServer4 能做什么？

**IdentityServer4 是一个中间件** ,它能够将符合规范的 OpenID Connect 和 OAuth2.0 端点添加到任意一个 ASP.NET Core 应用程序中。

通常，在你构建（或者复用）一个包含登录和注销页（或者 授权确认页）的应用程序的时候，IdentityServer 中间件会将需要的协议添加到页面头部，这样一来客户端应用程序就能够使用这些标准协议跟它协商了。

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%B8%80%E3%80%81%E7%AE%80%E4%BB%8B/1%E3%80%81%E6%A6%82%E8%A7%88/IdentityServer%E4%B8%AD%E9%97%B4%E4%BB%B6.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/一、简介/1、概览/IdentityServer中间件.png)

你可以根据你的需要使用尽可能复杂的宿主应用程序。但是，为了保持受攻击面尽可能小, 我们一般建议你只将认证相关的UI包含进来。

# 二、相关术语

------

规范、文档和对象模型等都使用特定的术语来表述。

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%B8%80%E3%80%81%E7%AE%80%E4%BB%8B/2%E3%80%81%E7%9B%B8%E5%85%B3%E6%9C%AF%E8%AF%AD/IdentityServer4%E7%9B%B8%E5%85%B3%E6%9C%AF%E8%AF%AD.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/一、简介/2、相关术语/IdentityServer4相关术语.png)

IdentityServer

IdentityServer 是一个 OpenID Connect 提供程序 —— 它实现了OpenID Connect 和 OAuth2 协议。

对于相同的角色，不同的文献将使用不同的术语 —— 你可能也发现了安全令牌服务（Security Token Service），身份提供程序（Identity Provider），授权服务器（Authorization Server），IP-STS 等等。但是他们都具相同的含义：软件中用来向客户端发行安全令牌的部分。

IdentityServer 包含一些职责和功能：

- 保护你的资源
- 使用本地账户存储或外部的身份提供程序来进行用户身份认证
- 提供会话管理和单点登录（Single Sign-on）
- 客户端管理和认证
- 给客户端发行身份令牌和访问令牌
- 验证令牌

### 用户

用户是通过已注册客户端访问相关数据的人。

### 客户端

客户端是软件中从 IdentityServer 请求令牌（Token）的部分 —— 既可以是为了认证一个用户（即请求的是 **身份令牌**），也可以是为了访问一个资源（即请求的是 **访问令牌**）。一个客户端必须首先注册到 IdentityServer 才能请求相关的令牌。

客户端可以是Web应用程序、移动客户端或桌面应用程序、单页面应用程序（SPA，Single Page Application）、服务器进程等等。

### 资源

资源就是你想要通过 IdentityServer 保护的东西 —— 既可以是你的用户的 **身份信息**，也可以是 **API**。

每个资源都有唯一的名称 —— 客户端使用这些名称来指定他们想要访问的资源。

**身份数据（Identity data）** 是一个用户的身份信息（又称为 claims），比如 名字（name） 和 邮箱地址（email address）。

**API** 资源表示的是客户端想要调用的功能 —— 通常通过 Web API 来对 API 资源建模，但这不是必须的。

### 身份令牌

一个身份令牌表示的是认证过程的输出。它最低限度地标识了某个用户（这也可以称为主身份信息的子集，原文：Called the sub aka subject claim），还包含了用户的认证时间和认证方式。身份令牌可以包含额外的身份数据。

### 访问令牌

访问令牌用来授予访问某个 API 资源的权限。客户端请求访问令牌，然后被导向 API。访问令牌包含了客户端和用户（如果提供了的话）的相关信息，API通过这些信息来给它们授予数据访问权限。

# 三、已支持的规范

------

IdentityServer实现了以下规范：

### OpenID连接

- OpenID Connect Core 1.0（[规范](http://openid.net/specs/openid-connect-core-1_0.html)）
- OpenID Connect Discovery 1.0（[规范](http://openid.net/specs/openid-connect-discovery-1_0.html)）
- OpenID Connect会话管理1.0 –草稿22（[规范](http://openid.net/specs/openid-connect-session-1_0.html)）
- 基于HTTP的OpenID Connect HTTP注销1.0 –草稿03（[规范](http://openid.net/specs/openid-connect-logout-1_0.html)）

### OAuth2.0的

- OAuth 2.0（[RFC 6749](http://tools.ietf.org/html/rfc6749)）
- OAuth 2.0承载令牌用法（[RFC 6750](http://tools.ietf.org/html/rfc6750)）
- OAuth 2.0多种响应类型（[规范](http://openid.net/specs/oauth-v2-multiple-response-types-1_0.html)）
- OAuth 2.0表单发布响应模式（[规范](http://openid.net/specs/oauth-v2-form-post-response-mode-1_0.html)）
- OAuth 2.0令牌吊销（[RFC 7009](https://tools.ietf.org/html/rfc7009)）
- OAuth 2.0令牌自省（[RFC 7662](https://tools.ietf.org/html/rfc7662)）
- 代码交换证明密钥（[RFC 7636](https://tools.ietf.org/html/rfc7636)）
- 用于客户端身份验证的JSON Web令牌（[RFC 7523](https://tools.ietf.org/html/rfc7523)）

# 四、打包和合并

------

IdentityServer由一些NuGet包组成。

### IdentityServer4

[nuget](https://www.nuget.org/packages/IdentityServer4/) | [github上](https://github.com/identityserver/IdentityServer4)

核心仅包含对内存配置和用户存储的支持-但是，您可以通过配置的方式插入其他的存储支持。这是其他仓库和程序包相关的内容。

### 快速入门界面

[github上](https://github.com/IdentityServer/IdentityServer4.Quickstart.UI)

包含一个简单的启动器UI，包括登录，替换和授权确认页面。

### 访问令牌验证中间件

[nuget](https://www.nuget.org/packages/IdentityServer4.AccessTokenValidation) | [github上](https://github.com/IdentityServer/IdentityServer4.AccessTokenValidation)

在API中用作验证令牌的ASP.NET Core中间件。提供一个简单的方式来验证访问令牌（包括JWT（JSON Web令牌）和参考）以及实施对范围的要求。

### ASP.NET核心身份

[nuget](https://www.nuget.org/packages/IdentityServer4.AspNetIdentity) | [github上](https://github.com/IdentityServer/IdentityServer4.AspNetIdentity)

ASP.NET Core Identity的IdentityServer集成程序包。该程序包提供了一个简单的配置API来为你的IdentityServer用户使用ASP.NET身份管理库。

### 实体框架核心

[nuget](https://www.nuget.org/packages/IdentityServer4.EntityFramework) | [github上](https://github.com/IdentityServer/IdentityServer4.EntityFramework)

IdentityServer的EntityFramework核心存储实现。该程序包为IdentityServer的配置和操作存储等提供了EntityFramework实现。

### 开发构建

另外，我们将dev / interim的合并发布到了MyGet上面。如果你想要尝试一下，可以添加以下程序包源到你的Visual Studio中：

https://www.myget.org/F/identity/



# 五、支持和咨询选项

------

我们为 IdentityServer 提供了一些免费的、商业性的支持和咨询方案。

### 免费支持

免费支持是以社区和公共论坛的形式提供的。

### StackOverflow

StackOverflow 社区里日益增多的 IdentityServer 用户在监视着上面的问题。如果时间允许，我们也会试着尽可能多地回答这些问题。

你可以使用以下源来订阅所有 IdentityServer4 相关的问题：

https://stackoverflow.com/questions/tagged/?tagnames=identityserver4&sort=newest

你在上面提问的时候记得要使用 `IdentitServer` 标签。

### Gitter

你可以在我们的 Gitter 聊天室里与其他 IdentityServer4 用户聊天交流：

https://gitter.im/IdentityServer/IdentityServer4

### 上报 BUG

如果你认为你已经找到一个 IdentityServer 的 BUG 或者在使用它时遇到了意外的行为，请在 Github [问题追踪](https://github.com/IdentityServer/IdentityServer4/issues) 上开一个问题出来。我们会尽快地回复你。请理解一下，因为我们还有日常工作，并且可能会非常忙，所以可能会无法马上回复你。

你还可以在发布问题之前查看一下[贡献指南](https://github.com/IdentityServer/IdentityServer4/blob/dev/CONTRIBUTING.md)。

### 商业支持

我们正在做身份和访问控制架构方面的咨询，尤其是 IdentityServer。请与我们[取得联系](mailto:identity%40leastprivilege.com)以讨论可能的选项。

#### 培训

我们会定期地召开身份 和 现代应用程序访问控制相关的研讨会。你可以点 [这里](https://identityserver.io/training) 查看日程安排和即将开始的时间。

#### 北美地区的生产支持

略

#### 欧洲的生产支持

略

#### 亚洲的生产支持

没有

### Admin UI, Identity Express and SAML2p support

（管理界面，身份表露 和 SAML2p 支持）

如果你对使用 IdentityServer 的商业支持感兴趣，请查看 https://www.identityserver.com/upcoming-products 。

# 六、示例服务器和测试

------

你可以在你喜欢的客户端库中[尝试](https://demo.identityserver.io/) IdentityServer4。我们在[demo.identityserver.io](https://demo.identityserver.io/)上有一个测试实例，在家里上你可以找到关于如何配置你的客户端和如何调用一个API的介绍。

此外我们还有一个包含大量IdentityServer与网页API组合演练的仓库（IdentityServer 3和4，ASP.NET核心和卡塔纳），我们使用该测试装置来确保所有排列能正常工作。可以你[克隆该仓库](https://github.com/IdentityServer/CrossVersionIntegrationTests)以自行对它进行测试。

# 七、贡献

------

我们对于社区贡献是很开放的，但是你应该遵循一些指导，如此我们才能够比较便捷地处理你的贡献。

### 如何贡献？

最简单的贡献方式就是打开一个问题并且开始讨论。然后我们可以决定一个功能或变更是否可以实现、如何实现。如果你要提交一个有代码变更的拉取请求，那么就从一个描述开始，只做最小的变更，并提供覆盖这些变更的测试就可以了。

你也可以先阅读这个：[成为一名优秀的开源公民](https://hackernoon.com/being-a-good-open-source-citizen-9060d0ab9732#.x3hocgw85)

### 常规反馈和讨论

请在 [核心仓库问题跟踪](https://github.com/IdentityServer/IdentityServer4/issues) 上开启一个讨论。

### 平台

IdentityServer 是针对 ASP.NET Core 1.1.0 使用 Visual Studio 2017 自带的 RTM 工具构建的。这是我们接受的唯一配置。

### BUG 和 功能 请求

请在合适的 Github 仓库上记录新问题：

- [Core（核心）](https://github.com/IdentityServer/IdentityServer4)
- [Samples（示例）](https://github.com/IdentityServer/IdentityServer4.Samples)
- [AccessTokenValidation（访问令牌验证）](https://github.com/IdentityServer/IdentityServer4.AccessTokenValidation)

### 其他讨论

https://gitter.im/IdentityServer/IdentityServer4

### 贡献代码和内容

我们非常欢迎你开始贡献你的项目代码（例如，实现对某数据库的支持，或者实现某种配置存储），记得告诉我们，这样我们才能在我们的文档中链接过去。

我们通常不会要你们贡献的库的所有权，为了支持核心项目，我们已经很忙了。

### 命名惯例

如果你将贡献到 IdentityServer 的库发布为 nuget 程序包，我们希望你不要使用 IdentityServer4 做前缀 —— 你可以将其作为后缀，比如，

建议的命名方式: MyProject.MongoDb.IdentityServer4

不建议的命名方式: IdentityServer4.MongoDb

# 八、设置和概览

------

有两种基础方式可以开始一个新的 IdentityServer 项目：

- 从零开始
- 从 Visual Studio 中的 ASP.NET Identity 模板开始

如果你是从零开始，我们为你提供了一对帮助器和内存存储，所以你无需在一开始就担心持久化问题。

快速入门一步一步地介绍了各种常用的 IdentityServer 场景，它们从抽象基础开始，逐渐复杂 —— 所以建议你按顺序去完成它们。

每个快速入门都有对应的解决方案 —— 你可以在快速入门目录下的 [IdentityServer4.Samples](https://github.com/IdentityServer/IdentityServer4.Samples) 仓库中找到这些代码。

### 基础设置

屏幕快照显示的是 Visual Studio —— 但这不是必须的。

#### 创建快速入门 IdentityServer

从创建一个新的 ASP.NET Core 项目开始。

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%BA%8C%E3%80%81%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/8%E3%80%81%E8%AE%BE%E7%BD%AE%E5%92%8C%E6%A6%82%E8%A7%88/%E5%88%9B%E5%BB%BAASP.NETCore%E9%A1%B9%E7%9B%AE.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/二、快速入门/8、设置和概览/创建ASP.NETCore项目.png)

然后选择 “空” 模板。

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%BA%8C%E3%80%81%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/8%E3%80%81%E8%AE%BE%E7%BD%AE%E5%92%8C%E6%A6%82%E8%A7%88/%E9%80%89%E6%8B%A9%E7%A9%BAASP.NETCore%E9%A1%B9%E7%9B%AE.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/二、快速入门/8、设置和概览/选择空ASP.NETCore项目.png)

> 注意：IdentityServer 目前只支持 ASP.NET Core 1.1

然后是添加 IdentityServer4 的 nuget 程序包。

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%BA%8C%E3%80%81%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/8%E3%80%81%E8%AE%BE%E7%BD%AE%E5%92%8C%E6%A6%82%E8%A7%88/%E6%B7%BB%E5%8A%A0IdentityServer4%E7%9A%84nuget%E7%A8%8B%E5%BA%8F%E5%8C%85.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/二、快速入门/8、设置和概览/添加IdentityServer4的nuget程序包.png)

此外你还可以在 **程序包管理控制台** 中运行以下命令来添加这个依赖：

```
Install-Package IdentityServer4
```

IdentityServer 使用常规的模式来配置和添加服务到 ASP.NET Core 宿主。在 `ConfigureServices` 方法中,必要的服务会被配置和添加到 DI 系统。在 `Configure` 方法中，中间件会被添加到 HTTP 管道中。

像这样修改你的 `Startup.cs` 文件：

```
public class Startup
{
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddIdentityServer()
            .AddTemporarySigningCredential();
    }

    public void Configure(IApplicationBuilder app, ILoggerFactory loggerFactory)
    {
        loggerFactory.AddConsole(LogLevel.Debug);
        app.UseDeveloperExceptionPage();

        app.UseIdentityServer();
    }
}
```

`AddIdentityServer` 会将 IdentityServer 注册到 DI。他还会注册一个基于内存存储的运行时状态，这是对于开发场景来说是很有用的。对于生产环境你就需要像数据库或缓存这些持久化或共享存储部件。查看 [EntityFramework](http://docs.identityserver.io/en/release/quickstarts/8_entity_framework.html#refentityframeworkquickstart) 快速入门可以了解更多这方面的信息。

`AddTemporarySigningCredential` 扩展方法会在每次启动时为签名令牌创建临时的密钥材料。再次说明这对于入门是很有用的，但在生产环境下要用一些持久化密钥材料替换掉它。查看 [密码学文档](http://docs.identityserver.io/en/release/topics/crypto.html#refcrypto) 可了解更多这方面的信息。

> 注意：IdentityServer 还不能够启动。事实上当你尝试启动它时你应该会看到一个异常说缺少服务。我们将在接下来的快速入门中添加这些服务。

### 修改宿主

默认情况下 Visual Studio 使用 IIS Express 来挂载你的 Web 项目。这样做完全没问题，只是你将无法看到输出到控制台的实时日志信息。

IdentityServer 广泛使用了日志，而对于 UI 上可见的或返回给客户端的错误信息则有意模糊。

我们建议在控制台宿主上运行 IdentityServer3。你可以通过切换 Visual Studio 中的启动配置来实现，你甚至都无需在每次运行 IdentityServer 的时候都启动一个浏览器窗口 —— 你也可以用相同的方式关闭它：

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%BA%8C%E3%80%81%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/8%E3%80%81%E8%AE%BE%E7%BD%AE%E5%92%8C%E6%A6%82%E8%A7%88/%E4%BF%AE%E6%94%B9%E5%AE%BF%E4%B8%BB%E9%85%8D%E7%BD%AE.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/二、快速入门/8、设置和概览/修改宿主配置.png)

当你切换到 自托管（self-hosting）的时候，Web 服务器端口默认就是 5000。你既可以通过上面对话框中的启动配置来修改它，也可以以编程的方式在 `Program.cs` 设置它 —— 在快速入门中，我们使用以下配置来设置 IdentityServer 宿主。

```
public class Program
{
    public static void Main(string[] args)
    {
        Console.Title = "IdentityServer";

        var host = new WebHostBuilder()
            .UseKestrel()
            .UseUrls("http://localhost:5000")
            .UseContentRoot(Directory.GetCurrentDirectory())
            .UseIISIntegration()
            .UseStartup<Startup>()
            .Build();

        host.Run();
    }
}
```

> 注意：我们建议将 IIS Express 和 自托管 配置为同一个端口。这样的话你可以自由地在两种模式下切换，无需关心和修改你客户端的任何配置。

### 如何运行快速入门

如前面所说，每个快速入门都会有对应的解决方案 —— 你可以在快速入门目录下的 [IdentityServer4.Samples](https://github.com/IdentityServer/IdentityServer4.Samples) 仓库中找到这些代码。

运行快速入门解决方案的个别部分最简单的方式是设置启动模式为“Current Selection”（当前选中）。右键点击解决方案并选择“设置启动项目”。

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%BA%8C%E3%80%81%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/8%E3%80%81%E8%AE%BE%E7%BD%AE%E5%92%8C%E6%A6%82%E8%A7%88/%E8%BF%90%E8%A1%8C%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/二、快速入门/8、设置和概览/运行快速入门.png)

通常你首先要启动 IdentityServer，然后是 API，然后是 Client。只有在你想要调试的时候才在调试模式下运行，否则 Ctrl+F5 是运行项目的最佳方式。

# 九、使用客户端凭证保护API

------

快速入门展示了使用IdentityServer保护API的最基础的场景。

在这个场景中，我们定义一个API，同时定义一个想要访问该API的客户端。客户端访问IdentityServer请求获得一个访问令牌，然后用这个令牌来获得API的访问权限。

### 定义API

范围（范围）用于定义系统中你想要保护的资源，例如API。

由于当前演练中我们使用的是内存配置-添加一个API，你需要做的只是创建一个`ApiResource`类型的实例，并为它设置合适的属性。

向你的项目中添加一份文件（例如：）`Config.cs`，然后添加如下代码：

```
公共 静态 IEnumerable < ApiResource > GetApiResources（）
{
    返回 新 列表 < ApiResource >
    {
        新的 ApiResource（“ api1 ”，“我的API ”）
    };
}
```

### 定义客户端

下一步是定义能够访问上述API的客户端。

在该场景中，客户端不会有用户参与交互，并且将使用IdentityServer中所谓的客户端密码（客户端密码）来认证。添加如下代码到你的配置中：

```
公共 静态 IEnumerable < Client > GetClients（）
{
    返回 新 列表 < 客户端 >
    {
        新 客户
        {
            ClientId  =  “客户端”，

            //没有交互性用户，使用的clientid /秘密实现认证。
            AllowedGrantTypes  =  GrantTypes。ClientCredentials，

            //用于认证的密码
            ClientSecrets  =
            {
                新的 秘密（“秘密”。SHA256（））
            }，
            //客户端有权访问的范围（Scopes）
            AllowedScopes  = { “ api1 ” }
        }
    };
}
```

### 配置IdentityServer

为了让IdentityServer使用您的范围和客户端定义，您需要向`ConfigureServices`方法中添加一些代码。您可以使用便捷的扩展方法来实现-在幕后会添加相关的存储和数据到DI系统中：

```
公共 无效的 ConfigureServices（IServiceCollection  服务）
{
    //使用内存存储，密钥，客户端和资源来配置身份服务器。
    服务。AddIdentityServer（）
        。AddTemporarySigningCredential（）
        。AddInMemoryApiResources（配置。GetApiResources（））
        。AddInMemoryClients（配置。GetClients（））;
}
```

现在，如果您运行服务器链接浏览器导航到[`http://localhost:5000/.well-known/openid-configuration`](http://localhost:5000/.well-known/openid-configuration)，您应该看能到所谓的**发现文档**。您的客户端和API将使用这些信息来下载所需要的配置数据。

[![img](https://camo.githubusercontent.com/bbf1baade4e7f722f8cafa91094ad2ac21a0ecce/687474703a2f2f696d61676573323031372e636e626c6f67732e636f6d2f626c6f672f3538353532362f3230313730382f3538353532362d32303137303830343031323833383136322d323035383530383336332e706e67)](https://camo.githubusercontent.com/bbf1baade4e7f722f8cafa91094ad2ac21a0ecce/687474703a2f2f696d61676573323031372e636e626c6f67732e636f6d2f626c6f672f3538353532362f3230313730382f3538353532362d32303137303830343031323833383136322d323035383530383336332e706e67)

### 添加API

下一步，向你的解决方案中添加API。

你可以使用ASP.NET Core Web API模板，或者添加`Microsoft.AspNetCore.Mvc`程序包到你的项目中。再一次建议你像之前一样，控制所使用的端口并使用与配置Kestrel和启动资料相同的技术。该演练假设你已经将你的API配置为运行于[`http://localhost:5001`](http://localhost:5001/)之上。

#### 控制器

添加一个新的控制器到你的API项目中：

```
[ 路线（“身份”）]
[ 授权 ]
 公共 类 IdentityController：ControllerBase
{
    [ HttpGet（）]
     公共 IActionResult  Get（）
    {
        返回 新 JsonResult（从 Ç  在 用户。权利要求 选择 新 { Ç。类型，Ç。值 }）;
    }
}
```

这个控制器将在后面被用于测试授权需求，同时通过API的眼睛（浏览工具）来可视化身份信息。

#### 配置

接下来，添加认证中间件到API主机。该中间件的主要工作是：

- 验证输入的令牌以确保它来自可信任的发布者（IdentityServer）;
- 验证令牌是否可用于该api（也就是Scope）。

将*IdentityServer4.AccessTokenValidation*NuGet程序包添加到你的API项目：

[![img](https://camo.githubusercontent.com/02454901a40b50f8d78281dd643a38614153a24d/687474703a2f2f696d61676573323031372e636e626c6f67732e636f6d2f626c6f672f3538353532362f3230313730382f3538353532362d32303137303830343031333032353935392d3235303238313133392e706e67)](https://camo.githubusercontent.com/02454901a40b50f8d78281dd643a38614153a24d/687474703a2f2f696d61676573323031372e636e626c6f67732e636f6d2f626c6f672f3538353532362f3230313730382f3538353532362d32303137303830343031333032353935392d3235303238313133392e706e67)

你还需要添加中间件到你的HTTP管道中-必须在添加MVC之前添加，样式：

```
 公共 无效 配置（IApplicationBuilder  应用程序，IHostingEnvironment  env，ILoggerFactory  loggerFactory）
 {
     loggerFactory。AddConsole（配置。GetSection（“记录”））;
     loggerFactory。AddDebug（）;

     应用程式。UseIdentityServerAuthentication（新的 IdentityServerAuthenticationOptions（）
     {
         Authority  =  “ http：// localhost：5000 ”，
          RequireHttpsMetadata  =  false，
          ApiName  =  “ api1 ”
     }）;

     应用程式。UseMvc（）;
 }
```

如果您使用浏览器导航到上述控制器（[http：// localhost：5001 / identity](http://localhost:5001/identity)），您应该收到返回的`401`状态码。这意味着您的API要求提供证书。

这样一来，API就是受IdentityServer保护的了。

### 创建客户端

最后一个步骤是编写一个客户端来请求访问令牌，然后使用该令牌来访问API。从而您需要为你的解决方案添加一个控制台应用程序。

IdentityServer上的令牌端点实现了`OAuth 2.0`协议，你应该使用合法的HTTP来访问它。然而，我们有一个叫做`IdentityModel`的客户端库，将协议交互封装到了一个易于使用的API里面。

添加*IdentityModel*NuGet程序包到你的客户端项目中。

[![img](https://camo.githubusercontent.com/3cc17f79a682f03a476231775deb0209e644a335/687474703a2f2f696d61676573323031372e636e626c6f67732e636f6d2f626c6f672f3538353532362f3230313730382f3538353532362d32303137303830343031323934323136322d3230393930373233332e706e67)](https://camo.githubusercontent.com/3cc17f79a682f03a476231775deb0209e644a335/687474703a2f2f696d61676573323031372e636e626c6f67732e636f6d2f626c6f672f3538353532362f3230313730382f3538353532362d32303137303830343031323934323136322d3230393930373233332e706e67)

IdentityModel了所有游戏一个用于**发现端点**。的客户端库这样一来你只需要知道IdentityServer的基础地址-实际的端点地址可以从元数据中读取：

```
//从元数据中发现端口
var  disco  =  等待 DiscoveryClient。GetAsync（ “ http：// localhost：5000 ”）;
```

你接着可以使用`TokenClient`类型来请求令牌。为了创建一个该类型的实例，你需要传入令牌端点地址，客户端ID和密码。

然后你可以使用`RequestClientCredentialsAsync`方法来为你的目标API请求一个令牌：

```
//请求以获得令牌
变种 tokenClient  =  新 TokenClient（迪斯科。 TokenEndpoint， “客户端”， “秘密”）;
var  tokenResponse  =  等待 tokenClient。RequestClientCredentialsAsync（ “ API1 ”）;

如果（tokenResponse。ISERROR）
{
    控制台。的WriteLine（tokenResponse。错误）;
    回报 ;
}

控制台。的WriteLine（tokenResponse。的Json）;
```

> 注意：控制台从复制中粘贴状语从句：访问令牌到[jwt.io](https://jwt.io/)以检查令牌的合法性。

最后是调用API。

为了发送访问令牌到API，您通常要使用HTTP授权标头。这可以通过`SetBearerToken`扩展方法来实现：

```
//调用API 
var  client  =  new  HttpClient（）;
客户。SetBearerToken（ tokenResponse。的accessToken）;

var  response  =  等待 客户端。GetAsync（“ http：// localhost：5001 / identity ”）;
如果（！响应。IsSuccessStatusCode）
{
    控制台。的WriteLine（响应。的StatusCode）;
}
其他
{
    var  content  =  等待 响应。内容。ReadAsStringAsync（）;
    控制台。的WriteLine（JArray。解析（内容））;
}
```

最终输出看起来应该是这样的：

[![img](https://camo.githubusercontent.com/219cfcf6318b4c9731fdcbe142a0492560715b9d/687474703a2f2f696d61676573323031372e636e626c6f67732e636f6d2f626c6f672f3538353532362f3230313730382f3538353532362d32303137303830343031333030363331392d3136333931323833382e706e67)](https://camo.githubusercontent.com/219cfcf6318b4c9731fdcbe142a0492560715b9d/687474703a2f2f696d61676573323031372e636e626c6f67732e636f6d2f626c6f672f3538353532362f3230313730382f3538353532362d32303137303830343031333030363331392d3136333931323833382e706e67)

> 注意：各种情况下访问令牌将包含范围身份信息，生命周期（nbf和exp），客户端ID（client_id）和发行者名称（iss）。

### 进一步实践

当前演练目前主要关注的是成功的步骤：

- 客户端可以请求令牌
- 客户端可以使用令牌来访问API

你现在可以尝试引发一些错误来学习系统的相关行为，比如：

- 尝试在IdentityServer未运行时（unavailable）连接它
- 尝试使用一个非法的客户端ID或密码来请求令牌
- 尝试在请求令牌的过程中请求一个非法的范围
- 尝试在API未运行时（不可用）调用它
- 不向API发送令牌
- 配置API为需要有所令牌中的范围

# 十、使用密码保护API

------

**OAuth 2.0 资源所有者密码授权** 允许一个客户端发送用户名和密码到令牌服务并获得一个表示该用户访问令牌。

（OAuth 2.0） **规范** 建议仅对“受信任”的应用程序使用资源所有者密码授权。一般来说，当你想要验证一个用户并请求访问令牌的时候，使用交互式 OpenID Connect 流通常会更好。

不过，这个授权类型允许我们在 IdentityServer 快速入门中引入 **用户** 的概念，这是我们要展示它的原因。

### 添加用户

就像基于内存存储的资源（即 范围 Scopes）和客户端一样，对于用户也可以这样做。

> 注意：查看基于 ASP.NET Identity 的快速入门以获得更多关于如何正确存储和管理用户账户的信息。

`TestUser` 类型表示一个测试用户及其身份信息。让我们向配置类（如果你有严格按照顺序进行演练，那么配置类应该在 QuickstartIdentityServer 项目的 Config.cs 文件中）中添加以下代码以创建一对用户：

首先添加以下 using 语句 到 Config.cs 文件中：

```
public static List<TestUser> GetUsers()
{
    return new List<TestUser>()
    {
        new TestUser
        {
            SubjectId="1",
            Username="爱丽丝",
            Password="password"
        },
        new TestUser
        {
            SubjectId="2",
            Username="博德",
            Password="password"
        }
    };
}
```

然后将测试用户注册到 IdentityServer：

```
public void ConfigureServices(IServiceCollection services)
{
    // 使用内存存储，密钥，客户端和资源来配置身份服务器。
    services.AddIdentityServer()
        .AddTemporarySigningCredential()
        .AddInMemoryApiResources(Config.GetApiResources())
        .AddInMemoryClients(Config.GetClients())
        .AddTestUsers(Config.GetUsers());
}
```

`AddTestUsers` 扩展方法在背后做了以下几件事：

- 为资源所有者密码授权添加支持
- 添加对用户相关服务的支持，这服务通常为登录 UI 所使用（我们将在下一个快速入门中用到登录 UI）
- 为基于测试用户的身份信息服务添加支持（你将在下一个快速入门中学习更多与之相关的东西）

### 为资源所有者密码授权添加一个客户端定义

你可以通过修改 `AllowedGrantTypes` 属性简单地添加对已有客户端授权类型的支持。

通常你会想要为资源所有者用例创建独立的客户端，添加以下代码到你配置中的客户端定义中：

```
public static IEnumerable<Client> GetClients()
{
    return new List<Client>
    {
        // 省略其他客户端定义...

        // 资源所有者密码授权客户端定义
        new Client
        {
            ClientId = "ro.client",

            AllowedGrantTypes = GrantTypes.ResourceOwnerPassword,

            ClientSecrets =
            {
                new Secret("secret".Sha256())
            },
            AllowedScopes = { "api1" }
        }
    };
}
```

### 使用密码授权请求一个令牌

客户端看起来跟之前 **客户端凭证授权** 的客户端是相似的。主要差别在于现在的客户端将会以某种方式收集用户密码，然后在令牌请求期间发送到令牌服务。

IdentityModel 的 `TokenClient` 在这里再次为我们提了供帮助：

```
// 请求以获得令牌
var tokenClient = new TokenClient(disco.TokenEndpoint, "ro.client", "secret");
var tokenResponse = await tokenClient.RequestResourceOwnerPasswordAsync("爱丽丝","password","api1");
if (tokenResponse.IsError)
{
    Console.WriteLine(tokenResponse.Error);
    return;
}
Console.WriteLine(tokenResponse.Json);
Console.WriteLine("\n\n");
```

当你发送令牌到身份 API 端点的时候，你会发现与客户端凭证授权 相比，资源所有者密码授权有一个很小但很重要的区别。访问令牌现在将包含一个 `sub` 信息，该信息是用户的唯一标识。`sub` 信息可以在调用 API 后通过检查内容变量来被查看，并且也将被控制台应用程序显示到屏幕上。

`sub` 信息的存在（或缺失）使得 API 能够区分代表客户端的调用和代表用户的调用。

# 十一、添加基于 OpenID Connect 的用户认证

------

在这个快速启动中，我们希望通过OpenID Connect协议向我们的 IdentityServer 添加对交互式用户身份验证的支持。

完成之后，我们将创建一个使用 IdentityServer 进行身份认证的 MVC 应用程序。

### 添加 UI(用户界面)

IdentityServer 内置了 OpenID Connect 需要的所有协议支持。你需要提供必需的 UI 部分，包括 登录、注销、授权确认以及错误页。

因为在每个 IdentityServer 的实现中，视觉、感觉以及实际工作流可能总是有所不同的，所以我们提供了一套基于 MVC 的样例 UI，你可以将其作为启动点来使用。

这套 UI 可以在 [快速入门仓库](https://github.com/IdentityServer/IdentityServer4.Quickstart.UI/tree/release) 找到。你还可以克隆或下载这个仓库，将其中的控制器、视图、模型以及 CSS 放到你的 Web 应用程序中。

你还可以在你的 Web 应用程序中以命令行的方式运行以下命令来自动下载：

```
iex ((New-Object System.Net.WebClient).DownloadString('https://raw.githubusercontent.com/IdentityServer/IdentityServer4.Quickstart.UI/release/get.ps1'))
```

查看 [自述文件](https://github.com/IdentityServer/IdentityServer4.Quickstart.UI/blob/release/README.md) 以了解更多 快速入门UI 相关的信息。

> 注意： UI 仓库的 `release` 分支拥有与最新发布的稳定版相匹配的 UI。`dev` 分支则与 IdentityServer4 的当前开发构建相符。如果你想要寻找指定版本的 UI，请查看相应的标签。

花一些时间去查阅控制器和模型，你越是了解他们，将来要修改他们就越简单。大部分代码都以“功能目录”的样式放在 “Quickstart” 文件夹下，如果这种样式不适合你，那就按照你想要的方式随意组织代码。

### 创建一个 MVC 客户端

接下来你将向解决方案添加一个 MVC 应用程序，可以使用 ASP.NET Core "Web 应用程序" 模板来实现。 将应用程序配置为使用 5002 端口（可以查看概览部分以了解如何配置）。

为了能向 MVC 应用程序添加 OpenID Connect 认证支持，请添加如下 NuGet 程序包：

- Microsoft.AspNetCore.Authentication.Cookies
- Microsoft.AspNetCore.Authentication.OpenIdConnect

然后添加这两个中间件到你的管道中 —— Cookies 对应的中间件很简单：

```
app.UseCookieAuthentication(new CookieAuthenticationOptions
{
    AuthenticationScheme="Cookies"
});
```

OpenID Connect 中间件需要稍微多一些配置。将它指向 Identity Server，指定一个客户端 ID 并且告诉它哪个中间件将会负责本地登陆（也就是 cookies 中间件）。此外，我们关闭了 JWT 身份信息类型映射，这样就允许 well-known 身份信息（比如，“sub” 和 “idp”） 无干扰地流过。这个身份信息类型映射的 “清理” 必须在调用 `UseOpenIdConnectAuthentication()` 之前完成：

```
JwtSecurityTokenHandler.DefaultInboundClaimTypeMap.Clear();

app.UseOpenIdConnectAuthentication(new OpenIdConnectOptions
{
    AuthenticationScheme = "oidc",
    SignInScheme = "Cookies",
    Authority = "http://localhost:5000",
    RequireHttpsMetadata = false,
    ClientId = "mvc",
    SaveTokens = true
});
```

**两个中间件都应该在 MVC 之前添加到管道。**

下一个步骤是触发认证握手，为此打开 `home` 控制器并添加 `[Authorize]` 到其中一个 `action` 上。另外，修改 action 对应的视图以显示用户的身份信息，比如：

```
<dl>
    @foreach (var claim in User.Claims)
    {
        <dt>@claim.Type</dt>
        <dd>@claim.Value</dd>
    }
</dl>
```

现在，如果你使用浏览器导航到上述控制器，一个Mvc客户端将视图重定向到 IdentityServer - 这会导致错误，因为 MVC 客户端还没有注册（在 IdentityServer 上定义）呢。

### 添加 OpenID Connect 身份 Scopes 支持

与 OAuth 2.0 相似，OpenID Connect 也使用 scopes 这个概念。再一次说明，Scopes 表示你想要保护的和客户端想要访问的事物。在与 OAuth 相比，OIDC(OpenID Connect) 中的 scopes 不仅代表 API，还代表了诸如 用户id、用户名 或 邮箱地址等身份数据。

通过（在 Config.cs 中）添加新的帮助器来创建 `IdentityResource` 对象的集合，可以添加对标准 `openid`（subject id，这里指的是用户id）和 `profile`（姓氏，名称 等等）等 scopes 的支持：

```
public static IEnumerable<IdentityResource> GetIdentityResources()
{
    return new List<IdentityResource>
    {
        new IdentityResources.OpenId(),
        new IdentityResources.Profile(),
    };
}
```

> 注意：所有标准的 Scopes 和他们对应的 身份信息 都可以在 [OpenID Connect 规范](https://openid.net/specs/openid-connect-core-1_0.html#ScopeClaims) 中找到。

接下来在 `Startup.cs` 中你要将这些身份资源添加到你的 IdentityServer 配置。在你调用 `AddIdentityServer()` 的地方使用 `AddInMemoryIdentityResources` 扩展方法即可：

```
public void ConfigureServices(IServiceCollection services)
{
    // 使用内存存储，密钥，客户端和资源来配置身份服务器。
    services.AddIdentityServer()
        .AddTemporarySigningCredential()
        .AddInMemoryApiResources(Config.GetApiResources())
        .AddInMemoryClients(Config.GetClients())
        .AddTestUsers(Config.GetUsers())
        .AddInMemoryIdentityResources(Config.GetIdentityResources());
}
```

### 为 OIDC 隐式流添加客户端定义

最后一个步骤是为 IdentityServer 添加一个新的客户端。

目前，我们添加的基于 OIDC 的客户端与 OAuth 2.0 客户端非常相似。但是由于 OIDC 中的流总是交互式的，所以我们需要添加一些重定向 URL 到我们的配置中。

添加以下代码到你的客户端配置中：

```
public static IEnumerable<Client> GetClients()
{
    return new List<Client>
    {
        // 省略的客户端...

        // OIDC 隐式流客户端（MVC）
        new Client
        {
            ClientId = "mvc",
            ClientName = "Mvc 客户端",
            AllowedGrantTypes = GrantTypes.Implicit,
            // 登录后重定向到的地址
            RedirectUris = { "http://localhost:5002/signin-oidc" },
            // 注销后重定向到的地址
            AllowedScopes = new List<string>
            {
                IdentityServerConstants.StandardScopes.OpenId,
                IdentityServerConstants.StandardScopes.Profile
            }
        }
    };
}
```

### 测试 MVC 客户端

现在，对于新的 MVC 客户端，一切都准备好了。

将浏览器导航到受保护的 控制器 action 以触发认证握手。你应该能看到客户端将你重定向到了 IdentityServer 的登录也。

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%BA%8C%E3%80%81%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/11%E3%80%81%E6%B7%BB%E5%8A%A0%E5%9F%BA%E4%BA%8EOpenIDConnect%E7%9A%84%E7%94%A8%E6%88%B7%E8%AE%A4%E8%AF%81/%E7%99%BB%E5%BD%95%E9%A1%B5%E9%9D%A2.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/二、快速入门/11、添加基于OpenIDConnect的用户认证/登录页面.png)

登录成功后，用户将在授权确认页中被呈现出来。在这里用户可以决定他是否想要发布他的身份信息给客户端应用程序。

> 注意： 授权确认页可以通过客户端定义对象的 `RequireConsent` 属性被关闭（以每个客户端为单位）。

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%BA%8C%E3%80%81%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/11%E3%80%81%E6%B7%BB%E5%8A%A0%E5%9F%BA%E4%BA%8EOpenIDConnect%E7%9A%84%E7%94%A8%E6%88%B7%E8%AE%A4%E8%AF%81/%E6%8E%88%E6%9D%83%E7%A1%AE%E8%AE%A4%E9%A1%B5.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/二、快速入门/11、添加基于OpenIDConnect的用户认证/授权确认页.png)

最终浏览器将被重定向回客户端应用程序，即展示用户的身份信息。

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%BA%8C%E3%80%81%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/11%E3%80%81%E6%B7%BB%E5%8A%A0%E5%9F%BA%E4%BA%8EOpenIDConnect%E7%9A%84%E7%94%A8%E6%88%B7%E8%AE%A4%E8%AF%81/%E5%B1%95%E7%A4%BA%E7%94%A8%E6%88%B7%E8%BA%AB%E4%BB%BD%E4%BF%A1%E6%81%AF.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/二、快速入门/11、添加基于OpenIDConnect的用户认证/展示用户身份信息.png)

> 注意：在开发期间你有时候可能会看到 **无法验证令牌** 的异常信息。这是因为实际上签名密钥材料是凭空产生的，并且在只内存中驻留。这个异常在 客户端 与 IdentityServer 不同步时就会发生。简单地重复客户端上的操作，等到下一次元数据被捕获时，一切都会再次正常工作的。

### 添加注销

最后的最后，是给 MVC 客户端添加 **注销**功能。

通过 IdentityServer 这样的服务进行身份认证，单单清除本地应用程序的 Cookies 是不够的。你还需要往返一次 IdentityServer 来清理集中式单点登录会话。

具体的协议步骤都在 OpenID Connect 中间件中实现了，简单地添加以下代码到某个控制器中就可以用来触发注销：

```
public async Task Logout()
{
    await HttpContext.Authentication.SignOutAsync("Cookies");
    await HttpContext.Authentication.SignOutAsync("oidc");
}
```

### 进一步实验

如前面所说，OpenID Connect 中间件默认会请求 *profile* scope。这个 scope 还包含了用户名或个人主页等身份信息。

让我们将这些身份信息添加到用户定义里面，这样的话 IdentityServer 就可以把它们放到身份令牌中了：

```
public static List<TestUser> GetUsers()
{
    return new List<TestUser>()
    {
        new TestUser
        {
            SubjectId="1",
            Username="爱丽丝",
            Password="password",


            Claims = new []
            {
                new Claim("name", "爱丽丝"),
                new Claim("website", "https://alice.com")
            }
        },
        new TestUser
        {
            SubjectId="2",
            Username="博德",
            Password="password",

            Claims = new []
            {
                new Claim("name", "博德"),
                new Claim("website", "https://bob.com")
            }
        }
    };
}
```

下一次你认证的时候，你的身份信息页将会显示额外的身份信息。

请随意添加更多的身份信息 - 还有更多的 scopes。OpenID Connect 中间件上的 `Scope` 属性是你用来配置哪些 Scopes 将在认证期间被发送到 IdentityServer 的地方。

值得注意的是，对令牌中身份信息的遍历是一个扩展点 - `IProfileService`。因为我们正在使用 `AddTestUser`，所以默认使用的是 `TestUserProfileService`。你可以检出[这里的源代码](https://github.com/IdentityServer/IdentityServer4/blob/dev/src/IdentityServer4/Test/TestUserProfileService.cs)来查看它的工作原理。

# 十二、（快速入门）添加外部认证支持

------

接下来我们将添加外部认证支持。这真的很简单，因为你所需要的实际上只是一个 ASP.NET Core 兼容的认证中间件。

ASP.NET Core 自身已经承载了对 Google，Facebook，Twitter，Microsoft 账户 以及 OpenID Connect 的支持。另外你可以在 [这里](https://github.com/aspnet-contrib/AspNet.Security.OAuth.Providers) 找到更多其他的认证提供程序。

### 添加 Google 支持

为了能够使用 Google 进行身份验证，你首先需要对其进行注册。这应该是在开发人员[控制台](https://console.developers.google.com/)完成的。创建一个新项目，启用 Google+ API 并且通过添加 /signin-google 路径到你的基地址来配置你本地 IdentityServer 的回调地址（比如：http://localhost:5000/signin-google）。

如果你在 5000 端口上运行 IdentityServer - 那么你可以简单地从以下代码片段中使用客户端id/密码，因为这是我们预先注册的。

首先添加 Google 认证中间 NuGet 程序包到你的项目中（`Microsoft.AspNetCore.Authentcation.Google`）

然后我们要将中间件添加到管道中。**顺序很重要，额外的认证中间件必须在 IdentityServer 之后、MVC 之前运行**。

默认情况下我们会在幕后连接一个 cookie 中间件，这样的话外部认证就能够存储它的输出。你只需要将外部认证中间件添加到管道中，并让它使用 `IdentityServerConstants.ExternalCookieAuthenticationScheme` 登录方案：

```
app.UseGoogleAuthentication(new GoogleOptions
{
    AuthenticationScheme = "Google",
    DisplayName = "Google",
    SignInScheme = IdentityServerConstants.ExternalCookieAuthenticationScheme,

    ClientId = "434483408261-55tc8n0cs4ff1fe21ea8df2o443v2iuc.apps.googleusercontent.com",
    ClientSecret = "3gcoTrEDPPJ0ukn_aYYT6PWo"
});
```

> 注意：在 ASP.NET Core Identity 中使用外部认证的时候，`SignInScheme` 必须设置为 `Identity.External`，而不是 `IdentityServerConstants.ExternalCookieAuthenticationScheme`。

现在运行 MVC 客户端，然后尝试进行认证 - 你将在登录页面上看到一个 Google 按钮：

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%BA%8C%E3%80%81%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/12%E3%80%81%E6%B7%BB%E5%8A%A0%E5%A4%96%E9%83%A8%E8%AE%A4%E8%AF%81%E6%94%AF%E6%8C%81/Google%E5%A4%96%E9%83%A8%E8%AE%A4%E8%AF%81.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/二、快速入门/12、添加外部认证支持/Google外部认证.png)

通过认证后，你可以看到现在的身份信息是由 Google 数据提供的了：

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%BA%8C%E3%80%81%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/12%E3%80%81%E6%B7%BB%E5%8A%A0%E5%A4%96%E9%83%A8%E8%AE%A4%E8%AF%81%E6%94%AF%E6%8C%81/Google%E6%8F%90%E4%BE%9B%E7%9A%84%E8%BA%AB%E4%BB%BD%E4%BF%A1%E6%81%AF.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/二、快速入门/12、添加外部认证支持/Google提供的身份信息.png)

### 进一步实验

你可以添加额外的外部认证提供程序。我们有一个云托管的 IdentityServer4 示例版本，你可以通过 OpenID Connect 集成它。

首先添加 *Microsoft.AspNetCore.Authentication.OpenID Connect* Nuget 程序包到你的 IdentityServer 项目中：

![](添加 Microsoft.AspNetCore.Authentication.OpenIdConnect.png)

然后添加对应的中间件：

```
// 外部 OpenId Connect 认证中间件。
app.UseOpenIdConnectAuthentication(new OpenIdConnectOptions
{
    SignInScheme = IdentityServerConstants.ExternalCookieAuthenticationScheme,
    SignOutScheme = IdentityServerConstants.SignoutScheme,
    DisplayName = "开放链接",
    Authority = "https://demo.identiyserver.io/",
    ClientId = "implicit",

    TokenValidationParameters = new TokenValidationParameters
    {
        NameClaimType = "name",
        RoleClaimType = "role"
    }
});
```

> 注意：快速入门 UI 会自动提供外部用户。换句话说，如果一个外部用户第一次登陆进来，就会创建一个本地用户，所有外部身份信息都会被复制过来并与新的本地用户关联。处理这种情况的方法完全取决于你怎么想。也许你会想要首先显示某种用户注册页面。默认的快速入门源代码可以在 [这里](https://github.com/IdentityServer/IdentityServer4/blob/dev/src/Host/Quickstart/Account/AccountService.cs) 找到。

------

在之前的快速入门中我们探讨了 API 访问和用户认证。现在我们想要把这两部分结合起来。

OpenID Connect 和 OAuth 2.0 结合的美妙之处在于，你既可以使用单一的协议，也可以向令牌服务做一次往返交互。

之前我们使用的是 OpenID Connect 隐式流。在隐式流中所有令牌都通过浏览器来传输，这对于 **身份令牌** 来说是完全没有问题的。现在我们还想要请求一个 **访问令牌**。

与身份令牌相比，访问令牌更加敏感，如果没有必要，我们是不会想将他们暴露给“外部世界”的。OpenID Connect 包含了一个叫做 “混合流（Hybrid flowe）” 的流，它为我们提供了两方面优点 —— 身份令牌通过浏览器频道来传输，这样客户端就能够在做任何工作前验证它；如果验证成功了，客户端就会打开一个后端通道来连接令牌服务以检索访问令牌。

### 修改客户端配置

需要修改的东西不是很多。首先我们想要允许客户端使用混合流（Hybrid Flow），另外我们还想要客户端允许服务于服务之间的 API 调用，并且这种调用不会与用户上下文混杂在一起（这与我们的客户端凭证快速入门非常相似）。这是使用 `AllowedGrantTypes` 属性来表示的。

然后我们要添加一个客户端密码，这将被用于在后端通道上检索访问令牌。

最后我们还要允许客户端访问 `offline_access` scope - 这允许为长期使用的 API 访问请求刷新令牌：

```
new Client
{
    ClientId = "mvc",
    ClientName = "MVC 客户端",
    AllowedGrantTypes = GrantTypes.HybridAndClientCredentials,

    ClientSecrets =
    {
        new Secret("secret".Sha256())
    },

    RedirectUris           = { "http://localhost:5002/signin-oidc" },
    PostLogoutRedirectUris = { "http://localhost:5002/signout-callback-oidc" },

    AllowedScopes =
    {
        IdentityServerConstants.StandardScopes.OpenId,
        IdentityServerConstants.StandardScopes.Profile,
        "api1"
    },
    AllowOfflineAccess = true
};
```

### 修改 MVC 客户端

对 MVC 客户端的修改同样也很少 - ASP.NET Core OpenID Connect 中间件是内置支持混合流的，所以我们只需要更改一些配置值。

我们配置 `ClientSecret` 以让它跟 IdentityServer 上的信息相匹配。添加 `offline_access` scopes，然后设置 `ResponseType`为 `code id_token`（基本的意思就是“使用混合流”）

```
app.UseOpenIdConnectAuthentication(new OpenIdConnectOptions
{
    AuthenticationScheme = "oidc",
    SignInScheme = "Cookies",

    Authority = "http://localhost:5000",
    RequireHttpsMetadata = false,

    ClientId = "mvc",
    ClientSecret = "secret",

    ResponseType = "code id_token",
    Scope = { "api1", "offline_access" },

    GetClaimsFromUserInfoEndpoint = true,
    SaveTokens = true
});
```

当你运行 MVC 客户端的时候，不会有太大的区别。除此之外，授权确认页现在还会向你请求访问 额外的 API 和 离线访问（offline access） scope。

### 使用访问令牌

OpenID Connect 中间件会自动为你保存令牌（身份令牌，访问令牌和现在我们例子中的刷新令牌）。这就是 `SaveTokens`设置的效果。

技术上，令牌是存储在 cookie 的属性片段之内的，访问它们最简单的方式是使用 `Microsoft.AspNetCore.Authentication` 名称空间下的扩展方法。

比如在你的身份信息视图上：

```
<dt>access token</dt>
<dd>@await ViewContext.HttpContext.Authentication.GetTokenAsync("access_token")</dd>

<dt>refresh token</dt>
<dd>@await ViewContext.HttpContext.Authentication.GetTokenAsync("refresh_token")</dd>
```

为了使用访问令牌访问 API，你所需要做的只是检索令牌，然后将其设置到你的 *HttpClient* 中：

```
public async Task<IActionResult> CallApiUsingUserAccessToken()
{
    var accessToken = await HttpContext.Authentication.GetTokenAsync("access_token");

    var client = new HttpClient();
    client.SetBearerToken(accessToken);
    var content = await client.GetStringAsync("http://localhost:5001/identity");

    ViewBag.Json = JArray.Parse(content).ToString();
    return View("json");
}
```

# 十三、（快速入门）切换到混合流并添加API访问

------

在之前的快速入门中我们探讨了API访问和用户认证。现在我们想要把这两部分结合起来。

OpenID Connect和OAuth 2.0结合的美妙之处在于，你既可以使用单一的协议，也可以向令牌服务做一次往返交互。

之前我们使用的是OpenID Connect隐式流。在隐式流中所有令牌都通过浏览器来传输，这对于**身份令牌**来说是完全没有问题的。现在我们还想要请求一个**访问令牌**。

与身份令牌类别，访问令牌更加敏感，如果没有必要，我们是不会想将他们暴露给“外部世界”的。OpenIDConnect包含了一个叫做“混合流（Hybrid flowe）”的流，它为我们提供了两方面优点-身份令牌通过浏览器频道来传输，这样客户端就能够在做任何工作前验证它；如果验证成功了，客户端就会打开一个替换通道来连接令牌服务以检索访问令牌。

### 修改客户端配置

需要修改的东西不是很多。首先我们想要允许客户端使用混合流（Hybrid Flow），另外我们还想要客户端允许服务于服务之间的API调用，并且这种调用不会与用户较多的地方一起（这与我们的客户端凭证快速入门非常相似）。的英文这使用`AllowedGrantTypes`属性来表示的。

然后我们要添加一个客户端密码，这将被用于在后端通道上检索访问令牌。

最后我们还要允许客户端访问`offline_access`范围-这允许为长期使用的API访问请求刷新令牌：

```
新 客户
{
    ClientId  =  “ mvc ”，
     ClientName  =  “ MVC客户端”，
     AllowedGrantTypes  =  GrantTypes。HybridAndClientCredentials，

    ClientSecrets  =
    {
        新的 秘密（“秘密”。SHA256（））
    }，

    RedirectUris            = { “ http：// localhost：5002 / signin-oidc ” }，
     PostLogoutRedirectUris  = { “ http：// localhost：5002 / signout-callback-oidc ” }，

    AllowedScopes  =
    {
        IdentityServerConstants。标准范围。OpenId，
         IdentityServerConstants。标准范围。配置文件，
         “ API1 ”
    }，
    AllowOfflineAccess  =  true 
};
```

### 修改MVC客户端

对MVC客户端的修改同样也很少-ASP.NET Core OpenID Connect中间件是内置支持混合流的，所以我们只需要更改一些配置值。

我们配置`ClientSecret`以让它跟IdentityServer上的信息相匹配。添加`offline_access`范围，然后设置`ResponseType`为`code id_token`（基本的意思就是“使用混合流”）

```
应用程式。UseOpenIdConnectAuthentication（新的 OpenIdConnectOptions
{
    AuthenticationScheme  =  “ oidc ”，
     SignInScheme  =  “ Cookies ”，

    Authority  =  “ http：// localhost：5000 ”，
     RequireHttpsMetadata  =  false，

    ClientId  =  “ mvc ”，
     ClientSecret  =  “ secret ”，

    ResponseType  =  “ code id_token ”，
     范围 = { “ api1 ”，“ offline_access ” }，

    GetClaimsFromUserInfoEndpoint  =  true，
     SaveTokens  =  true 
}）;
```

当您运行MVC客户端的时候，不会有太大的区别。此外，授权确认页现在将向您请求访问额外的API和离线访问（offline access）范围。

### 使用访问令牌

OpenID Connect中间件会自动为你保存令牌（身份令牌，访问令牌和现在我们示例中的刷新令牌）。这就是`SaveTokens`设置的效果。

技术上，令牌是存储在cookie的属性片段之内的，访问其最简单的方式是使用`Microsoft.AspNetCore.Authentication`名称空间下的扩展方法。

比如在你的身份信息视图上：

```
< dt > 访问 令牌< / dt > 
< dd > @await  ViewContext。HttpContext。身份验证。GetTokenAsync（“ access_token ”）< / dd >

< dt > 刷新 令牌< / dt > 
< dd > @await  ViewContext。HttpContext。身份验证。GetTokenAsync（“ refresh_token ”）< / dd >
```

为了使用访问令牌访问API，您所需要做的只是检索令牌，然后将其设置到您的*HttpClient*中：

```
公共 异步 任务 < IActionResult > CallApiUsingUserAccessToken（）
{
    var  accessToken  =  等待 HttpContext。身份验证。GetTokenAsync（“ access_token ”）;

    var  client  =  new  HttpClient（）;
    客户。SetBearerToken（accessToken）;
    var  content  =  等待 客户端。GetStringAsync（“ http：// localhost：5001 / identity ”）;

    ViewBag。JSON  =  JArray。解析（内容）。ToString（）;
    返回 View（“ json ”）;
}
```

# 十四、（快速入门）使用 ASP.NET Core Identity

------

IdentityServer 是为灵活性而设计的，其中的表现之一就是，它允许你使用任何你想要用的数据库来存储你的用户以及他们的数据（包括账户密码）。如果你正在从一个全新的用户数据库开始，那么 ASP.NET Identity 是你的选项之一。这个快速入门显示了如何以 IdentityServer 的方式使用 ASP.NET identity。

当前快速入门假设你已经通过了所有之前的快速入门。该快速入门使用 ASP.NET Identity 的方法是从 Visual Studio 中的 ASP.NET Identity 模板创建一个新的项目。新项目将替代之前的快速入门中我们从零开始构建的 IdentityServer 项目。解决方案中的其他所有项目（客户端和API）都将保持不变。

### 用于 ASP.NET Identity 的新项目

第一步是为 ASP.NET Identity 添加一个新项目到你的解决方案中。

考虑到 ASP.NET Identity 需要大量代码，使用 Visual Studio 中的模板会非常有意义。你最终将会删除掉之前旧的 IdentityServer 项目（假设你之前是严格按照快速入门做的），但是你需要将一些项迁移过来（或者跟之前的快速入门一样从零开始重写）。

从创建一个新的 “ASP.NET Core Web 应用程序”项目开始：

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%BA%8C%E3%80%81%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/14%E3%80%81%E4%BD%BF%E7%94%A8ASP.NETCoreIdentity/%E5%88%9B%E5%BB%BAIdentityServerWithAspNetIdentity%E9%A1%B9%E7%9B%AE.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/二、快速入门/14、使用ASP.NETCoreIdentity/创建IdentityServerWithAspNetIdentity项目.png)

然后选择 “Web 应用程序” 选项：

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%BA%8C%E3%80%81%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/14%E3%80%81%E4%BD%BF%E7%94%A8ASP.NETCoreIdentity/%E9%80%89%E6%8B%A9Web%E5%BA%94%E7%94%A8%E7%A8%8B%E5%BA%8F.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/二、快速入门/14、使用ASP.NETCoreIdentity/选择Web应用程序.png)

然后点击“更改身份验证”按钮，选择“个人用户账户”（这意味着使用的是 ASP.NET Identity）：

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%BA%8C%E3%80%81%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/14%E3%80%81%E4%BD%BF%E7%94%A8ASP.NETCoreIdentity/%E6%9B%B4%E6%94%B9%E8%BA%AB%E4%BB%BD%E9%AA%8C%E8%AF%81%E4%B8%BA%E4%B8%AA%E4%BA%BA%E7%94%A8%E6%88%B7%E8%B4%A6%E6%88%B7.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/二、快速入门/14、使用ASP.NETCoreIdentity/更改身份验证为个人用户账户.png)

最后是点击确定以创建项目。

### 修改宿主

别忘了修改宿主（像[之前描述的](http://docs.identityserver.io/en/release/quickstarts/0_overview.html#modify-hosting)一样）以让应用程序运行在 5000 端口上。这对于让已有的客户端和 api 项目能继续工作很重要。

### 添加 IdentityServer 程序包

添加 `IdentityServer4.AspNetIdentity` NuGet 程序包（目前的最新版本是“1.0.1”）。该程序包依赖于 `IdentityServer4` 程序包，所以这些会作为传递依赖被自动添加：

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%BA%8C%E3%80%81%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/14%E3%80%81%E4%BD%BF%E7%94%A8ASP.NETCoreIdentity/%E6%B7%BB%E5%8A%A0IdentityServer4.AspNetIdentity%E7%A8%8B%E5%BA%8F%E5%8C%85.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/二、快速入门/14、使用ASP.NETCoreIdentity/添加IdentityServer4.AspNetIdentity程序包.png)

### Scopes 和 客户端 配置

尽管这是一个 IdentityServer 新项目，但是我们仍然需要与之前快速入门中一样的 Scope 和 客户端 配置。将之前快速入门中的配置类（[Config.cs](https://github.com/IdentityServer/IdentityServer4.Samples/blob/dev/Quickstarts/1_ClientCredentials/src/QuickstartIdentityServer/Config.cs) 文件）复制到现在这个新项目中。

（现在）需要对配置文件做的变更之一是禁用 MVC 客户端的授权确认页。我们还没有将之前 IdentityServer 项目中的授权确认代码拷贝过来，所以现在要对 MVC 客户端进行修改，将 RequireConsent 设置为 false：

```
new Client
{
    ClientId = "mvc",
    ClientName = "MVC 客户端",
    AllowedGrantTypes = GrantTypes.HybridAndClientCredentials,

    RequireConsent = false,

    ClientSecrets =
    {
        new Secret("secret".Sha256())
    },

    RedirectUris           = { "http://localhost:5002/signin-oidc" },
    PostLogoutRedirectUris = { "http://localhost:5002/signout-callback-oidc" },

    AllowedScopes =
    {
        IdentityServerConstants.StandardScopes.OpenId,
        IdentityServerConstants.StandardScopes.Profile,
        "api1"
    },
    AllowOfflineAccess = true
}
```

### 配置 IdentityServer

跟之前一样，IdentityServer 需要在 Startup.cs 的 `ConfigureServices` 和 `Configure` 中进行配置。

#### ConfigureServices

这里同时展示了 ASP.NET Identity 模板生成的代码以及 IdentityServer 需要的额外功能代码（末尾）。在之前的快速入门中，`AddTestUsers` 扩展方法被用来注册用户，但是在现在这个环境中我们将用扩展方法 `AddAspNetIdentity` 替代它，以使用 ASP.NET Identity 用户替代内存用户。 `AddAspNetIdentity` 扩展方法需要一个泛型参数，即你的 ASP.NET 用户类型（与模板中 `AddIdentity` 方法需要用户类型参数一样）。

```
public void ConfigureServices(IServiceCollection services)
{
    services.AddDbContext<ApplicationDbContext>(options =>
        options.UseSqlServer(Configuration.GetConnectionString("DefaultConnection")));

    services.AddIdentity<ApplicationUser, IdentityRole>()
        .AddEntityFrameworkStores<ApplicationDbContext>()
        .AddDefaultTokenProviders();

    services.AddMvc();

    services.AddTransient<IEmailSender, AuthMessageSender>();
    services.AddTransient<ISmsSender, AuthMessageSender>();

    services.AddIdentityServer()
        .AddTemporarySigningCredential()
        .AddInMemoryApiResources(Config.GetApiResources())
        .AddInMemoryClients(Config.GetClients())
        .AddInMemoryIdentityResources(Config.GetIdentityResources())
        .AddAspNetIdentity<ApplicationUser>();
}
```

#### Configure

这里也同时展示了 ASP.NET Identity 模板生成的代码以及 IdentityServer 需要的额外功能代码（紧跟在 `UseIdentity` 之后）。当使用 ASP.NET Identity 时候，IdentityServer 放在 ASP.NET Identity 之后注册到管道是很重要的，因为 IdentityServer 依赖于 ASP.NET Identity 创建和管理的认证Cookie。

```
public void Configure(IApplicationBuilder app, IHostingEnvironment env, ILoggerFactory loggerFactory)
{
    loggerFactory.AddConsole(Configuration.GetSection("Logging"));
    loggerFactory.AddDebug();

    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
        app.UseDatabaseErrorPage();
        app.UseBrowserLink();
    }
    else
    {
        app.UseExceptionHandler("/Home/Error");
    }

    app.UseStaticFiles();

    app.UseIdentity();

    app.UseIdentityServer();

    app.UseMvc(routes =>
    {
        routes.MapRoute(
            name: "default",
            template: "{controller=Home}/{action=Index}/{id?}");
    });
}
```

### 创建用户数据库

因为这是一个新的 ASP.NET Identity 项目，所以你需要创建数据库。你可以在项目目录下运行命令提示符，并运行命令 `dotnet ef database update`，像这样：

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%BA%8C%E3%80%81%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/14%E3%80%81%E4%BD%BF%E7%94%A8ASP.NETCoreIdentity/%E8%BF%90%E8%A1%8C%E6%95%B0%E6%8D%AE%E8%BF%81%E7%A7%BB.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/二、快速入门/14、使用ASP.NETCoreIdentity/运行数据迁移.png)

### 创建用户

现在，你应该能够运行项目并创建/注册用户到数据库了。启动应用程序，然后点击 Home 页面的 “Register” 链接：

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%BA%8C%E3%80%81%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/14%E3%80%81%E4%BD%BF%E7%94%A8ASP.NETCoreIdentity/Home%E9%A1%B5.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/二、快速入门/14、使用ASP.NETCoreIdentity/Home页.png)

在注册页面上创建一个新的用户帐户:

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%BA%8C%E3%80%81%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/14%E3%80%81%E4%BD%BF%E7%94%A8ASP.NETCoreIdentity/%E6%B3%A8%E5%86%8C%E6%96%B0%E7%94%A8%E6%88%B7.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/二、快速入门/14、使用ASP.NETCoreIdentity/注册新用户.png)

那么现在你就有了一个用户账户了，你应该能够登录，使用客户端以及调用 API。

### 登录 MVC 客户端

启动 MVC 客户端应用程序，你应该能够点击 “Secure” 链接来进入登录页：

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%BA%8C%E3%80%81%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/14%E3%80%81%E4%BD%BF%E7%94%A8ASP.NETCoreIdentity/Mvc%E5%AE%A2%E6%88%B7%E7%AB%AF%E9%A6%96%E9%A1%B5.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/二、快速入门/14、使用ASP.NETCoreIdentity/Mvc客户端首页.png)

你应该会被重定向到 ASP.NET Identity 登录页。使用新创建的用户登录：

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%BA%8C%E3%80%81%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/14%E3%80%81%E4%BD%BF%E7%94%A8ASP.NETCoreIdentity/%E7%99%BB%E5%BD%95.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/二、快速入门/14、使用ASP.NETCoreIdentity/登录.png)

登录后，你应该已经直接跳过了授权确认页面（想一下我们之前所做的变更），然后马上就重定向回 MVC 客户端应用程序，随之你的用户身份信息也应该被展示出来：

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%BA%8C%E3%80%81%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/14%E3%80%81%E4%BD%BF%E7%94%A8ASP.NETCoreIdentity/%E7%94%A8%E6%88%B7%E8%BA%AB%E4%BB%BD%E4%BF%A1%E6%81%AF.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/二、快速入门/14、使用ASP.NETCoreIdentity/用户身份信息.png)

点击 “Call Api using application identity”，你应该还能够以用户的身份调用 API：

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%BA%8C%E3%80%81%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/14%E3%80%81%E4%BD%BF%E7%94%A8ASP.NETCoreIdentity/%E4%BB%A5%E7%94%A8%E6%88%B7%E8%BA%AB%E4%BB%BD%E8%B0%83%E7%94%A8API.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/二、快速入门/14、使用ASP.NETCoreIdentity/以用户身份调用API.png)

那么现在你已经是通过 ASP.NET Identity 的用户进行登录的了。

### 接下来做什么？

之前快速入门中的 IdentityServer 项目提供了一个授权确认页面，一个错误页面，以及一个注销页面，现在这些丢失的代码片段可以简单地从先前的快速入门项目中拷贝过来。做完这一步，你就可以将旧的 IdentityServer 项目删掉/清除了。还有，做完这一步后别忘了重新启用 MVC 客户端配置的授权确认页（RequireConsent=true 标记）。

[当前快速入门的样例代码](https://github.com/IdentityServer/IdentityServer4.Samples/tree/dev/Quickstarts/6_AspNetIdentity)已经为你完成了这些步骤，所以你可以快速地开始使用所有这些特性。祝你愉快！

# 十五、（快速入门）添加 JavaScript 客户端

------

该快速入门将展示如何搭建一个 JavaScript 客户端应用程序，其中的用户将登陆到 IdentityServer，使用 IdentityServer 发布的访问令牌调用 Web API，然后从 IdentityServer 注销。

### 新的 JavaScript 客户端项目

创建一个新的 JavaScript 应用程序项目。这可以是一个简单的空的 Web 项目，或者空的 ASP.NET Core 应用程序。这里将使用空的 ASP.NET Core 应用程序。

创建一个新的 ASP.NET Core Web 应用程序：

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%BA%8C%E3%80%81%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/15%E3%80%81%E6%B7%BB%E5%8A%A0JavaScript%E5%AE%A2%E6%88%B7%E7%AB%AF/%E5%88%9B%E5%BB%BA%E7%A9%BA%E7%9A%84ASP.NETCore%E5%BA%94%E7%94%A8%E7%A8%8B%E5%BA%8F.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/二、快速入门/15、添加JavaScript客户端/创建空的ASP.NETCore应用程序.png)

选择 “空” 模板：

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%BA%8C%E3%80%81%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/15%E3%80%81%E6%B7%BB%E5%8A%A0JavaScript%E5%AE%A2%E6%88%B7%E7%AB%AF/%E9%80%89%E6%8B%A9%E2%80%9C%E7%A9%BA%E2%80%9D%E6%A8%A1%E6%9D%BF.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/二、快速入门/15、添加JavaScript客户端/选择“空”模板.png)

点击“确定”按钮以创建项目。

### 修改宿主

修改宿主（像[之前描述的](http://docs.identityserver.io/en/release/quickstarts/0_overview.html#modify-hosting)一样）以让应用程序运行在 5003 端口上。

### 添加静态文件中间件

考虑到该项目主要运行于客户端，我们需要 ASP.NET 提供构成应用程序的静态 HTML 和 JavaScript 文件。静态文件中间件被设计来做这些事。 添加 NuGet 程序包 `Microsoft.AspNetCore.StaticFiles`：

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%BA%8C%E3%80%81%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/15%E3%80%81%E6%B7%BB%E5%8A%A0JavaScript%E5%AE%A2%E6%88%B7%E7%AB%AF/%E6%B7%BB%E5%8A%A0%E9%9D%99%E6%80%81%E6%96%87%E4%BB%B6%E4%B8%AD%E9%97%B4%E4%BB%B6.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/二、快速入门/15、添加JavaScript客户端/添加静态文件中间件.png)

### 注册静态文件中间件

接下来是在 *Startup.cs* 文件的 `Configure` 方法中注册静态文件中间件：

```
public void Configure(IApplicationBuilder app, IHostingEnvironment env, ILoggerFactory loggerFactory)
{
    app.UseDefaultFiles();
    app.UseStaticFiles();
}
```

中间件现在将能够从应用程序的 *~/wwwroot* 目录提供静态文件 —— 这是我们将要放置 Html 和 JavaScript 文件的地方。

### 引用 oidc-client

在 MVC 项目中，我们使用了一个代码库来处理 OpenID Connect 协议。在该项目中我们也需要一个相似的库，只是这个库要在 JavaScript 中工作并且设计运行于浏览器端。[oidc-client 库](https://github.com/IdentityModel/oidc-client-js)就是这样一个库，可以通过 [NPM](https://github.com/IdentityModel/oidc-client-js)，[Bower](https://bower.io/search/?q=oidc-client) 等获取到该库，还可以[直接从 github 下载](https://github.com/IdentityModel/oidc-client-js/tree/master/dist)该库。

#### NPM

如果你想通过 NPM 来下载 *oidc-client* ,可以按照这些步骤来做：

向你的项目中添加一个新的 NPM 程序包定义文件并命名为 *package.json*：

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%BA%8C%E3%80%81%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/15%E3%80%81%E6%B7%BB%E5%8A%A0JavaScript%E5%AE%A2%E6%88%B7%E7%AB%AF/%E4%BD%BF%E7%94%A8NPM%E8%8E%B7%E5%8F%96iodc-client%E5%BA%93.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/二、快速入门/15、添加JavaScript客户端/使用NPM获取iodc-client库.png)

在 *package.json* 文件的 `devDependency` 结点中添加一个 `oidc-client` 引用：

```
"devDependencies": {
  "oidc-client": "1.3.0"
}
```

一旦你保存该文件，Visual Studio 应该会自动还原这些程序包到一个名为 *node_modules* 的目录下：

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%BA%8C%E3%80%81%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/15%E3%80%81%E6%B7%BB%E5%8A%A0JavaScript%E5%AE%A2%E6%88%B7%E7%AB%AF/VS%E8%87%AA%E5%8A%A8%E8%BF%98%E5%8E%9F%E7%9A%84oidc-client%E5%BA%93.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/二、快速入门/15、添加JavaScript客户端/VS自动还原的oidc-client库.png)

在 *~/node_modules/oidc-client/dist* 目录下找到名为 *oidc-client.js* 的文件，并将其复制到应用程序的 *~/wwwroot* 目录。有其他更为复杂的方式可以将你的 NPM 程序包复制到 `~/wwwroot` 目录下，但是这些技术超出了当前快速入门的范围。

### 添加你的 Html 和 JavaScript 文件

接下来是将你的 HTML 和 JavaScript 文件添加到 `~/wwwroot` 目录下。这里涉及到两份 HTML 文件和一份面向具体应用程序的 JavaScript 文件（不同于 *oidc-client.js* 库的文件）。在 *~/wwwroot* 目录下，添加一份名为 *index.html* 和一份名为 *callback.html* 的 HTML 文件，还有一份名为 *app.js* 的 JavaScript 文件。

#### index.html

这将是你应用程序的主页面，它将简单地包含用于用户登录、注销和调用 Web API 的按钮，还将包含引用上述两份 JavaScript 文件的 `<script>` 标签和用于向用户显示消息的 `<pre>` 标签。

它看起来应该是这样的：

```
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title></title>
</head>
<body>
    <button id="login">Login</button>
    <button id="api">Call API</button>
    <button id="logout">Logout</button>

    <pre id="results"></pre>

    <script src="oidc-client.js"></script>
    <script src="app.js"></script>
</body>
</html>
```

#### app.js

该文件将包含我们应用程序的主要代码。首先我们要在里面添加一个帮助器函数来将消息记录到 `<pre>` 标签：

```
function log() {
    var results = document.getElementById('results');
    results.innerText = '';
    Array.prototype.forEach.call(arguments, function (msg) {
        if (msg instanceof Error) {
            msg = "错误：" + msg.message;
        } else if (typeof msg !== 'string') {
            msg = JSON.stringify(msg, null, 2);
        }
        results.innerHTML += msg + '\r\n';
    });
}
```

然后添加代码，为上述三个按钮注册 “click” 事件处理程序：

```
document.getElementById('login').addEventListener('click', login, false);
document.getElementById('api').addEventListener('click', api, false);
document.getElementById('logout').addEventListener('click', logout, false);
```

接着我们可以使用 *oidc-client* 库中的 `UserManager` 类型来管理 OpenID Connect 协议。它要求与 MVC 客户端中需要的相似的配置（虽然其中的值不尽相同）。添加这些代码以配置和初始化 `UserManager`：

```
var config = {
    authority: 'http://localhost:5000',
    client_id: 'js',
    redirect_uri: 'http://localhost:5003/callback.html',
    response_type: 'id_token token',
    scope: 'openid profile api1',
    post_logout_redirect_uri: 'http://localhost:5003/index.html'
};
var manager = new Oidc.UserManager(config);
```

`UserManager` 提供了一个 `getUser` API 来确定用户是否已经登录到 JavaScript 应用程序。其用了一个 JavaScript `Promise`来返回异步结果。返回的 `User` 对象具有一个包含用户身份信息的 `profile` 属性。添加以下代码以检测用户是否已经登录到 JavaScript 应用程序：

```
manager.getUser().then(function (user) {
    if (user) {
        log('用户已登录', user.profile);
    } else {
        log('用户未登录');
    }
});
```

接下来我们要实现 `login`、`api`、`logout` 等方法。`UserManager` 提供了 `signinRedirect` 来登录用户，还提供了 `signoutRedirect` 来注销用户。在上述代码中我们获取到的 `User` 对象还有一个 `access_token` 属性，这可以用来认证到 web API。`access_token` 将通过 *Bearer* 模式的 *Authorization* header 被传递到 web API。添加以下代码以实现我们应用程序中的这三个功能：

```
function login() {
    manager.signinRedirect();
}

function api() {
    manager.getUser().then(function (user) {
        var url = "http://localhost:5001/identity";
        var xhr = new XMLHttpRequest();
        xhr.open("GET", url);
        xhr.onload = function () {
            log(xhr.status, JSON.parse(xhr.responseText));
        }
        xhr.setRequestHeader("Authorization", "Bearer " + user.access_token);
        xhr.send();
    });
}

function logout() {
    manager.signoutRedirect();
}
```

#### callback.html

当用户登录到 IdentityServer 后，该 HTML 文件是指定的 `redirect_uri` 页面，它将完成与 IdentityServer 间 OpenID Connect 协议的登录握手。之前我们使用的 `UserManager` 提供了所有实现这些的代码。一旦登录完成，我们就可以将用户重定向回 index.html 主页面。添加以下代码以完成登录过程：

```
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>登录回调</title>
</head>
<body>
    <script src="scripts/oidc-client.js"></script>
    <script>
        new Oidc.UserManager().signinRedirectCallback().then(function () {
            window.location = 'index.html';
        }).catch(function (e) {
            console.error(e);
        });
    </script>
</body>
</html>
```

### 添加 JavaScript 客户端定义

现在客户端应用程序已经准备好运行了，我们需要在 IdentityServer 中为这个新的 JavaScript 客户端定义一个配置入口。在 IdentityServer 项目中定位到客户端配置（在 *Config.cs* 文件中），然后为我们新的 JavaScript 应用程序向列表中添加新的 *Client* 定义。配置看起来应该是这样的：

```
new Client
{
    ClientId="js",
    ClientName="JavaScript 客户端",
    AllowedGrantTypes = GrantTypes.Implicit,
    AllowAccessTokensViaBrowser=true,

    RedirectUris = { "http://localhost:5003/callback.html" },
    PostLogoutRedirectUris = { "http://localhost:5003/index.html" },
    AllowedCorsOrigins = { "http://localhost:5003" },

    AllowedScopes =
    {
        IdentityServerConstants.StandardScopes.OpenId,
        IdentityServerConstants.StandardScopes.Profile,
        "api1"
    }
}
```

### 允许 Ajax 以 CORS 的方式调用 Web API

最后需要配置的是 web API 项目中的 CORS。这将允许 Ajax 调用从 *http://localhost:5003* 跨越到 *http://localhost:5001* 。

#### CORS NuGet 程序包

添加 `Microsoft.AspNetCore.Cors` NuGet 程序包。

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%BA%8C%E3%80%81%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/15%E3%80%81%E6%B7%BB%E5%8A%A0JavaScript%E5%AE%A2%E6%88%B7%E7%AB%AF/%E6%B7%BB%E5%8A%A0Microsoft.AspNetCore.Cors%E7%A8%8B%E5%BA%8F%E5%8C%85.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/二、快速入门/15、添加JavaScript客户端/添加Microsoft.AspNetCore.Cors程序包.png)

#### 配置 CORS

接着在 *Startup.cs* 文件的`ConfigureServices` 方法中将 CORS 服务添加到依赖注入系统：

```
public void ConfigureServices(IServiceCollection services)
{
    services.AddCors(options =>
    {
        // 这里定义一个 CORS 名为“default”的代理。
        options.AddPolicy("default", policy =>
        {
            policy.WithOrigins("http://localhost:5003")
                .AllowAnyHeader()
                .AllowAnyMethod();
        });
    });

    services.AddMvcCore()
        .AddAuthorization()
        .AddJsonFormatters();
}
```

最后，在 `Configure` 方法中将 CORS 中间件添加到管道：

```
public void Configure(IApplicationBuilder app, IHostingEnvironment env, ILoggerFactory loggerFactory)
{
    loggerFactory.AddConsole(Configuration.GetSection("Logging"));
    loggerFactory.AddDebug();

    app.UseCors("default");

    app.UseIdentityServerAuthentication(new IdentityServerAuthenticationOptions()
    {
        Authority = "http://localhost:5000",
        RequireHttpsMetadata = false,
        ApiName = "api1"
    });

    app.UseMvc();
}
```

### 运行 JavaScript 客户端

现在你应该能够运行 JavaScript 客户端了：

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%BA%8C%E3%80%81%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/15%E3%80%81%E6%B7%BB%E5%8A%A0JavaScript%E5%AE%A2%E6%88%B7%E7%AB%AF/%E8%BF%90%E8%A1%8CJavaScript%E5%AE%A2%E6%88%B7%E7%AB%AF.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/二、快速入门/15、添加JavaScript客户端/运行JavaScript客户端.png)

点击 “登录” 按钮以登录用户。当用户被返回到 JavaScript 应用程序时，你应该能够看到他们的身份信息：

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%BA%8C%E3%80%81%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/15%E3%80%81%E6%B7%BB%E5%8A%A0JavaScript%E5%AE%A2%E6%88%B7%E7%AB%AF/%E7%94%A8%E6%88%B7%E8%BA%AB%E4%BB%BD%E4%BF%A1%E6%81%AF.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/二、快速入门/15、添加JavaScript客户端/用户身份信息.png)

然后点击 “调用 API” 以调用 web API：

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%BA%8C%E3%80%81%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/15%E3%80%81%E6%B7%BB%E5%8A%A0JavaScript%E5%AE%A2%E6%88%B7%E7%AB%AF/%E8%B0%83%E7%94%A8WebAPI.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/二、快速入门/15、添加JavaScript客户端/调用WebAPI.png)

最后点击 “注销” 以注销用户。

你现在已经入门了使用 IdentityServer 进行登录，注销以及认证 Web API 调用的 JavaScript 客户端应用程序。

# 十六、（快速入门）使用EntityFramework Core存储配置数据

------

该快速入门展示了如何配置IdentityServer以使用EntityFramework（EF）作为其数据存储机制（取代目前为止我们一直使用的内存）实现）。

### IdentityServer4.EntityFramework

我们将移动到数据库的数据有两种，第一种是配置数据（资源和客户端客户端定义的数据）。第二种是IdentityServer运行时产生的操作数据。这些存储库都是基于接口建模的，并且我们在*IdentityServer4.EntityFramework*NuGet程序包中为这些接口提供了一套EF实现。

我们从添加*IdentityServer4.EntityFramework*NuGet程序包的引用到IdentityServer项目中开始（请使用“ 1.0.1”以上版本的程序包）：

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%BA%8C%E3%80%81%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/16%E3%80%81%E4%BD%BF%E7%94%A8EntityFrameworkCore%E5%AD%98%E5%82%A8%E9%85%8D%E7%BD%AE%E6%95%B0%E6%8D%AE/%E6%B7%BB%E5%8A%A0IdentityServer4.EntityFramework%E7%A8%8B%E5%BA%8F%E5%8C%85.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/二、快速入门/16、使用EntityFrameworkCore存储配置数据/添加IdentityServer4.EntityFramework程序包.png)

### 添加SqlServer

在该快速入门中我们将使用Visual Studio自带的SqlServer LocalDb版。

为了添加SqlServer，我们需要多一些NeGet程序包。

添加*Microsoft.EntityFrameworkCore.SqlServer*程序包：

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%BA%8C%E3%80%81%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/16%E3%80%81%E4%BD%BF%E7%94%A8EntityFrameworkCore%E5%AD%98%E5%82%A8%E9%85%8D%E7%BD%AE%E6%95%B0%E6%8D%AE/%E6%B7%BB%E5%8A%A0Microsoft.EntityFrameworkCore.SqlServer%E7%A8%8B%E5%BA%8F%E5%8C%85.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/二、快速入门/16、使用EntityFrameworkCore存储配置数据/添加Microsoft.EntityFrameworkCore.SqlServer程序包.png)

添加*Microsoft.EntityFrameworkCore.Tools*程序包：

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%BA%8C%E3%80%81%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/16%E3%80%81%E4%BD%BF%E7%94%A8EntityFrameworkCore%E5%AD%98%E5%82%A8%E9%85%8D%E7%BD%AE%E6%95%B0%E6%8D%AE/%E6%B7%BB%E5%8A%A0Microsoft.EntityFrameworkCore.Tools%E7%A8%8B%E5%BA%8F%E5%8C%85.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/二、快速入门/16、使用EntityFrameworkCore存储配置数据/添加Microsoft.EntityFrameworkCore.Tools程序包.png)

接下来，我们要添加一些命令行工具（更多细节请点击[这里](https://docs.microsoft.com/en-us/ef/core/miscellaneous/cli/dotnet)）-很不幸，您必须通过手动编辑*.csproj*文件来实现这些。您可以在IdentityServer项目上单击鼠标快捷键并选择“编辑QuickstartIdentityServer .csproj的”以手动修改*.csproj的*文件：

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%BA%8C%E3%80%81%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/16%E3%80%81%E4%BD%BF%E7%94%A8EntityFrameworkCore%E5%AD%98%E5%82%A8%E9%85%8D%E7%BD%AE%E6%95%B0%E6%8D%AE/%E9%80%89%E6%8B%A9%E7%BC%96%E8%BE%91IdentityServer%E9%A1%B9%E7%9B%AE%E6%96%87%E4%BB%B6.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/二、快速入门/16、使用EntityFrameworkCore存储配置数据/选择编辑IdentityServer项目文件.png)

然后添加以下片段到元素标签之前：

```
< ItemGroup >
  < DotNetCliToolReference  Include = “ Microsoft.EntityFrameworkCore.Tools.DotNet ” 版本 = “ 1.0.0 ” />
</ ItemGroup >
```

其最终看起来是这样的：

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%BA%8C%E3%80%81%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/16%E3%80%81%E4%BD%BF%E7%94%A8EntityFrameworkCore%E5%AD%98%E5%82%A8%E9%85%8D%E7%BD%AE%E6%95%B0%E6%8D%AE/%E4%BF%AE%E6%94%B9%E5%90%8E%E7%9A%84%E9%A1%B9%E7%9B%AE%E6%96%87%E4%BB%B6.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/二、快速入门/16、使用EntityFrameworkCore存储配置数据/修改后的项目文件.png)

保存并关闭该文件为了验证你已经安装了工具属性，你可以在项目文件目录下打开命令提示符并运行。`dotnet ef`命令运行结果看起来大概是这样的：

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%BA%8C%E3%80%81%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/16%E3%80%81%E4%BD%BF%E7%94%A8EntityFrameworkCore%E5%AD%98%E5%82%A8%E9%85%8D%E7%BD%AE%E6%95%B0%E6%8D%AE/%E9%AA%8C%E8%AF%81%E5%B7%B2%E6%B7%BB%E5%8A%A0EntityFramework%E5%91%BD%E4%BB%A4%E5%B7%A5%E5%85%B7.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/二、快速入门/16、使用EntityFrameworkCore存储配置数据/验证已添加EntityFramework命令工具.png)

### 配置存储

下一个步骤是替换当前在*Startup.cs*的`ConfigureServices`方法中调用的`AddInMemoryClients`，`AddInMemoryIdentityResources`状语从句：`AddInMemoryApiResources`我们将用以下代码替换它们：

```
公共 无效的 ConfigureServices（IServiceCollection  服务）
{
    服务。AddMvc（）;

    var  connectionString  =  @“ server =（localdb）\ mssqllocaldb; database = IdentityServer4.Quickstart.EntityFramework; trusted_connection = yes ” ;
    var  migrationsAssembly  =  typeof（Startup）。GetTypeInfo（）。组装。GetName（）。名称 ;

    //配置使用内存存储用户信息，但使用EF存储客户端和资源信息。
    服务。AddIdentityServer（）
        。AddTemporarySigningCredential（）
        。AddTestUsers（配置。GetUsers（））
        。AddConfigurationStore（助洗剂 => 
            助洗剂。UseSqlServer（的connectionString，选项 => 
                 选项。MigrationsAssembly（migrationsAssembly）））
        。AddOperationalStore（助洗剂 => 
            助洗剂。UseSqlServer（的connectionString，选项 => 
                 选项。MigrationsAssembly（migrationsAssembly）））;
}
```

上述代码将连接字符串直接硬编码到了代码里面，你可以根据需要进行更改。还有，调用`AddConfigurationStore`和`AddOperationalStore`其实是为了将EF的存储实现注册到系统中。

传递给这些API的“构建器”替代函数是EF的机制，这种机制允许您为上述两个存储实现的`DbContext`配置对应的`DbContextOptionsBuilder`-这涉及到您将如何使用数据库提供程序来装配DbContext类型的实例。这里通过调用`UseSqlServer`来使用SqlServer。您也可以看得出来，这里就是提供数据库连接字符串的地方。

`UseSqlServer` 方法中的“ options”是用于配置EF数据迁移定义所在程序集的。EF需要使用数据迁移来为数据库定义相应的架构。

> 注意：定义这些迁移应该是你的宿主应用程序的职责，因为它们是特定于你的数据库及其提供程序。

我们接下来将添加数据迁移。

### 添加数据迁移

为了创建迁移，您需要打开命令合并并定位到IdentityServer项目所在的目录，然后运行以下两个命令：

```
dotnet ef迁移会添加InitialIdentityServerPersistedGrantDbMigration -c PersistedGrantDbContext -o数据/迁移/ IdentityServer / PersistedGrantDb
dotnet ef迁移会添加InitialIdentityServerConfigurationDbMigration -c ConfigurationDbContext -o数据/迁移/ IdentityServer / ConfigurationDb
```

运行结果看起来应该是这样的：

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%BA%8C%E3%80%81%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/16%E3%80%81%E4%BD%BF%E7%94%A8EntityFrameworkCore%E5%AD%98%E5%82%A8%E9%85%8D%E7%BD%AE%E6%95%B0%E6%8D%AE/%E6%B7%BB%E5%8A%A0%E6%95%B0%E6%8D%AE%E8%BF%81%E7%A7%BB.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/二、快速入门/16、使用EntityFrameworkCore存储配置数据/添加数据迁移.png)

### 初始化数据库

现在我们有了数据迁移，我们可以编写代码来从数据迁移创建数据库了。我们还将使用之前的快速入门中定义的内存配置数据作为种子来初始化数据库。

在Startup.cs中添加以下方法来协助初始化数据库：

```
私有 void  InitializeDatabase（IApplicationBuilder  应用程序）
{
    使用（VAR  serviceScope  =  应用。ApplicationServices。GetService的 < IServiceScopeFactory >（）。CreateScope（））
    {
        serviceScope。服务提供者。GetRequiredService < PersistedGrantDbContext >（）。数据库。迁移（）;

        var  context  =  serviceScope。服务提供者。GetRequiredService < ConfigurationDbContext >（）;
        情境。数据库。迁移（）;
        如果（！情境。客户。任何（））
        {
            的foreach（VAR  的客户 中 配置。GetClients（））
            {
                情境。客户端。添加（客户端。ToEntity（））;
            }
            情境。SaveChanges（）;
        }

        如果（！情境。IdentityResources。任何（））
        {
            的foreach（VAR  资源 的 配置。GetIdentityResources（））
            {
                情境。IdentityResources。添加（资源。ToEntity（））;
            }
            情境。SaveChanges（）;
        }

        如果（！情境。ApiResources。任何（））
        {
            的foreach（VAR  资源 的 配置。GetApiResources（））
            {
                情境。ApiResources。添加（资源。ToEntity（））;
            }
            情境。SaveChanges（）;
        }
    }
}
```

在然后`Configure`方法中调用它：

```
公共 无效 配置（IApplicationBuilder  应用程序，IHostingEnvironment  env，ILoggerFactory  loggerFactory）
{
    //人为
    初始化数据库InitializeDatabase（ app）;

    //其他官方的代码
    // ... 
}
```

现在，如果您运行IdentityServer项目，应该会创建数据库并使用之前定义的配置数据初始化它。您应该能够使用SqlServer Management Studio或Visual Studio连接和检查数据：

[![img](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/raw/master/%E4%BA%8C%E3%80%81%E5%BF%AB%E9%80%9F%E5%85%A5%E9%97%A8/16%E3%80%81%E4%BD%BF%E7%94%A8EntityFrameworkCore%E5%AD%98%E5%82%A8%E9%85%8D%E7%BD%AE%E6%95%B0%E6%8D%AE/%E5%B7%B2%E5%88%9B%E5%BB%BA%E5%92%8C%E5%88%9D%E5%A7%8B%E5%8C%96%E7%9A%84%E6%95%B0%E6%8D%AE%E5%BA%93.png)](https://github.com/raochunjiang/IdentityServer4.Docs.zh-Hans/blob/master/二、快速入门/16、使用EntityFrameworkCore存储配置数据/已创建和初始化的数据库.png)

### 运行客户端应用程序

现在你应该能够运行所有现有的客户端应用程序并登陆，获取令牌以及调用API了-这些都是基于数据库配置的。