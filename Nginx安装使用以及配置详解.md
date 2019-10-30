# Nginx安装使用以及配置详解

#### 1、官网下载window版本的Nginx

 				http://nginx.org/en/download.html 



![Nginx-1](C:\Users\Administrator\Desktop\Documents\Images\Nginx-1.png)

#### 2、解压到指定文件夹

![Nginx-1](C:\Users\Administrator\Desktop\Documents\Images\Nginx-2.png)

#### 3、打开conf文件夹，编辑nginx.conf文件

~~~conf

#user  nobody;
worker_processes  1;

#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

#pid        logs/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       mime.types;
    default_type  application/octet-stream;
    client_max_body_size 20m;

    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';

    #access_log  logs/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    keepalive_timeout  65;
	server_names_hash_bucket_size 512;
	include vhost/*.conf;	//vhost文件夹的所有的conf文件

    #gzip  on;



}

~~~

#### 4、在conf文件夹里新建一个文件夹vhost

所有新建的.conf文件放到此文件夹中，nginx会自动识别

![Nginx-1](C:\Users\Administrator\Desktop\Documents\Images\Nginx-3.png)

#### 5、server配置

~~~conf
server{
   listen 80;	//监听端口
   server_name heart.an1.scigeeker.com;	//域名请求地址

   location /{
      proxy_pass http://127.0.0.1:9051;	//下游实际请求地址
		proxy_http_version 1.1;
		proxy_set_header Upgrade $http_upgrade;
		proxy_set_header Connection keep-alive;
		proxy_set_header Host $host;
		proxy_cache_bypass $http_upgrade;
		proxy_set_header X-Real-IP $remote_addr;
		proxy_set_header X-Forwarded-Proto  $scheme;
   }
  
}

server{
  listen 80;
  server_name heartweb.an1.scigeeker.com;

  location /{
    root E:\Project\web\An1_CabinetHeartBeatWeb;
    index index.html;
  }
}
~~~

