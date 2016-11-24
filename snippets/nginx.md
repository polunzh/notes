# Nginx 常用配置

## 反向代理

### 最简单的反向代理
``` nginx
server {
    listen    { port };
    server_name    polun.me;
    location / {
        proxy_pass { ori server }
    }
}
```