docker file from nginx  
https://github.com/nginxinc/docker-nginx/blob/b71469ab815f580ba0ad658a32e91c86f8565ed4/stable/alpine/Dockerfile  
health check from https://github.com/zhouchangxun/ngx_healthcheck_module  
stream或者http 的 health check  都支持  

stream conf:  
/etc/nginx/conf.d/stream/*.conf  

```bash
docker build -t nginx:alpine3.8 -f Dockerfile .
docker run --name nginx -v /data/nginx/config:/etc/nginx/conf.d -v /data/nginx/html:/usr/share/nginx/html -p80:80 -p8088:8088 -p60189:60189 -d nginx:alpine3.8
```


```
upstream abc{
        hash $remote_addr consistent;
        server ip1:port max_fails=3 fail_timeout=600s;     # ip:port
        server ip2:port max_fails=3 fail_timeout=600s;     # ip:port
        check interval=5000 rise=2 fall=3 timeout=1000 type=tcp;
}

server {
        listen       60189;

        #access_log  /var/log/nginx/host.access.log  main;

        proxy_buffer_size 64k;
        proxy_connect_timeout 600s;
        proxy_timeout 5m;
        proxy_pass abc;

}
```
