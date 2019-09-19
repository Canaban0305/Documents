# C#依赖注入

### 1、在Program.cs文件中添加注入

~~~C#
using System;
using Microsoft.Extensions.DependencyInjection;
using BeetleX.FastHttpApi.Hosting;
using Microsoft.Extensions.Hosting;
using BeetleX.FastHttpApi;
using Microsoft.Extensions.Configuration;
using NLog;
using AN1.ClientSync.WebAPI.Utility;
//using AN1.ClientSync.WebAPI.Model;
//using SqlSugar;
using System.Collections.Generic;
using AN1.ClientSync.WebAPI.Service;
using Mapster;
using AN1.ClientSync.WebAPI.Model;
using AN1.ClientSync.WebAPI.Model.Mapster;
using Consul;
using AN1.ClientSync.WebAPI.Common;

namespace AN1.ClientSync.WebAPI
{
    class Program
    {
        static void Main(string[] args)
        {        
            var builder = new HostBuilder()
                .ConfigureAppConfiguration((hostingContext, config) =>
                {
                    config.AddJsonFile("appsettings.json", optional: true, 				reloadOnChange: false);
                })
                .ConfigureServices((hostingContext, services) =>
                {
                    services
                    .AddSingleton<DemoService>()
                    .UseBeetlexHttp(o =>
                    {
                        o.Port = int.Parse(hostingContext.Configuration["HttpConfig:Port"]);
                        o.LogToConsole = true;
                        o.LogLevel = BeetleX.EventArgs.LogType.Debug;
                        o.SetDebug();
                    }, typeof(Program).Assembly);

                });
            builder.Build().Run();
        }
    }
}

~~~



**添加引用：**

> using Microsoft.Extensions.DependencyInjection;
> using BeetleX.FastHttpApi.Hosting;
> using Microsoft.Extensions.Hosting;
> using BeetleX.FastHttpApi;



**config.AddJsonFile("appsettings.json", optional: true, reloadOnChange: false);注入appsettings文件**

~~~appsettings.json
{
  "ConnectionStrings": {
    "default": "server=192.168.10.79;port=3306;database=an1_clientsync;user id=root;pwd=An1#24;Charset=utf8mb4;"
  },
  "HttpConfig": {
    "Port": 8080
  },
  "AppSettings": {
    "DBProvider": "MySql",
    "DBConnection": "default",
    "ConsulServerUrl": "http://192.168.10.79:8500",
    "ConsulServiceName": "cananban",
    "ConsulServiceHttpCheck": "http://192.168.10.192",
    "ConsulServiceAddress": "192.168.10.192",
    "ConsulServicePort": "8080"
  }
}

~~~



**.AddSingleton<DemoService>()**

注入DemoService实体类

~~~DemoService
using System;
using System.Collections.Generic;
using System.Text;

namespace AN1.ClientSync.WebAPI.Utility
{
    public class DemoService
    {

        public bool Login(string name, string pwd)
        {
            return name == "admin" && pwd == "123456";
        }

    }
}
~~~

**int.Parse(hostingContext.Configuration["HttpConfig:Port"]);端口号**

### 2、应用

**home_demo**

~~~home_demo
using AN1.ClientSync.WebAPI.Utility;
using BeetleX.FastHttpApi;
using Microsoft.Extensions.Configuration;
using System;
using System.Collections.Generic;
using System.Text;

namespace AN1.ClientSync.WebAPI.Controller
{
    [Controller(BaseUrl = "home")]
    public class Home_demo :BaseDemo
    {

        public Home_demo(HttpApiServer server, DemoService userService, IConfiguration config)
        {
            mHttpApiServer = server;
            mUserService = userService;
            mconfig = config;
            this.GetDB();
        }

        private DemoService mUserService;

        private HttpApiServer mHttpApiServer;

      

        [Get(Route = "{school}")]
        public JsonResult Hello22(string school)
        {
            return new JsonResult($"not log in{school}");
        }
        [Get(Route = "{school}")]
        public JsonResult Hello(string school,string name,string password)
        {
            if(mUserService.Login(name, password)){
                return new JsonResult( $"hello {school}{name}, Connection {mconfig.GetConnectionString("default")}");
            }
            else
            {
                return new JsonResult($"not log in{school}");
            }
           
        }
         
        public JsonResult HelloPost(string name, string password, IHttpContext con)
        {
         
            //db.Queryable
            if (mUserService.Login(name, password))
            {
                return new JsonResult($"hello {name}, Connection {mconfig.GetConnectionString("default")}");
            }
            else
            {
                return new JsonResult($"not log in");
            }

        }
    }
}

~~~

