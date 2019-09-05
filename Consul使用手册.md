## **Consul使用手册**



[TOC]



#### [Api官方文档地址][https://www.consul.io/api/index.html]

#### [下载地址][https://www.consul.io/downloads.html]

![img](file:///C:\Users\ADMINI~1\AppData\Local\Temp\ksohtml23532\wps1.jpg) 

#### ****设置系统环境变量：添加 计算机 右键 属性 高级属性设置环境变量设置

![img](file:///C:\Users\ADMINI~1\AppData\Local\Temp\ksohtml23532\wps2.jpg) 



![img](file:///C:\Users\ADMINI~1\AppData\Local\Temp\ksohtml23532\wps3.jpg) 

#### ****cmd运行：****consul agent -dev

![img](file:///C:\Users\ADMINI~1\AppData\Local\Temp\ksohtml23532\wps4.jpg) 

 

#### ****在程序里注册Consul微服务

- ##### 构建注册方法：

~~~c#
Public static void Register()
{

	Var consulClient = new ConsulClient(x => x.Address = new Uri(http://localhost:8500));	//请求注册的Consul地址

	Var httpCheck = new AgentServiceCheck()
	{
        DeregisterCriticalServiceAfter = TimeSpan.FromSeconds(5),		//服务启动多久后注册
        Interval = TimeSpan.FromSeconds(10),	//健康检查时间间隔，或者称之为心跳间隔
        HTTP = $“{ip}:{port}/api/health”,	//健康检查地址
        Timeout = TimeSpan.FromSeconds(5)
	};

	Var registration = new AgentServiceRegistration()
	{
        Check = new[] {httpCheck},
        ID = Guid.NewGuid.ToString(),	//服务id
        Name = “Test”,	//服务名称
        Address = ip,	//服务IP地址
        Port = port,	 //端口号
        Tags = new[]{$”urlprefix-/Test”}
	};

	consulClient.Agent.ServiceRegister(registration);
}

~~~



- ##### 在Startup的Configure里运行该方法

![img](file:///C:\Users\ADMINI~1\AppData\Local\Temp\ksohtml23532\wps5.jpg) 

#### ****到Consul上查看

![img](file:///C:\Users\ADMINI~1\AppData\Local\Temp\ksohtml23532\wps6.jpg) 

![img](file:///C:\Users\ADMINI~1\AppData\Local\Temp\ksohtml23532\wps7.jpg) 

 

#### ****查看微服务上所有注册程序：**[**http://localhost:8500/v1/agent/services]

![img](file:///C:\Users\ADMINI~1\AppData\Local\Temp\ksohtml23532\wps8.jpg) 

#### ****根据服务id获取该服务信息：**[**http://localhost:8500/v1/agent/service/****服务id]

![img](file:///C:\Users\ADMINI~1\AppData\Local\Temp\ksohtml23532\wps9.jpg) 

 

#### ****获得当地服务健康****



#### ****手动注册Consul：http://localhost:8500/v1/agent/service/register

![img](file:///C:\Users\ADMINI~1\AppData\Local\Temp\ksohtml23532\wps10.jpg) 