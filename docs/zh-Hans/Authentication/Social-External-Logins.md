# 社交/外部登录

## ASP.NET Core MVC / Razor Pages UI

[帐户模块](../Modules/Account.md)已配置为开箱即用的处理社交或外部登录. 你可以按照ASP.NET Core文档向你的应用程序添加社交/外部登录提供程序.

### 示例: Facebook 认证

按照[ASP.NET Core Facebook集成文档](https://docs.microsoft.com/zh-cn/aspnet/core/security/authentication/social/facebook-logins)向你应用程序添加Facebook登录.

#### 添加NuGet包

添加[Microsoft.AspNetCore.Authentication.Facebook]包到你的项目. 基于你的架构,可能是 `.Web`,`.IdentityServer`(对于分层启动)或 `.Host` 项目.

#### 配置提供程序

在你模块的 `ConfigureServices` 方法中使用 `.AddFacebook(...)` 扩展方法来配置客户端:

````csharp
context.Services.AddAuthentication()
    .AddFacebook(facebook =>
    {
        facebook.AppId = "...";
        facebook.AppSecret = "...";
        facebook.Scope.Add("email");
        facebook.Scope.Add("public_profile");
    });
````

> 最佳实践是使用 `appsettings.json` 或ASP.NET Core用户机密系统来存储你的凭据,而不是像这样硬编码值. 请参阅[微软](https://docs.microsoft.com/en-us/aspnet/core/security/authentication/social/facebook-logins)文档了解如何使用用户机密.