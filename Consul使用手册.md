<<<<<<< HEAD
# **Consul使用手册**
=======
## **Consul使用手册**
>>>>>>> 2be3329345bcf49fc7a22d3bde8c80a5f9bf963c



[TOC]



#### [Api官方文档地址][https://www.consul.io/api/index.html]

#### [下载地址][https://www.consul.io/downloads.html]

![img](https://github.com/Canaban0305/Documents/blob/master/Images/Consul-1.jpg?raw=true) 

#### 设置系统环境变量

添加 计算机 右键 属性 高级属性设置环境变量设置（选择Consul程序路径）![img](https://github.com/Canaban0305/Documents/blob/master/Images/Consul-2.jpg?raw=true) 



![img](https://github.com/Canaban0305/Documents/blob/master/Images/Consul-3.png?raw=true) 

#### cmd运行

consul agent -dev

![img](https://github.com/Canaban0305/Documents/blob/master/Images/Consul-4.png?raw=true) 

 

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

![img](https://github.com/Canaban0305/Documents/blob/master/Images/Consul-5.png?raw=true) 

#### ****到Consul上查看

http://localhost:8500

![img](https://github.com/Canaban0305/Documents/blob/master/Images/Consul-6.png?raw=true) 

![img](https://github.com/Canaban0305/Documents/blob/master/Images/Consul-7.png?raw=true) 

![img](https://github.com/Canaban0305/Documents/blob/master/Images/Consul-7_2.png?raw=true) 

 

#### 查看微服务上所有注册程序

http://localhost:8500/v1/agent/services

![img](https://github.com/Canaban0305/Documents/blob/master/Images/Consul-8.png?raw=true) 

#### 根据服务id获取该服务信息

http://localhost:8500/v1/agent/service/服务id

![img](https://github.com/Canaban0305/Documents/blob/master/Images/Consul-9.png?raw=true) 

 

#### ****获得当地服务健康****



#### 手动注册Consul

http://localhost:8500/v1/agent/service/register

![img](https://github.com/Canaban0305/Documents/blob/master/Images/Consul-10.jpg?raw=true) 





