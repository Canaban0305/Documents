### NLog配置文件

```config
<?xml version="1.0" encoding="utf-8" ?>
<nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

  <targets async="true">
    <target name="loginfofile" xsi:type="File" fileName="Log/Info/${shortdate}.txt" layout="${longdate}  【Level】：${level}  【message】：${message}" />
    <target name="logerrorfile" xsi:type="File" fileName="Log/Error/${shortdate}.txt" layout="${longdate}  【Level】：${level}  【ClssName】：${callsite:className=True:fileName=True}  【message】：${message}" />
  </targets>

  <rules>
    <logger name="*" minlevel="Info" writeTo="loginfofile" />
    <logger name="*" minlevel="Error" writeTo="logerrorfile" />
  </rules>
</nlog>
```

