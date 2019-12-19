---
layout: post
title: Cài đặt PM2 trên linux và sử dụng
tags: [pm2, nodejs, linux]
comments: true
---

<!-- Content here -->
## Cài đặt NodeJS và NPM trên linux
Cài đặt NodeJS `sudo apt-get install nodejs`

Cài đặt npm `sudo apt-get install npm`

Nên update system trước khi install `sudo apt-get update`

## Cài đặt PM2 trên linux
Cài đặt PM2 bằng npm global `npm i -g pm2`

Kiểm tra version PM2 `pm2 -v`

1. Khởi chạy lệnh `npm start` và đặt tên cho process bằng PM2 `pm2 start npm --name "Your_APP_Name" -- start`
2. Stop process bằng tên `pm2 stop "Your_APP_Name"`
3. Start process bằng tên `pm2 start "Your_APP_Name"`
4. Restart process bằng tên `pm2 restart "Your_APP_Name"`
5. Xem log 15 dòng mới nhất `pm2 log "Your_APP_Name"`
6. Xem log số dòng tùy ý (300) `pm2 log "Your_APP_Name" --lines 300`
7. Monitor process `pm2 monit`