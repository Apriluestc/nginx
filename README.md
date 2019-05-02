# nginx 基本命令

- nginx 服务启动
  - nginx
  - systemctl start nginx.service
- nginx 服务停止
  - nginx -s stop
  - nginx -s quit
  - systemctl nginx.service
  - killall nginx
- nginx 服务重启
  - systemctl restart nginx.service
- 重新载入配置文件
  - nginx -s reload

# nginx 配置文件

```bash
user  nginx;
#运行用户，默认即是 nginx，可以不进行配置

worker_processes  1;
#Nginx 进程，一般设置为和 CPU 核数一样

error_log  /var/log/nginx/error.log warn;
#错误日志存放目录

pid        /var/run/nginx.pid;
#进程 pid 存放位置

events {
    worker_connections  1024;
    #单个后台进程的最大并发数
}

http {
    include       /etc/nginx/mime.types;
    #文件扩展名与类型映射表

    default_type  application/octet-stream;
    #默认文件类型

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';
    #设置日志模式

    access_log  /var/log/nginx/access.log  main;
    #nginx 访问日志存放位置

    sendfile        on;
    #开启高效传输模式

    #tcp_nopush     on;
    #减少网络报文段的数量

    keepalive_timeout  65;
    #保持连接的时间，也叫超时时间

    #gzip  on;
    #开启 gzip 压缩

    include /etc/nginx/conf.d/*.conf;
    #包含的子配置项位置和文件
}
```
## 下期再会
