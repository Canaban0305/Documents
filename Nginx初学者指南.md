## 初学者指南



本指南对nginx进行了基本介绍，并描述了一些可以使用它完成的简单任务。假设已经在阅读器的计算机上安装了nginx。如果不是，请参阅“ [安装nginx”](http://nginx.org/en/docs/install.html)页面。本指南描述了如何启动和停止nginx以及重新加载其配置，解释了配置文件的结构，并描述了如何设置nginx以提供静态内容，如何将nginx配置为代理服务器以及如何将其与FastCGI应用程序。

nginx有一个主进程和几个工作进程。主流程的主要目的是读取和评估配置，以及维护工作流程。工作进程对请求进行实际处理。nginx使用基于事件的模型和依赖于操作系统的机制来有效地在工作进程之间分配请求。工作进程的数量在配置文件中定义，可以针对给定的配置固定，也可以自动调整为可用CPU内核的数量（请参阅[worker_processes](http://nginx.org/en/docs/ngx_core_module.html#worker_processes)）。

nginx及其模块的工作方式在配置文件中确定。默认情况下，该配置文件被命名`nginx.conf` ，并放入目录`/usr/local/nginx/conf`， `/etc/nginx`或 `/usr/local/etc/nginx`。



### 启动，停止和重新加载配置

要启动nginx，请运行可执行文件。一旦启动nginx，就可以通过使用`-s`参数调用可执行文件来对其进行控制。使用以下语法：

> ```
> nginx -s signal
> ```

其中*信号*可能是以下之一：

- `stop` —快速关机
- `quit` —正常关机
- `reload` —重新加载配置文件
- `reopen` —重新打开日志文件

例如，要在等待工作进程完成对当前请求的服务的过程中停止nginx进程，可以执行以下命令：

> ```
> nginx -s quit
> ```



> 此命令应在启动nginx的同一用户下执行。



在重新加载配置的命令发送到nginx或重新启动它之前，不会应用对配置文件所做的更改。要重新加载配置，请执行：

> ```
> nginx -s reload
> ```



一旦主进程接收到重新加载配置的信号，它将检查新配置文件的语法有效性，并尝试应用其中提供的配置。如果成功，则主进程将启动新的工作进程，并将消息发送到旧的工作进程，要求它们关闭。否则，主进程将回滚所做的更改，并继续使用旧配置。旧的工作进程接收到关闭命令，停止接受新的连接并继续为当前请求提供服务，直到为所有此类请求提供服务为止。之后，旧的工作进程退出。

也可以借助Unix工具（如`kill`实用程序）将信号发送到nginx进程。在这种情况下，将信号直接发送给具有给定进程ID的进程。默认情况下，nginx主进程的进程ID写入 `nginx.pid`目录 `/usr/local/nginx/logs`或中的 `/var/run`。例如，如果主进程ID为1628，要发送导致NGINX正常关闭的QUIT信号，请执行：

> ```
> kill -s QUIT 1628
> ```

为了获取所有正在运行的nginx进程的列表，`ps` 可以使用该实用程序，例如，通过以下方式使用：

> ```
> ps -ax | grep nginx
> ```

有关将信号发送到nginx的更多信息，请参见 [控制nginx](http://nginx.org/en/docs/control.html)。



### 配置文件的结构

nginx由受配置文件中指定的指令控制的模块组成。伪指令分为简单伪指令和块伪指令。一个简单的指令由名称和参数组成，这些名称和参数之间用空格分隔，并以分号（`;`）结尾。块指令的结构与简单指令的结构相同，但是它以分号（而不是分号）结尾，并带有一组用括号（`{`和`}`）括起来的附加指令。如果块指令在花括号内可以有其他指令，则称为上下文（示例： [events](http://nginx.org/en/docs/ngx_core_module.html#events)， [http](http://nginx.org/en/docs/http/ngx_http_core_module.html#http)， [server](http://nginx.org/en/docs/http/ngx_http_core_module.html#server)和 [location](http://nginx.org/en/docs/http/ngx_http_core_module.html#location)）。

放置在任何上下文外部的配置文件中的指令都被视为在 [主](http://nginx.org/en/docs/ngx_core_module.html)上下文中。在`events`和`http`指令驻留在`main`上下文`server`中`http`，并`location`在 `server`。

`#`符号 后的其余行被视为注释。



提供静态内容

Web服务器的一项重要任务是分发文件（例如图像或静态HTML页面）。您将实现一个示例，其中根据请求，文件将从不同的本地目录提供：（`/data/www` 可能包含HTML文件）和`/data/images` （包含图像）。这将需要编辑配置文件，并 在 带有两个[位置](http://nginx.org/en/docs/http/ngx_http_core_module.html#location) 块的[http](http://nginx.org/en/docs/http/ngx_http_core_module.html#http)块内设置 [服务器](http://nginx.org/en/docs/http/ngx_http_core_module.html#server)块。

首先，创建`/data/www`目录并在其中放置`index.html`包含任何文本内容的 文件，然后创建`/data/images`目录并在其中放置一些图像。

接下来，打开配置文件。默认配置文件已经包含该`server`块的几个示例，大部分已被注释掉。现在注释掉所有这样的块并开始一个新 `server`块：

> ```
> http {
>     server {
>     }
> }
> ```

通常，配置文件可以包括几个`server`块，这些 块 通过它们[侦听](http://nginx.org/en/docs/http/ngx_http_core_module.html#listen)的端口和[服务器名称](http://nginx.org/en/docs/http/server_names.html)来 [区分](http://nginx.org/en/docs/http/request_processing.html)。一旦nginx决定了哪个处理请求，它就会根据块内定义的指令 的参数测试在请求标头中指定的URI 。 `server``location``server`

将以下`location`块添加到该 `server`块：

> ```
> location / {
>     root /data/www;
> }
> ```

与请求中的URI相比， 此`location`块指定“ `/`”前缀。对于匹配的请求，会将URI添加到[root](http://nginx.org/en/docs/http/ngx_http_core_module.html#root) 指令中指定的路径，即添加到`/data/www`，以形成本地文件系统上所请求文件的路径。如果有多个匹配的`location`块，nginx将选择前缀最长的块。`location`上面的块提供了最短的前缀（长度为1），因此只有在所有其他`location` 块均未提供匹配项时，才会使用该块。

接下来，添加第二个`location`块：

> ```
> location /images/ {
>     root /data;
> }
> ```

这将匹配以开头的请求`/images/` （`location /`也匹配此类请求，但前缀较短）。

`server`块 的最终配置应如下所示：

> ```
> server {
>     location / {
>         root /data/www;
>     }
> 
>     location /images/ {
>         root /data;
>     }
> }
> ```

这已经是服务器的工作配置，可以在标准端口80上侦听，并且可以在本地计算机上访问 `http://localhost/`。响应以开头的URI请求`/images/`，服务器将从`/data/images`目录中发送文件。例如，响应`http://localhost/images/example.png`请求，nginx将发送`/data/images/example.png`文件。如果该文件不存在，nginx将发送一个指示404错误的响应。URI不以开头的请求`/images/`将被映射到`/data/www`目录中。例如，响应`http://localhost/some/example.html`请求，nginx将发送`/data/www/some/example.html`文件。

要应用新配置，请启动尚未启动`reload`的nginx，或通过执行以下命令将信号发送到nginx的主进程：

> ```
> nginx -s reload
> ```





> 万一某些功能无法正常工作，您可以尝试在目录或中 查找原因`access.log`和 `error.log`文件 。`/usr/local/nginx/logs``/var/log/nginx`





### 设置简单的代理服务器

nginx的一种常用用法是将其设置为代理服务器，这意味着服务器可以接收请求，将请求传递给代理服务器，从请求中检索响应并将它们发送给客户端。

我们将配置一个基本的代理服务器，该服务器为图像请求和本地目录中的文件提供服务，并将所有其他请求发送到代理服务器。在此示例中，两个服务器都将在单个nginx实例上定义。

首先，通过向`server` nginx的配置文件添加一个以下内容来定义代理服务器：

> ```
> server {
>     listen 8080;
>     root /data/up1;
> 
>     location / {
>     }
> }
> ```

这将是一个简单的服务器，它侦听端口8080（以前，`listen`自从使用标准端口80以来就未指定该指令），并将所有请求映射到`/data/up1`本地文件系统上的目录。创建此目录并将`index.html`文件放入其中。请注意，该`root`指令位于 `server`上下文中。这样`root`，当用于指令 `location`选择用于服务请求中不包含自己的块`root`指令。

接下来，使用上一部分中的服务器配置并对其进行修改以使其成为代理服务器配置。在第一个`location`块中，将[proxy_pass](http://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_pass) 指令与参数中指定的代理服务器的协议，名称和端口（在本例中为`http://localhost:8080`）放置在一起：

> ```
> server {
>     location / {
>         proxy_pass http://localhost:8080;
>     }
> 
>     location /images/ {
>         root /data;
>     }
> }
> ```



我们将修改第二个`location` 块，该块当前将带有`/images/` 前缀的请求映射到目录下的`/data/images`文件，以使其与具有典型文件扩展名的图像的请求匹配。修改后的`location`块如下所示：

> ```
> location ~ \.(gif|jpg|png)$ {
>     root /data/images;
> }
> ```

该参数是一个正则表达式匹配结尾的所有URI `.gif`，`.jpg`或`.png`。正则表达式应以开头`~`。相应的请求将被映射到`/data/images` 目录。

当nginx选择一个`location`块来服务请求时，它首先检查 指定前缀的[位置](http://nginx.org/en/docs/http/ngx_http_core_module.html#location)指令，记住`location` 最长的前缀，然后检查正则表达式。如果存在与正则表达式匹配的内容，则nginx会选择此匹配项`location`，否则，它将选择之前记住的匹配项 。

代理服务器的最终配置如下所示：

> ```
> server {
>     location / {
>         proxy_pass http://localhost:8080/;
>     }
> 
>     location ~ \.(gif|jpg|png)$ {
>         root /data/images;
>     }
> }
> ```

该服务器将过滤以`.gif`， `.jpg`或结束的请求，`.png` 并将它们映射到`/data/images`目录（通过将URI添加到 `root`伪指令的参数），并将所有其他请求传递到上面配置的代理服务器。

要应用新配置，请`reload`按照前面几节中的说明将信号发送到nginx。

还有许多[其他](http://nginx.org/en/docs/http/ngx_http_proxy_module.html) 指令可用于进一步配置代理连接。



设置FastCGI代理

nginx可用于将请求路由到FastCGI服务器，该服务器运行使用各种框架和编程语言（例如PHP）构建的应用程序。

与FastCGI服务器一起使用的最基本的nginx配置包括使用 [fastcgi_pass](http://nginx.org/en/docs/http/ngx_http_fastcgi_module.html#fastcgi_pass) 指令而不是`proxy_pass`指令，以及[fastcgi_param](http://nginx.org/en/docs/http/ngx_http_fastcgi_module.html#fastcgi_param) 指令来设置传递给FastCGI服务器的参数。假设可通过访问FastCGI服务器`localhost:9000`。以上一节中的代理配置为基础，用`proxy_pass`指令 替换`fastcgi_pass`指令并将参数更改为 `localhost:9000`。在PHP中，该`SCRIPT_FILENAME`参数用于确定脚本名称，该`QUERY_STRING` 参数用于传递请求参数。结果配置为：

> ```
> server {
>     location / {
>         fastcgi_pass  localhost:9000;
>         fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
>         fastcgi_param QUERY_STRING    $query_string;
>     }
> 
>     location ~ \.(gif|jpg|png)$ {
>         root /data/images;
>     }
> }
> ```

这将设置一个服务器，该服务器将把对静态图像的请求以外的所有请求路由到`localhost:9000`通过FastCGI协议运行的代理服务器 。