# httpbin: HTTP Request & Response Service in Node.js

[![Build Status](https://travis-ci.org/isayme/node-httpbin.svg?branch=master)](https://travis-ci.org/isayme/node-httpbin)
[![Coverage Status](https://coveralls.io/repos/github/isayme/node-httpbin/badge.svg?branch=master)](https://coveralls.io/github/isayme/node-httpbin?branch=master)

## run
```bash
npm install
node app/app.js 8080
node app/app.js 8081
```

## Nginx config
```
upstream demo_server {
    server 127.0.0.1:8080;
    server 127.0.0.1:8081;
}
server {
    listen 80;
    server_name localhost;
    
    set $proxy_pass demo_server;
    location / {
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header Host $host;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_pass http://$proxy_pass;
    }
}
```
