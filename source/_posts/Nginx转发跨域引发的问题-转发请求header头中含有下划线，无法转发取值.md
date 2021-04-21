---
title: Nginx转发跨域引发的问题-转发请求header头中含有下划线，无法转发取值
tags: [Nginx, Linux]
index_img: /img/bg/3.jpg #缩略图-a
banner_img: /img/bg/1.jpg #banner图-a
top_img: /img/md/md9.png #banner图-b
cover:  /img/md/md1.jpg #缩略图-b
date: 2021-01-14 15:38
updated: 2021-01-14 15:38

---
### 一、起因查找
**今天发现有个前后端分离站点通过nginx转发原以为是普通的跨域问题，就简单的在配置里加上了**

```
       location /API {
       add_header Access-Control-Allow-Origin *;
       add_header Access-Control-Allow-Headers 'DNT,X-CustomHeader,Keep-Alive,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type,_tag_,';
       add_header Access-Control-Allow-Methods GET,POST,OPTIONS,HEAD,PUT;
       add_header Access-Control-Allow-Credentials true;
  
       proxy_set_header x-real-ip $remote_addr;
       proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

	   if ( $request_method = 'OPTIONS' ) { 
		     return 200;
		}
      proxy_pass http://66.66.66.66:8888/API;

      
    }
```
**修改完发现无效果，遂去检查一下后端的跨域配置，也无果**


### 二、原因分析

**查了一下发现是nginx在代理转发默认会把header头中的参数带有下划线：_ 的自定义字段省略掉，所以后端就获取不到带下划线：_ 的自定义参数名，我这里传的参数这好歹下划线**

**看一下ng的官网对于客户端请求标头字段中启用或禁用下划线的说明 http://nginx.org/en/docs/http/ngx_http_core_module.html#underscores_in_headers**

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/548e5968d8d44dd1895197f7a022857c~tplv-k3u1fbpfcp-zoom-1.image)

**机翻一下**

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/763c114598954832adfd9fcd8dd9d6a6~tplv-k3u1fbpfcp-zoom-1.image)

**大体意思是默认的情况下会忽略掉带下划线的变量。要解决这个需要配置  underscores_in_headers off 改为 on**

**我们在继续查看一下ng的源码，https://trac.nginx.org/nginx/browser/nginx/src/http/ngx_http_parse.c**

**在ngx_http_parse_header_line() 的函数下面是这样的**
```
ngx_http_parse_header_line(ngx_http_request_t *r, ngx_buf_t *b,ngx_uint_t allow_underscores)

if (ch == '_') {
    if (allow_underscores) {
        hash = ngx_hash(0, ch);
        r->lowcase_header[0] = ch;
        i = 1;
    } else {
        r->invalid_header = 1;
    }
     break;
}

```
**也可以发现其中allow_underscores 是否允许下划线这个选项**

**so**

#### 三、解决方案

**在前后端nginx配置中添加**

```
underscores_in_headers on;
```

**nginx配置**
```
server
{
    listen 80;
    server_name api.2021.com;

    underscores_in_headers on;   #这里添加

    #REWRITE-END
    location / {

     proxy_pass http://66.66.66.66:8888;
    
    }

    #禁止访问的文件或目录
    location ~ ^/(\.user.ini|\.htaccess|\.git|\.svn|\.project|LICENSE|README.md)
    {
        return 404;
    }
    

    access_log  /usr/local/nginx/logs/api.2021.com.log;
    error_log  /usr/local/nginx/logs/api.2021.com.error.log;
}
```
**就OK了**
