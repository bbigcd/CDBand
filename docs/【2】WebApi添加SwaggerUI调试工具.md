#### 从0开始搭建netcore+vue前后端开发框架之WebApi添加SwaggerUI调试工具

[参考地址](https://docs.microsoft.com/zh-cn/aspnet/core/tutorials/getting-started-with-swashbuckle?view=aspnetcore-2.2&tabs=visual-studio)

##### 添加 NuGet 包

```shell
dotnet add package Swashbuckle.AspNetCore --version 4.0.1
```

如果不指定版本号，将自动安装最新的版本。

最新的版本还在rc阶段（2019年08月01日），所以这里指定最新的稳定版本 4.0.1

添加时，需进入CDBand.WebApi目录中，然后在终端中运行上面的命令

添加成功后，在 `CDBand.WebApi.csproj` 中看到如下的代码，即表示添加成

```csharp
<PackageReference Include="Swashbuckle.AspNetCore" Version="4.0.1" />
```

##### 添加中间件

在 Startup.cs 文件中的 `ConfigureServices` 方法添加如下配置:

```c#
services.AddSwaggerGen(options =>
{
    options.SwaggerDoc("v1", new Info { Title = "系统后端Api文档", Version = "v1" });
});
```

其中 Info 需添加引用 `using Swashbuckle.AspNetCore.Swagger;`

在 `Configure` 方法中添加中间件

```c#
// 添加中间件
app.UseSwagger();
// 添加中间件的UI
app.UseSwaggerUI(options =>
{
    options.SwaggerEndpoint("/swagger/v1/swagger.json", "My API V1");
    options.RoutePrefix = string.Empty;
});
```

##### 运行结果

执行 `dotnet run` 在浏览器中访问默认的路径，看到下方图片所示，即配置成功

![结果](https://github.com/bbigcd/CDBand/blob/master/images/Api%E6%96%87%E6%A1%A31.png?raw=true)