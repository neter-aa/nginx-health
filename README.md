```bash
docker build -t nginx:alpine3.8 -f Dockerfile .
docker run --name nginx -v /data/nginx/config:/etc/nginx/conf.d -v /data/nginx/html:/usr/share/nginx/html -p80:80 -p8088:8088 -p60189:60189 -d nginx:alpine3.8
```

