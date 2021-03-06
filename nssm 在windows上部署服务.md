# nssm 在windows上部署服务

## 简介

　　[NSSM](http://www.nssm.cc/)是一款可将Nodejs项目注册为Windows系统服务的工具。当你的Node.js项目需要部署在Windows Server上时，NSSM是一个不错的选择。

## 特点

　　[NSSM](http://www.nssm.cc/)将Node.js项目注册为服务后，启动、停止、重启皆由windows来管理，所以我们不必担心NSSM无法处理项目因意外的停止，而Windows的服务管理即可处理这些问题。

## 使用

1.下载NSSM    [download](http://www.nssm.cc/release/nssm-2.24.zip).
2.根据自己的平台，将32/64位nssm.exe文件解压至任意文件夹。
3.cmd定位至nssm.exe所在目录。
4.输入 `nssm.exe install`，即注册服务的名称。注册服务弹出如下NSSM界面。

![img](https://images2018.cnblogs.com/blog/1207100/201803/1207100-20180329160115318-512703640.png)

 

![img](https://segmentfault.com/img/bV1hvC?w=435&h=234)

5.Application标签设置：

- Application Path: 选择系统安装的node.exe(dotnet.exe)。-一般在`C:\Program Files\dotnet`下
- Startup directory: 选择需要封装的项目的根目录。
- Arguments: 启动的exe文件或者dll文件
- Service name：window 服务名称
- Detail：描述

6.上述步骤操作完成，即可点击Install service来注册服务。我们在系统的服务中即可找到刚刚注册的服务。
7.在系统服务中找到刚刚注册的服务，右键`属性 - 恢复`即可设置此服务挂掉重启等内容。

 

nssm常用命令：

nssm install servername //创建servername服务

nssm start servername //启动服务

nssm stop servername //暂停服务

nssm restart servername //重新启动服务

nssm remove servername //删除创建的servername服务