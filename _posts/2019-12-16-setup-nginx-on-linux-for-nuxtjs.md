---
layout: post
title: Cài đặt NGINX trên linux cho project NuxtJS
tags: [nginx, nuxtjs, linux]
comments: true
---

<!-- Content here -->
<div class="flex justify-space-around">
  <img src="/img/nginx.png" height="150">
  <img src="/img/nuxt.png" height="150">
</div>

## Cài đặt NGINX trên linux

Chỉ cần chạy lệnh `sudo apt-get install nginx` . Sau khi cài đặt xong, kiểm tra cài đặt thành công bằng lệnh kiểm tra version cài đặt `sudo nginx -v` 

Webserver mới sẽ được cài đặt tại thư mục `/etc/nginx` 

1. Start nginx `sudo systemctl start nginx`
2. Stop nginx `sudo systemctl stop nginx`
3. Restart nginx `sudo systemctl restart nginx`

## Cấu hình NGINX cho project NuxtJS

`sudo vi /etc/nginx/sites-available/default` 

``` sh
// Redirect port 80 to 4000
server {
  listen 80 default_server;
  server_name _;
  location / {
    proxy_pass http://127.0.0.1:4000;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection 'upgrade';
    proxy_set_header Host $host;
    proxy_cache_bypass $http_upgrade;
  }
}
```

## Cấu hình SSL với NGINX

1. Tạo SSL certification trên [https://sslforfree.com](https://sslforfree.com), làm theo hướng dẫn để download được 3 file `ca_bundle.crt` , `certificate.crt` , `private.key` 
2. Copy 3 file này lên server, đặt vào thư mục bất kì
3. Chỉnh sửa lại file `sudo vi /etc/nginx/sites-available/default` 
``` sh
server {
  listen 80 default_server;
  listen 443 ssl;
  listen [::]:443 ssl;
  ssl_certificate <đường dẫn tới file certificate.crt>;
  ssl_certificate_key <đường dẫn tới file private.key>;
  ...
}
```
4. Start nginx `sudo systemctl start nginx` hoặc restart nginx `sudo systemctl restart nginx` 

## Cấu hình access mặc định vào https (redirect port 80 to 443)

1. Chỉnh sửa lại file `sudo vi /etc/nginx/sites-available/default` 
``` sh
server {
  listen 80;
  server_name _;
  return 301 https://$host$request_uri;
}
server {
  listen 80 default_server;
  listen 443 ssl;
  listen [::]:443 ssl;
  ssl_certificate <đường dẫn tới file certificate.crt>;
  ssl_certificate_key <đường dẫn tới file private.key>;
}
```
2. Start nginx `sudo systemctl start nginx` hoặc restart nginx `sudo systemctl restart nginx` 

