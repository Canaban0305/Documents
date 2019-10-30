# 将Nginx封装成window服务



需要借助"Windows Service Wrapper"小工具，项目地址： https://github.com/kohsuke/winsw

下载地址：  http://repo.jenkins-ci.org/releases/com/sun/winsw/winsw/2.1.2/winsw-2.1.2-bin.exe

下载该工具后，将其放在 Nginx安装目录下，并重命名为nginx-service.exe，创建配置文件nginx-service.xml（名字要和工具名一样）

nginx-service.xml内容如下：

~~~xml
<configuration>
  <!-- ID of the service. It should be unique accross the Windows system-->
  <id>Nginx</id>
  <!-- Display name of the service -->
  <name>Nginx Service For Web</name>
  <!-- Service description -->
  <description>Nginx静态网站服务，动态网站转发到IIS</description>

  <onfailure action="restart" delay="3 min"/>
  <onfailure action="restart" delay="3 min"/>
  <onfailure action="restart" />
  <resetfailure>1 hour</resetfailure>

  <workingdirectory>C:\Download\nginx-1.16.1</workingdirectory>
  <executable>%BASE%\nginx.exe</executable>
  <arguments></arguments>
  <startarguments></startarguments>

  <stopexecutable>%BASE%\nginx.exe</stopexecutable>
  <stoparguments>-s stop</stoparguments>
  
  <!--
    OPTION: priority
    Desired process priority.
    Possible values: Normal, Idle, High, RealTime, BelowNormal, AboveNormal
    Default value: Normal
  -->
  <priority>Normal</priority>
  <stoptimeout>30 sec</stoptimeout> 
  <startmode>Automatic</startmode>
  <logpath>%BASE%\logs</logpath>
  <log mode="roll-by-time">
      <pattern>yyyyMMdd</pattern>
  </log>
  

</configuration>

~~~

**workingdirectory：**nginx.exe所在目录路径

**logpath：**日记存储位置

**在cmd中运行如下命令安装windows服务**

nginx-service.exe install  #安装Windows服务
nginx-service.exe uninstall  #卸载Windows服务

nginx-service.exe start  #启动Windows服务
nginx-service.exe stop  #停止Windows服务

nginx-service.exe restart #重新启动服务

nginx-servicestatus 检查服务的当前状态



**注意：cmd需要以管理员身份运行 ，否则会报FATAL - WMI Operation failure: AccessDenied,conf文件书写格式需正确，否则服务启动不了，且会报1067错误**